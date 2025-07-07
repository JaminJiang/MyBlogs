---
slug: algorithm-tao
title: 算法面试宝典：道法术器（道法篇）
date: 2025-04-06T20:31:27.154Z
excerpt: 算法面试的本质是对复杂问题的拆解与优化能力的考察。本文从“道法术器”四个层次展开，深入探讨如何通过方法论、思维方式和工具选择，快速找到解题思路并高效实现。无论你是算法新手还是进阶选手，掌握这些核心思想，都能在面试中脱颖而出。
coverImage: https://pic.interview-genie.com/09-algorithm-tao-main-interview-algorithms-bible.png
tags:
  - Documentation
---

# 前言
算法面试的本质是对复杂问题的拆解与优化能力的考察。本文从“道法术器”四个层次展开，深入探讨如何通过方法论、思维方式和工具选择，快速找到解题思路并高效实现。无论你是算法新手还是进阶选手，掌握这些核心思想，都能在面试中脱颖而出。  
![算法面试宝典-道法术器](https://pic.interview-genie.com/09-algorithm-tao-main-interview-algorithms-bible.png)

# 道：大道至简，衍化至繁
> “道生一，一生二，二生三，三生万物”——《道德经》  

![算法面试宝典-道](https://pic.interview-genie.com/09-algorithm-tao-tao.jpg)

复杂的系统由简单的规则演化而来。我们可以从系统的表象中推敲出其内在的规则，然后用这个规则去理解系统、控制系统。  
硕士毕业找工作那会，刷 Leetcode 算法面试新题的时候，我总是毫无头绪，看完答案之后，又总是捶胸顿足“我咋没想到呢”。于是我开始思考，有没有什么方法可以快速想到解题思路。通过总结刷过的题型，我整理出了一系列想出解题思路的方法论。继续深入思考，我发现，算法问题的解决之道，往往蕴含在“将复杂问题变化为已知解法的简单问题”这一核心“道”理中。

# 法：以道驭术，万变归宗
> “臣之所好者道也，进乎技矣”——《庄子·养生主》  

![算法面试宝典-法](https://pic.interview-genie.com/09-algorithm-tao-fa.jpg)

此语道破了技艺与道法的高下之别。真正的算法高手，不是记忆千种解法，而是掌握十种可组合的元技能。  
上一章提到解算法题的“道”在于“将复杂问题变化为已知解法的简单问题”，本章我将列出我归纳出的四大“变化”之“法”：
## 1. 问题拆解：从整体到局部的智慧
> "天下难事必作于易，天下大事必作于细"——《道德经》  

复杂问题往往让人无从下手，但如果我们能将其拆解为更小的部分，问题就会变得清晰。而拆解的方式可以分为按规模拆解和按流程步骤拆解：  
### 问题规模分解
#### 小样例推演
##### 从小数字开始推演  
- 示例：LeetCode 70. [爬楼梯](https://leetcode.com/problems/climbing-stairs/)  
  简介：计算爬到第n阶楼梯的方法数，每次可爬1或2阶。  
  思路：通过小数字推演（n=1有1种，n=2有2种，n=3=1+2种），发现是斐波那契数列，可用递推或动态规划实现。
##### 从低维度上开始推演  
- 示例：LeetCode 121. [买卖股票的最佳时机](https://leetcode.com/problems/best-time-to-buy-and-sell-stock/)  
  描述：在一维数组中找到买卖股票的最大利润（低买高卖）。  
  低维解法：遍历数组，记录历史最低价，计算当前价与最低价的差值。  
  高维推演：  
    类似题目：LeetCode 122. [买卖股票的最佳时机](https://leetcode.com/problems/best-time-to-buy-and-sell-stock-ii/) II（多次交易）  
    LeetCode 123. [买卖股票的最佳时机 III](https://leetcode.com/problems/best-time-to-buy-and-sell-stock-iii/)（最多 2 次交易）  
    LeetCode 188. [买卖股票的最佳时机 IV](https://leetcode.com/problems/best-time-to-buy-and-sell-stock-iv/)（最多 k 次交易）  
    思路：从单次交易（一维 DP）推演到多次交易（二维 DP，状态机）。
#### 递推
##### 数学归纳法（Recursion），问题规模从1推到n  
推导过程：  
  n=1，成立  
  n=k时成立能推导出n=k+1时成立。  
- 示例：LeetCode 206. [反转链表](https://leetcode.com/problems/reverse-linked-list/)  
  简介：将单链表完全反转  
  思路：递归实现，归纳证明：  
    基础情况：当链表只有1个节点时，反转结果即自身  
    归纳步骤：  
      假设已能反转前k个节点（head → ... → node_k）  
      对于k+1个节点，只需将node_{k+1}的next指向node_k  
      最终head的next置空即完成  
##### 备忘录法（Memoization），自顶向下，递归+缓存  
- 示例：LeetCode 509. [斐波那契数](https://leetcode.com/problems/fibonacci-number/)  
  简介：计算第n个斐波那契数。  
  思路：递归计算时缓存中间结果（如f(3)），避免重复计算，时间复杂度从O(2^n)降至O(n)。  
##### **动态规划**（Dynamic Programming），自底向上，迭代实现  
- 示例：LeetCode 322. [零钱兑换](https://leetcode.com/problems/coin-change/)
  简介：用最少数量的硬币凑出金额。  
  思路：自底向上迭代，dp[i] 表示金额 i 的最小硬币数，转移方程为 dp[i] = min(dp[i - coin] + 1)。  
##### **分治**（Divide and Conquer）  
- 示例：LeetCode 23. [合并K个排序链表](https://leetcode.com/problems/merge-k-sorted-lists/)  
  简介：合并k个有序链表为一个有序链表。  
  思路：将链表数组二分，递归合并左右两部分，再合并两个有序链表，时间复杂度优化至O(NlogK)。  

### 问题步骤分解  
把大象装进冰箱需要几步？答：三步，把冰箱门打开，大象塞进去，关上冰箱门。  
这个看似荒谬的回答其实蕴含深刻的解题智慧——任何复杂任务都可以分解为可执行的简单步骤。  
- 示例：LeetCode 54. [螺旋矩阵](https://leetcode.com/problems/spiral-matrix/)  
  简介：按顺时针螺旋顺序返回矩阵所有元素。  
  思路：逐层剥离法：  
    定义四边界：初始化上、下、左、右四个边界。  
    按层遍历：依次遍历顶行→右列→底行→左列，每遍历完一层后收缩边界。  
    每层处理独立，逻辑重复但步骤清晰。  

## 2. 迭代优化的演变：从低效到高效的进化
> “苟日新，日日新，又日新”——《礼记·大学》  

优化的本质是找到更高效、更优雅的解法，而优化的过程往往从简单、直观的解法开始。面试过程中一时间想不到高效的解法，可以先给出简单暴力的解法，先保证正确。然后面试官一般会提醒你继续优化，甚至告诉你一些优化的方向。面试考察的不仅是技术，还有学习能力，通过思维过程展现学习能力、举一反三能力、应变能力也能加分。
### 从近似（**贪心**、启发式）解法开始优化  
- 示例：LeetCode 55. [跳跃游戏](https://leetcode.com/problems/jump-game/)  
  简介：给定一个非负整数数组 nums，数组中的每个元素代表你在该位置可以跳跃的最大长度。判断你是否能够到达最后一个下标。  
  解决思路：  
    贪心初始解：每步选择当前能跳的最远距离，但可能错过更优路径。  
    优化：从左到右遍历数组，维护一个变量 max_reach 表示当前能到达的最远位置。如果当前位置超过了 max_reach，则无法继续前进，返回 false。  
有些情况下，贪心解经证明即为正确解。  
- 示例：LeetCode 134. [环形加油站](https://leetcode.com/problems/gas-station/)
  简介：环形加油站，判断能否绕行一圈。  
  解决思路：贪心策略：总油量 sum(gas) >= sum(cost)，则必存在解。  
    遍历时累加 curr_tank，若为负则重置起点。  
    正确性证明：起点之后的剩余油量必然能覆盖之前的亏损。  
### 从低效（**暴力**、模拟）解法开始优化  
- 示例：LeetCode 1. [两数之和](https://leetcode.com/problems/two-sum/)  
  简介：在数组中找到和为target的两个数。  
  思路：暴力枚举优化为哈希表存储值到索引的映射，时间复杂度从O(n²)降至O(n)。  

## 3. 思考角度变换：横看成岭侧成峰
> “横看成岭侧成峰，远近高低各不同。”——苏轼《题西林壁》  

同一个问题，从不同的角度观察，可能会有完全不同的解法。
### 数据结构角度
数据结构是算法的基础，选择合适的数据结构往往能事半功倍。
#### 数据结构设计（Data structure）  
- 示例：LeetCode 200. [岛屿数量](https://leetcode.com/problems/number-of-islands/)  
  简介：计算二维网格中的岛屿数量。  
  思路：使用并查集。并查集（Union-Find）是一种用于处理一些不交集（Disjoint - Set）的合并及查询问题的数据结构，该算法的演化路径很有启发性。Union-Find最朴素的实现是Quick-Find（快速查找）和Quick-Union（快速合并）。进一步，避免树过高，合并时让较小的树成为较大树的子树，这就是按秩合并（Union by Rank）算法。再进一步，通过在查找过程中，将查找路径上的节点都指向根节点，有利于后续的查找操作更加高效，这就产生了路径压缩算法。  
  结合“按秩合并”和“路径压缩”的并查集算法模板如下：
  ```
  class ufs {
  private:
  vector<int> parent;
  public:
    ufs(int size): parent(vector<int>(size)){}
    // “路径压缩” 优化
    int find(x) {
      // 父节点为0或正数表示存储父节点id
      // 父节点为负数表示存储子节点数目
      return parent[x]<0?x:parent[x]=find(parent[x]);
    }
    // 按size合并
    int union(int x1, int x2){
      int f1=find(x1);
      int f2=find(x2);
      if (f1==f2) return -1;
      if(parent[f1]<parent[f2]){
        parent[f1]+=parent[f2]
        parent[f2]=f1
      } else {
        // opposite above.
      }
      return 0;
    }
  }
  ```
#### 图建模（Graph modeling）
##### 搜索   
- 深度优先搜索（DFS）  
  优化：**回溯法**=DFS+剪枝  
  实现思路：
  - 递归实现，逐步扩展状态。
  - 用一个栈path存储当前处理路径，处理前入栈，处理后出栈。
  - 用一个队列results存储所有可行的路径作为结果。
  - 加速技巧：1. 剪枝，2. memorization 缓存去重。
  
  算法模版：
  ```
  void dfs(type *input, type *path, int cur_or_gap, type *result) {
      if (数据非法/图出度为0) return;         // 终止条件
      if (cur == input.size || gap == 0) {  // 收敛条件
          TODO 将 path 放入result }          // 收敛路径放入结果集
      if (可以剪枝) return;                  // 加速1--剪枝
      if (已访问过) return;                  // 加速2--memorization 判重
      vector<type> new_states = state_extend(state, ...); // 扩展状态，判重可以放这
      for (state ... new_states) {          // 执行所有状态
          TODO 执行动作,修改path
          dfs(input, ++step/--gap, result); // 递归
          TODO 恢复path                      // 回溯
      }
  }
  ```
- 广度优先搜索（BFS）  
  常用于找最短路径。  
  优化：**分支限界法**=BFS+剪枝   
  实现思路：
    - 使用队列做逐层扩展（三种实现：1个队列，则元素state包含当前层数；或2个队列，即当前层队列+下层队列；或数字记录当层节点数）
    - set/visited_array 用于判重
    - 使用一颗用unordered_map<to, father>表示的树来存储逆向路径（可推出结果）。
  
  算法模板：
  ```
  template<typename state_t>
  vector<state_t> bfs(state_t &start,
                      bool (*state_is_target)(const state_t&),
                      vector<state_t>(*state_extend)(const state_t&, unordered_set<string> &visited)) {
      queue<state_t> next, current;
      unordered_set<state_t> visited;
      unordered_map<state_t, state_t> father;

      int level = 0;
      bool found = false;
      state_t target;

      current.push(start);
      visited.insert(start);

      while(!current.empty() && !found) {
          ++level;
          while(!current.empty() && !found) {
              const state_t state = current.front();
              current.pop();
              vector<state_t> new_states = state_extend(state, visited);
              for (state_t new_state : new_states) {
                  if(state_is_target(new_state)) { // 找到
                      found = true;
                      target = new_state;
                      father[new_state] = state;
                      break;
                  }
                  next.push(new_state);
                  // visited.insert(new_state) 放到 state_extend() 里。
                  father[new_state] = state;
              }
          }
          swap(next, current);
      }
      if(found) {
          return gen_path(father, target); // 反向推出路径
      } else {
          return vector<state_t>();
      }
  }
  ```

- 示例：LeetCode 200. [岛屿数量](https://leetcode.com/problems/number-of-islands/)  
  简介：同上，计算二维网格中的岛屿数量。  
  思路：也可以将网格建模为图，遍历每个点，通过DFS/BFS标记相邻陆地，统计连通分量数。

### 状态空间变换  
状态空间变换是将问题从一个难以处理的域转换到另一个更容易处理的域。
示例：  
- 傅立叶变换（Fourier transform）：将时域信号转换为频域信号，揭示信号的频率成分，广泛应用于信号处理、图像分析和微分方程求解等领域。
- 霍夫变换（Hough Transform）：用于检测图像中的几何形状（如直线、圆等），通过参数空间投票机制将复杂的形状检测问题转化为参数空间的峰值搜索问题。
- 配置空间(Configuration Space):在机器人运动规划中，将机器人的物理空间映射到其关节参数空间，从而简化路径规划问题，尤其适用于足型机器人或多自由度系统的运动优化。

### 对偶问题  
对偶问题揭示了问题的另一面，就像镜子中的倒影，虽然看似不同，但本质上是同一事物的两种表现。
示例：  
- SVM对偶问题：在支持向量机（SVM）中，原始问题涉及高维空间中的约束优化，而对偶问题通过拉格朗日乘子法转化为凸优化问题，更易求解且能自然引入核函数处理非线性分类。
- 最大流-最小割定理：在图论中，网络的最大流问题等价于其最小割问题，该定理不仅揭示了二者对偶关系，还提供了高效的算法设计思路（如Ford-Fulkerson算法）。

### 变种（Variation）或相似问题  
> “万物皆有源，殊途而同归。”——《列子·天瑞》  

世间万物虽形态各异，但往往有共同的起源和本质规律。算法问题亦如此，许多看似不同的问题，实则是同一类问题的不同变种。
- 示例：LeetCode 121. [买卖股票的最佳时机](https://leetcode.com/problems/best-time-to-buy-and-sell-stock/)  
  简介：计算股票的最大利润。  
  思路：与“最大子数组和”问题类似，可以使用动态规划解决。  

## 4. 问题领域（限定、条件）变换：宏观与微观的切换  
有时，我们可以通过扩大问题的视野，将其置于更广阔的领域中去考量，从而巧妙地避开那些特殊情况的繁琐处理，使整个问题的处理逻辑变得更加简洁明了。而另一方面，我们也可以将问题的范围缩小，聚焦于其所有的子问题，然后逐一击破。
### Generalization 泛化到已知问题或研究领域  
- 示例：斐波那契数列的递推关系可表示为矩阵乘法形式，进一步可推导出的闭式表达式为矩阵幂。通过快速幂（分治法）计算矩阵的 n 次幂，时间复杂度优化至 O(logn)，远优于传统线性方法。  
### Case Analysis 特化，特定情况（有限）下解法已知  
- 示例：LeetCode 65. [有效数字](https://leetcode.com/problems/valid-number/)  
  简介：判断字符串是否为有效数字。  
  思路：特化处理各种情况（符号、小数点、指数），通过有限状态机或条件分支逐一验证。  

上面的方法中，已覆盖各类“元算法”（上文用黑体标出），如贪心、暴力、分治法、动态规划、回溯法、分支限界法等。  
可以看到，所有心法中，都蕴含一个“变”字。  
- 变规模（拆解）
- 变效率（优化）
- 变视角（转化）
- 变视野（缩放）

**变化是唯一的不变。**这就是解算法题的“法”。  
算法面试不仅是技术的较量，更是思维方式的较量。通过掌握这些“变化之法”，我们不仅能解决算法题，还能在生活和工作中找到复杂问题的简单解法。  
我将这些“变化之法”整理到思维导图中（如下图），原始文件中，有更多示例和模板代码，想要进一步学习的朋友可以私聊我获取思维导图。  
![算法面试宝典-变化之法](https://pic.interview-genie.com/09-algorithm-tao-fa-mind-watermarked.jpg)  


# 术【TODO 道家名句】
掌握了"道"与"法"之后，我们需要具体的"术"来实现算法思想。这一章节将系统性地梳理算法面试中必备的数据结构与算法知识体系，它们如同武林高手的招式，需要勤加练习方能运用自如。
<素材1>
# 数据结构
数据结构是算法的基础，选择合适的数据结构往往能事半功倍。数据结构是存储和组织数据的方式，直接影响算法的效率。面试中常见的数据结构可分为线性结构和非线性结构：
## 线性结构
- 数组
  - <vector>
  - <list>
- 字符串
  - 字符串API (strlen, strcpy, strstr, atoi)
  - strstr
  - strcpy
    - memcpy(assemble effective) and memmove(call handle overlap)
  - pattern串预处理
    - KMP算法 (从前往后，根据模式串已匹配字符跳跃)
    - Boyer-Moore算法 (从后往前，坏字符+好后缀跳跃)
    - Rabin-Karp算法 (增量hash)
  - 匹配长串预处理
    - 后缀树
    - AC自动机+KMP+Trie
  - 模式匹配
    - 通配符匹配
    - 正则表达式

- 栈
  - <stack>

- 单项链
  - <queue>

- 队列
  - <queue>
  - priority_queue

## 非线性结构
- 树
  - 二叉树
    - 遍历
      - 先、中、后序（深度优先）
      - 层序（广度优先）
    - Morris Traversal
  - 2-3查找树
  - B树
  - B+树
    - 相同原理不同实现
  - B树
  - 红黑树
  - AVL树
  - 平衡查找树
  - 线索二叉树
    - 堆（数组实现）

- 并查集（索引结构实现）
  - quick find
  - quick union
  - 加权quick union
  - 路径压缩的加权quick union

- 线段树
- Trie
- 后缀树
- hash map

## 图
- 类型
  - 基于场景分类
    - Undirected Graph
    - Directed Graph
    - 稠密图
    - 稀疏图
    - 邻接矩阵
    - 邻接表
  - 基于实现分类
    - Shortest Path
    - Minimum Spanning Tree
    - 拓扑排序

- 其他
  - bitset
# 算法
## 按任务类型分类

### 排序 (for frequent search)
- 插入、交换、选择、基数（桶）排序
  - 直接插入排序
  - 插入排序
    - 折半插入排序
    - 希尔插入排序
  - 交换排序
    - 冒泡排序
    - 快速排序
  - 选择排序
    - 简单选择排序
    - 堆排序
- 归并排序
- 基数排序
  - LSD (Least significant digital)
  - MSD (Most significant digital)
- priority queues

### 查找
- 有序表查找
  - 二分查找
  - 插值查找
  - 稠密索引
  - 倒排索引
- 线性索引查找
- 树表查找
  - 树
    - 平衡查找树
    - 线索二叉树（堆，数组实现）
- 符号表
  - hash表
    - 冲突解决方法
      - 完美hash
      - 开放定址法
      - 拉链法
    - 变形
      - 位图
      - 布隆过滤器
    - 广度优先搜索
      - 分支限界法
    - 深度优先搜索
      - 回溯法

- 图
  - (路径) 搜索
    - 广度优先搜索 分支限界法
    - 深度优先搜索 回溯法
  - 连通分量
    - 循环+搜索+标记
    - Union-find

## 按算法思路分类 (meta algorithms)

### 动态规划法
- 动态规划与备忘录
  - 状态记录以Index为首
    - 序列型动态规划
      - 状态记录以Index为尾
        - 例：最大子序列和
        - 例：最长递增子序列
    - 双序列型动态规划
      - 例：最大公共子序列（不要求连续）
      - 例：最大公共子串
    - 区间型动态规划
      - 例：最大子数组乘积
      - 解法
        - 转化为序列型动态规划，部分问题状态转移只考虑上一步，如最大子数组乘积
        - 三重循环，枚举区间的长度
    - 划分型动态规划
      - 例：分割数组以得到最大的值（分割内元素可都改为其中最大值）
      - 解法
        - 转化为序列型动态规划，状态转移需遍历考虑前面 1 ~ max step 步
    - 矩阵型动态规划
      - 解法
        - 矩阵记录状态
        - 部分问题可优化为：使用循环数组记录状态，因为只与矩阵上一行有关
    - 背包型动态规划
      - 类型
        - 0-1背包无价值
        - 0-1背包有价值
        - 完全背包（每种物品可无限次放置）
        - 多重背包（每种物品有限个）
      - 解法
        - 序列型
        - 区间型
    - 博弈型动态规划
    - 树型动态规划
</素材1>
【TODO】根据上面<素材1>和</素材1>之间的内容扩展本章节《术》，注意起承转合，逻辑关联。

# 器：【TODO 道家名言】
> "君子生非异也，善假于物也"——《荀子·劝学》

在算法面试中，工具的选择和使用可以大大提高效率。这里推荐一个神器——面试精灵：
【TODO】解释【器】
<素材2>
# 为什么选择面试精灵？
## 顶级GPT
利用最先进的GPT技术，提供智能且上下文感知的面试回答，支持超长上下文，确保回复连贯且切题。
全新升级的AI引擎——**🚀极限精英版**性能出众。搭配 AI 联网搜索功能，回复准确率大幅提高。
![顶级GPT](https://pic.interview-genie.com/gpt-CN-sm.jpg)

## 实时互动体验
自研语音系统结合声纹识别技术，自动区分问题来源，提供实时反馈，支持多种语音交互方式。
![实时互动体验](https://pic.interview-genie.com/voice-CN-sm.jpg)

## 个性化
用户可上传简历和职位需求，定制化面试会话，获得与个人职业目标契合的智能回复。
![个性化](https://pic.interview-genie.com/customizable-CN-sm.jpg)

## 提示词优化
通过提示词优化，实现输出结果要点先行、条理清晰、并用黑体强调关键点，帮助您快速抓住回复重点。搭配前端优化，完美支持Latex公式、流程图、泳道图等显示，AI 输出展示简单直观。
![提示词优化](https://pic.interview-genie.com/prompt-optimized-CN-sm.jpg)

## 优质优价
提供免费使用配额，通过技术优化性价比，以低成本帮助用户撬动高薪工作。平均每场面试（1小时）耗费低于10元。发布阶段，所有功能免费开放，[快来体验吧](https://interview-genie.com)。
更详细的定价信息请点击链接查看：[面试精灵-定价](https://interview-genie.com/blog/pricing/)

![优质优价](https://pic.interview-genie.com/affordable-CN-sm.jpg)
具体定价参考：

## 笔试助手
通过多设备隐蔽互联，以支持跨设备远程截屏。然后使用视觉大模型自动识别问题，并帮您生成答案。只需访问网站，无需下载安装APP，无需复杂的设置，操作简单，隐蔽性强。
![笔试助手](https://pic.interview-genie.com/written-exam-CN-sm.jpg)

## 轻松可达
无需安装，随时随地访问，使面试准备变得轻松。
![轻松可达](https://pic.interview-genie.com/easily-accessible-CN-sm.jpg)

## 实时面试记录
记录面试会话，让用户可以回顾和改善表现，提升面试技巧。
![实时面试记录](https://pic.interview-genie.com/live-recording-CN-sm.jpg)

</素材2>
【TODO】根据上面<素材2>和</素材2>之间的内容，介绍并推荐“面试精灵”的优势和帮助。

# 面试实战建议【TODO 扩展本章节内容】
心态调整：
将面试视为技术交流
遇到难题时分解提问
展现学习能力和思维过程

五步解题法：
澄清题意（确认输入输出）
举例验证（小样例）
（可选）暴力解法（先保证正确）
优化分析（识别重复计算）
代码实现与分析

沟通技巧：
明确说出思考过程
先讲思路再写代码
主动分析时间/空间复杂度
主动举一反三介绍其他解法展示自己的知识面

【TODO】加入个人IP标识。
【TODO】原文地址，转载标明出处，翻版必究。

基于上面内容，按照要求完善“术”、“器”两个章节所有【TODO】部分，基于<素材>完善内容后需删除原始<素材>。并且要求保证“术”、“器”与前面的内容风格、格式一致。

