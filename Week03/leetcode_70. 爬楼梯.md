假设你正在爬楼梯。需要 n 阶你才能到达楼顶。

每次你可以爬 1 或 2 个台阶。你有多少种不同的方法可以爬到楼顶呢？
```
输入： 3
输出： 3
解释： 有三种方法可以爬到楼顶。
1.  1 阶 + 1 阶 + 1 阶
2.  1 阶 + 2 阶
3.  2 阶 + 1 阶
```

### c plus 

***
该题本质上是求斐波拉契数列。
* **递归**
```c
class Solution {
public:
    int climbStairs(int n) {
        if (n <= 2) return n;
        return climbStairs(n - 1) + climbStairs(n - 2);
    }
};
//以上做法是傻递归的形式，会有很多重复性的计算，浪费大量的时间
```

* **优化递归**
  将上一种做法中重复计算的数据保存到数组，供下次直接使用
```c
class Solution {
public:
    int climbStairs(int n) {
        if (n <= 2) return n;
        vector<int> res(n, 0);
        return f(n - 1) + f(n - 2);
    }
    int f(int n, vector<int>& res) {
        if (n <= 2) return n;
        if (res[n] != 0) return res[n];
        return res[n] = f(n - 1) + f(n - 2);
    }
};
```
* **迭代**
  类似于递归中保存计算过的数据。
```c
class Solution {
public:
    int climbStairs(int n) {
        if (n <= 2) return n;
        vector<int> res(n + 1, 0);
        res[1] = 1;
        res[2] = 2;
        for (int i = 3; i < n + 1; ++i) {
            res[i] = res[i - 1] + res[i -2];
        }
        return res[n];
    }
};
```
***