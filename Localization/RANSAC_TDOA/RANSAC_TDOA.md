# 标题：使用RANSAC的鲁棒TDOA Chan定位算法

#### 作者：姜小明 @[github](https://github.com/JaminJiang)
#### 日期：2020-09-03
#### 关键字：RANSAC, TDOA, localization

> 如果我们知道点到各个监测站的距离，我们可以很方便的计算出位置。然而，一般情况下，我们很难获取当前点到各个监测站的绝对距离，却可以方便的获取其到各个监测站之间距离的差值。TDOA(Time Different Of Arrival)算法根据其定义，是一类根据距离差进行定位的方法，可解决上述问题，而其中Chan算法是一种准确高效的TDOA算法。另一方面，如果个别监测站偶发存在较大误差，可使用RANSAC（随机抽样一致性算法）思想，获取更鲁棒的解。

## 1. TDOA
TDOA定位是一种利用时间差进行定位的方法。通过测量信号到达监测站的时间，可以确定信号源的距离。利用信号源到各个监测站的距离(以监测站为中心，距离为半径作圆)，就能确定信号的位置。但是绝对时间一般比较难测量，通过比较信号到达各个监测站的绝对时间差，就能作出以监测站为焦点，距离差为长轴的双曲线，双曲线的交点就是信号的位置[百度百科-TDOA](https://baike.baidu.com/item/TDOA/6961547?fr=aladdin)。如下图，左图为给到监测站距离的情况下的定位方法，右侧为给定距离差的情况下的定位方法，即TDOA。
![TDOA concept](https://raw.githubusercontent.com/JaminJiang/MyBlogs/master/Localization/RANSAC_TDOA/RANSAC_TDOA_resources/TDOA.jpg)

### 1.1 Chan算法思路
除了待求的x、y，我们可以引入一个新的变量r1表示当前点到第一个监测站的距离。然后，使用4个点，可以构造出三个关于x、y、r1的方程，求解即可计算出一个结果。可是这么直接计算只能计算初略位置，因其忽略了r1和x、y之间的相关性。
Chan算法在计算初略位置后，构建了另一个关于$(x-x_1)^2$和$(y-y_1)^2$的方程，并利用加权最小二乘法求解出更精确的解。

### 1.2 算法
Chan算法只需求解一次最小二乘和两次加权最小二乘法即可得到精确的解。算法求解分解为如下三步。
#### 1.2.1 最小二乘法求解初略位置
使用最朴素的方法求解初略位置：引入一个新的未知量r1表示当前点到第一个监测站的距离。使用4个点可以构造三个关于$x$、$y$、$r_1$的方程。求解即可计算出一个初略位置。
如下图（参考[CSDN博客-Chan定位算法](https://blog.csdn.net/qq_23947237/article/details/82715784)）：
![TDOA step1](https://raw.githubusercontent.com/JaminJiang/MyBlogs/master/Localization/RANSAC_TDOA/RANSAC_TDOA_resources/TDOA-step1.png)
实现如下：
```
    // G_a*z_a=h
    Ga = gsl_matrix_alloc(matrix_row_num, coefficient_num);
    h = gsl_matrix_alloc(matrix_row_num, 1);

    // step 0. prepare data
    int index_0 = effective_landmark_indexes[0];
    double k_0 = landmarks[index_0].x * landmarks[index_0].x + landmarks[index_0].y * landmarks[index_0].y;
    for (int i = 0; i < matrix_row_num; i++) {
        int index_ip1 = effective_landmark_indexes[i+1];
        double r_i_0 = difference_of_distances[index_ip1] - difference_of_distances[index_0];
        gsl_matrix_set(Ga, i, 0, -(landmarks[index_ip1].x - landmarks[index_0].x));
        gsl_matrix_set(Ga, i, 1, -(landmarks[index_ip1].y - landmarks[index_0].y));
        gsl_matrix_set(Ga, i, 2, -r_i_0);
        double k_i = landmarks[index_ip1].x * landmarks[index_ip1].x + landmarks[index_ip1].y * landmarks[index_ip1].y;
        gsl_matrix_set(h, i, 0, 0.5*(r_i_0 * r_i_0 - k_i + k_0));
    }

    // step 1. the 1st least square, to get a raw position.
    // Za0 = inv(Ga'*inv(Q)*Ga)*Ga'*inv(Q)*h'
    Za0 = gsl_matrix_alloc(coefficient_num, 1);
    int solve_res = 0;
    solve_res = solve(Ga, h, Q, Za0);
    double Mx0 = gsl_matrix_get(Za0, 0, 0);
    double My0 = gsl_matrix_get(Za0, 1, 0);
```
#### 1.2.2 加权最小二乘法精细化初略位置
在上一步中，假设$x$、$y$、$r_1$相对独立，且误差权重相同（方差相同）。现在我们求出了$x$、$y$、$r_1$初略值，可以计算误差权重（协方差的倒数），并进行加权最小二乘法精细化位置。
经推导，协方差与距离的平方成正比，即$\Sigma = BQB$.
实现如下：
```
    B = gsl_matrix_alloc(matrix_row_num, matrix_row_num);
    gsl_matrix_set_identity(B);
    for (int i = 0; i < matrix_row_num; i++) {
        int index_ip1 = effective_landmark_indexes[i+1];
        gsl_matrix_set(B, i, i, sqrt((landmarks[index_ip1].x - Mx0) * (landmarks[index_ip1].x - Mx0) + (landmarks[index_ip1].y - My0) * (landmarks[index_ip1].y - My0)));
    }

    tmp_for_calc_FI = gsl_matrix_alloc(matrix_row_num, matrix_row_num);
    matrix_multiplication(B, Q, tmp_for_calc_FI);
    FI = gsl_matrix_alloc(matrix_row_num, matrix_row_num);
    matrix_multiplication(tmp_for_calc_FI, B, FI);
    int inverse_res = 0;
    inverse_res = matrix_inverse_inplace(FI);
    if (!inverse_res) {
        success_flag = 0;
        goto LABEL_FREE_BEFORE_EXIT;
    }

    Za1 = gsl_matrix_alloc(coefficient_num, 1);
    solve_res = solve(Ga, h, FI, Za1);
    double Mx1 = gsl_matrix_get(Za1, 0, 0);
    double My1 = gsl_matrix_get(Za1, 1, 0);
```
其中，加权最小二乘的计算公式为：

![weighted least square](https://raw.githubusercontent.com/JaminJiang/MyBlogs/master/Localization/RANSAC_TDOA/RANSAC_TDOA_resources/TDOA-weighted_least_square.png)

加权最小二乘算法实现：
```
int solve(gsl_matrix* G, gsl_matrix* b, gsl_matrix* weight, gsl_matrix* result) {
    int ret = 1;
    int coefficient_num = G->size2;
    int matrix_row_num = b->size1;
    gsl_matrix* GT = NULL;
    gsl_matrix* matrix_3xn_A1 = NULL;
    gsl_matrix* matrix_3X3_A2 = NULL;
    gsl_matrix* matrix_3Xn_A3 = NULL;
    gsl_matrix* matrix_3Xn_A4 = NULL;
    GT = gsl_matrix_alloc(coefficient_num, matrix_row_num);
    gsl_matrix_transpose_memcpy(GT, G);

    matrix_3xn_A1 = gsl_matrix_alloc(coefficient_num, matrix_row_num);
    matrix_multiplication(GT, weight, matrix_3xn_A1);
    matrix_3X3_A2 = gsl_matrix_alloc(coefficient_num, coefficient_num);
    matrix_multiplication(matrix_3xn_A1, G, matrix_3X3_A2);
    int invert_success = matrix_inverse_inplace(matrix_3X3_A2);
    if (!invert_success) {
        ret = 0;
    } else {
        matrix_3Xn_A3 = gsl_matrix_alloc(coefficient_num, matrix_row_num);
        matrix_multiplication(matrix_3X3_A2, GT, matrix_3Xn_A3);
        matrix_3Xn_A4 = gsl_matrix_alloc(coefficient_num, matrix_row_num);
        matrix_multiplication(matrix_3Xn_A3, weight, matrix_3Xn_A4);
        matrix_multiplication(matrix_3Xn_A4, b, result);
        ret = 1;
    }
    gsl_matrix_free(GT);
    gsl_matrix_free(matrix_3xn_A1);
    gsl_matrix_free(matrix_3X3_A2);
    gsl_matrix_free(matrix_3Xn_A3);
    gsl_matrix_free(matrix_3Xn_A4);
    
    return ret;
}
```
需要注意的是，在矩阵求逆的过程中，可能遇到矩阵不可逆，或是矩阵为"病态矩阵"，可通过条件数判定，具体方法参考项目代码。
#### 1.2.3 无相关变量加权最小二乘法计算准确值
上一步中，我们忽略了$x$, $y$, $r_1$的相关性。这里，我们构建新的关于$(x-x_1)^2$和$(y-y_1)^2$的方程。利用上一步计算的较准确位置，计算协方差（权重），并最终利用加权最小二乘法计算准确值。
方程如下（参考[CSDN博客-Chan定位算法](https://blog.csdn.net/qq_23947237/article/details/82715784)）：
![TDOA step3](https://raw.githubusercontent.com/JaminJiang/MyBlogs/master/Localization/RANSAC_TDOA/RANSAC_TDOA_resources/TDOA-step3.png)

权重计算参考论文[1]。
算法实现如下：
```
    // Step 3. the 3rd weighted least square, using a new equation which has no correlated arguments in it(unlike the 2 least square problems above).
    // Za2=inv(sGa'*inv(sFI)*sGa)*sGa'*inv(sFI)*sh  in which  sFI=4*sB*CovZa*sB  and  CovZa=inv(Ga'*inv(FI)*Ga) .
    GT = gsl_matrix_alloc(coefficient_num, matrix_row_num);
    gsl_matrix_transpose_memcpy(GT, Ga);
    tmp_for_calc_CovZa = gsl_matrix_alloc(coefficient_num, matrix_row_num);
    matrix_multiplication(GT, FI, tmp_for_calc_CovZa);
    CovZa = gsl_matrix_alloc(coefficient_num, coefficient_num);
    matrix_multiplication(tmp_for_calc_CovZa, Ga, CovZa);
    
    inverse_res = matrix_inverse_inplace(CovZa);
    if (!inverse_res) {
        success_flag = 0;
        goto LABEL_FREE_BEFORE_EXIT;
    }

    // B'
    sB = gsl_matrix_alloc(coefficient_num, coefficient_num);
    gsl_matrix_set_zero(sB);
    
    gsl_matrix_set(sB, 0, 0, Mx1 - landmarks[index_0].x);
    gsl_matrix_set(sB, 1, 1, My1 - landmarks[index_0].y);
    gsl_matrix_set(sB, 2, 2, gsl_matrix_get(Za1, 2, 0));
    // FI'
    tmp_for_calc_sFI = gsl_matrix_alloc(coefficient_num, coefficient_num);
    matrix_multiplication(sB, CovZa, tmp_for_calc_sFI);
    sFI = gsl_matrix_alloc(coefficient_num, coefficient_num);
    matrix_multiplication(tmp_for_calc_sFI, sB, sFI);
    gsl_matrix_scale(sFI, 4);
    inverse_res = matrix_inverse_inplace(sFI);
    if (!inverse_res) {
        success_flag = 0;
        goto LABEL_FREE_BEFORE_EXIT;
    }
    // Ga'
    double sGa_arr[3][2] = {1,0,0,1,1,1};
    sGa = gsl_matrix_alloc(coefficient_num, 2);
    for (int i = 0; i < coefficient_num; i++) {
        for (int j = 0; j < 2; j++) {
            gsl_matrix_set(sGa, i, j, sGa_arr[i][j]);
        }
    }
    sh = gsl_matrix_alloc(coefficient_num, 1);
    gsl_matrix_set_zero(sh);
    gsl_matrix_set(sh, 0, 0, (Mx1 - landmarks[index_0].x) * (Mx1 - landmarks[index_0].x));
    gsl_matrix_set(sh, 1, 0, (My1 - landmarks[index_0].y) * (My1 - landmarks[index_0].y));
    gsl_matrix_set(sh, 2, 0, gsl_matrix_get(Za1, 2, 0) * gsl_matrix_get(Za1, 2, 0));
    Za2 = gsl_matrix_alloc(2, 1);

    solve_res = solve(sGa, sh, sFI, Za2);
```
最后，由于我们这一步求出来的是$(x-x_1)^2$和$(y-y_1)^2$，所以可以根据($x_1$, $y_1$)坐标确定四个点，再将前两步算出的位置作为先验，排除其他位置，就可以算出准确位置，代码如下：
```
    double delta_x_0_abs = gsl_matrix_get(Za2, 0, 0) > 0 ? sqrt(gsl_matrix_get(Za2, 0, 0)) : 0;
    double delta_y_0_abs = gsl_matrix_get(Za2, 1, 0) > 0 ? sqrt(gsl_matrix_get(Za2, 1, 0)) : 0;
    double popssible_poses[4][2] = {
        {landmarks[index_0].x - delta_x_0_abs, landmarks[index_0].y - delta_y_0_abs}, 
        {landmarks[index_0].x + delta_x_0_abs, landmarks[index_0].y - delta_y_0_abs},
        {landmarks[index_0].x - delta_x_0_abs, landmarks[index_0].y + delta_y_0_abs},
        {landmarks[index_0].x + delta_x_0_abs, landmarks[index_0].y + delta_y_0_abs}
    };
    // choose the one based on pre-aquired position.
    int best_index = -1;
    double smallest_distance_2_za1 = DBL_MAX;
    for (int i = 0; i < 4; i++) {
        double square_distance_2_za1 = (Mx1 - popssible_poses[i][0]) * (Mx1 - popssible_poses[i][0]) + (My1 - popssible_poses[i][1]) * (My1 - popssible_poses[i][1]);
        if (square_distance_2_za1 < smallest_distance_2_za1) {
            best_index = i;
            smallest_distance_2_za1 = square_distance_2_za1;
        }
    }
    result_pos->x = popssible_poses[best_index][0];
    result_pos->y = popssible_poses[best_index][1];
```
## 2. RANSAC 提升鲁棒性
实际场景中，个别点偶发测量误差较大。这些误差大的点参与运算会导致计算的结果偏差大。针对这一问题，可以引入RANSAC（随机抽样一致性算法）思路来排除外点的影响：
1. “随机抽样”最小抽样集，计算一个初始解。
2. 在剩余集合中，选择符合初始解的内点并添加构成“一致集”。
3. 利用一致集重新拟合，获取更精确的解。
4. 重复上述过程数次，选出拟合数目最多，方差最小的解作为最终结果。

算法实现如下：
```
/***
 * @description: TDOA problem solved by method Chan, using ransac for robustness. 
 *              Details for method Chan: A simple and Efficient Estimator for Hyperbolic Location.
 * @input:
 *      landmarks: containing all landmarks' positions in the map.
 *      distances: relative distances from landmark to current position for TDOA problem. 
 *                 Only the distance of the detected(effective) landmarks need to be set.
 *      effective_landmark_mask: mask that indicates which landmarks are detected(effective). 
 *      total_landmark_num: The length of landmarks, distances, and effective_landmark_mask are all total_landmark_num.
 *      std_dev: the standard deviation of measurements, this value is used to filter noise data.
 * @output:
 *      result_pos: the result position.
 * @return: success or not. The method may fail when the effective landmarks are too less, or they are in one line, 
 *          or some matrix operations failed.
 ***/
int tdoa_ransac(const Position2D landmarks[], const double distances[], 
        const int effective_landmark_mask[], int total_landmark_num, double std_dev,
        Position2D* result_pos) { // ransac
    double residual_best = DBL_MAX;
    int fit_cnt_best = -1;

    int sample_output_indexes[RANSAC_MAX_ITERATION][CALCULABLE_LEAST_CNT];
    getAllSampleIndexes(effective_landmark_indexes, effective_landmark_num, CALCULABLE_LEAST_CNT, RANSAC_MAX_ITERATION, sample_output_indexes);

    int sample_indexes_best[CALCULABLE_LEAST_CNT];
    int* all_fit_indexes = (int*)malloc(sizeof(int) * effective_landmark_num);
    int* all_fit_indexes_best = (int*)malloc(sizeof(int) * effective_landmark_num);
    Position2D tmp_pos;
    for (int i = 0; i < RANSAC_MAX_ITERATION; i++) {
        int* sample_indexes = sample_output_indexes[i];
        int success_once = tdoa_chan(landmarks, distances, total_landmark_num, 
            sample_indexes, CALCULABLE_LEAST_CNT, threshold, &tmp_pos);
        if (success_once) {
            double total_residual = DBL_MAX;
            int n = get_all_fit_indexes(landmarks, distances, total_landmark_num, effective_landmark_indexes, effective_landmark_num, 
                sample_indexes, CALCULABLE_LEAST_CNT, &tmp_pos, threshold, 
                all_fit_indexes, &total_residual);
            if (n > fit_cnt_best || (n == fit_cnt_best && total_residual < residual_best)) {
                residual_best = total_residual;
                fit_cnt_best = n;
                for (int j = 0; j < n; j++) {
                    all_fit_indexes_best[j] = all_fit_indexes[j];
                }
                for (int j = 0; j < CALCULABLE_LEAST_CNT; j++) {
                    sample_indexes_best[j] = sample_indexes[j];
                }
                result_pos->x = tmp_pos.x;
                result_pos->y = tmp_pos.y;
                success_flag = 1;
            }
        }
    }
    // refine model
    if (success_flag) {
        if (ENABLE_RANSAC_REFINE && fit_cnt_best > CALCULABLE_LEAST_CNT) {
            Position2D pos_refined;
            int success_once = tdoa_chan(landmarks, distances, total_landmark_num, 
                all_fit_indexes_best, fit_cnt_best, threshold, &pos_refined);
            if (success_once) {
                double residual_refined = 0.0;
                double* distances_estimated = (double*)malloc(sizeof(double) * total_landmark_num);
                memset(distances_estimated, 0, sizeof(double) * total_landmark_num);
                for (int i = 0; i < total_landmark_num; i++) {
                    distances_estimated[i] = sqrt(pow((landmarks[i].x - pos_refined.x), 2) + pow((landmarks[i].y - pos_refined.y), 2));
                }
                residual_refined = calc_total_residual(distances, distances_estimated, sample_indexes_best, CALCULABLE_LEAST_CNT, all_fit_indexes_best, fit_cnt_best);
                if (residual_refined < residual_best) {
                    result_pos->x = pos_refined.x;
                    result_pos->y = pos_refined.y;
                }
                free(distances_estimated);
            }
        }
    }
    free(all_fit_indexes);
    free(all_fit_indexes_best);
}
```
其中effective_landmark_mask是用来标识地图中所有监测站之中，哪些监测站本次测量有数据，为1表示有数据，为0表示无数据。
# 3 项目描述
全部工程代码：[github-RANSAC_TDOA_CHAN](https://github.com/JaminJiang/RANSAC_TDOA_CHAN)

项目使用C语言实现了TDOA Chan定位算法，并使用了RANSAC思想排除异常点的干扰，获取稳定的解。本项目中实现了两个版本的Chan算法，一个是基于gsl运算库（ransac_tdoa_gsl.h），另一个不依赖gsl库（ransac_tdoa.h）。main.c中包含了一段测试代码。编译方式和gsl库配置方法详见readme.md

## 4. 算法评估
经测试算法运行效率高，精度高，且可以排除外点的干扰。

# 5. 参考文献
1. Chan, Yiu-Tong, and K. C. Ho. “A simple and efficient estimator for hyperbolic location.” IEEE Transactions on signal processing 42.8 (1994): 1905-1915.