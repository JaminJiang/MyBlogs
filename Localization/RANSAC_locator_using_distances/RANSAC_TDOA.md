# 标题：三边测距定位

#### 作者：姜小明 @[github](https://github.com/JaminJiang)
#### 日期：2020-09-06
#### 关键字：RANSAC, Multilateral positioning, localization

> 上一篇文章（《使用RANSAC的鲁棒TDOA Chan定位算法》）中提到，如果我们知道当前位置到各个基站的距离，可以很方便的确定位置。本篇文章我们简短介绍测距定位算法及其实现。

## 1. 三边测距定位算法简介
利用信号源到各个监测站的距离，最少通过三个监测站，我们就能确定信号的位置，该方法为三边测距定位。如下图,以监测站为中心，距离为半径作圆可以确定信号的位置：
![三边测距](https://raw.githubusercontent.com/JaminJiang/MyBlogs/master/Localization/RANSAC_locator_using_distances/resources/3line.jpg)

## 2. 算法
### 2.1 算法推导
算法推导如下图（参考[知乎-三边测量及多边测量](https://zhuanlan.zhihu.com/p/108771993)）：
![多边测距定位算法推导](https://raw.githubusercontent.com/JaminJiang/MyBlogs/master/Localization/RANSAC_locator_using_distances/resources/3line_algo.jpg)

### 2.2 算法实现
算法实现如下：
```
bool calculate_pos_with_index_(const Position2D landmarks[], const double distances[], const int effective_landmark_indexes[], int effective_landmark_num, 
        double* x_out, double* y_out) {
    if (is_landmarks_in_one_line(landmarks, effective_landmark_indexes, effective_landmark_num)) {
        printf("all landmarks in one line, cannot locate the position.\n");
        return false;
    }
    int matrix_row_num = effective_landmark_num - 1;
    int coefficient_num = 2;
    // Ax=b
    gsl_matrix* A = gsl_matrix_alloc(matrix_row_num, coefficient_num);
    gsl_matrix* a = gsl_matrix_alloc(matrix_row_num, coefficient_num);
    gsl_vector* b = gsl_vector_alloc(matrix_row_num);
    
    // result
	gsl_vector *sx = gsl_vector_alloc(coefficient_num);

    //Clear data
    gsl_matrix_set_zero(A);
    gsl_vector_set_zero(b);

    int index_last = effective_landmark_indexes[effective_landmark_num - 1];
    for (int i = 0; i < effective_landmark_num - 1; i++) {
        int index_i = effective_landmark_indexes[i];
        gsl_matrix_set(A, i, 0, (landmarks[index_i].x - landmarks[index_last].x) * 2);
        gsl_matrix_set(A, i, 1, (landmarks[index_i].y - landmarks[index_last].y) * 2);
        double bi = landmarks[index_i].x * landmarks[index_i].x - landmarks[index_last].x * landmarks[index_last].x
                        + landmarks[index_i].y * landmarks[index_i].y - landmarks[index_last].y * landmarks[index_last].y
                        + distances[index_last] * distances[index_last] - distances[index_i] * distances[index_i];
        gsl_vector_set(b, i, bi);
    }
    gsl_matrix_memcpy(a, A);
    gsl_vector* tau = gsl_vector_alloc(coefficient_num); //matrix_row_num, coefficient_num
    gsl_vector* residuals = gsl_vector_alloc(matrix_row_num);

    gsl_multifit_linear_workspace *w = gsl_multifit_linear_alloc(matrix_row_num, coefficient_num);
    gsl_multifit_linear_svd(A, w);
    double rcond = gsl_multifit_linear_rcond(w); // reciprocal condition number
    printf("conditional number is:%f\n", 1.0 / rcond);
    if (rcond < 1e-4) {
        printf("conditional number is too large, indicating that the problem is ill-conditioned.\n");
        return false;
    }
    double lambda_gcv = 0.1;
    double chisq, rnorm, snorm;
    gsl_multifit_linear_solve(0.0, A, b, sx, &rnorm, &snorm, w);

    *x_out = gsl_vector_get(sx, 0);
    *y_out = gsl_vector_get(sx, 1);

    gsl_matrix_free(A);
    gsl_matrix_free(a);
    gsl_vector_free(b);
    gsl_vector_free(tau);
    gsl_vector_free(sx);
    gsl_vector_free(residuals);
    return true;
}
```
## 3. 项目描述
全部工程代码：[github-RANSAC_Locator_using_distances](https://github.com/JaminJiang/RANSAC_Locator_using_distances)

项目使用C语言实现了三边测距定位算法。和上一篇定位文章类似地，本项目使用了RANSAC思想排除异常点的干扰，获取稳定的解。main.c中包含了一段测试代码。编译方式和gsl库配置方法详见readme.md。
