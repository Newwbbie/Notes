### 2021-03-01
- 动态规划暴力法
```
static int fib1(int N) {
    if (N == 1 || N == 2) return 1;
    return fib1(N - 1) + fib1(N - 2);
}
```
- 动态规划字典法
```
static int fib2(int N) {
    int[] dic = new int[N + 1];
    return fun(dic, N);
}

static int fun(int[] dic, int n) {
    if (n == 1 || n == 2)   return 1;
    if (dic[n] != 0) {
        return dic[n];
    } else {
        System.out.println(n);
        dic[n] = fun(dic, n - 1) + fun(dic, n - 2);
        return dic[n];
    }
}
```
### 2021-03-02
```
// 自底向上，动态规划
Long fib3(int n) {
    if (n < 1)  return 0L;
    if (n == 1 || n == 2)   return 1L;
    Long[] dp = new Long[n + 1];
    dp[1] = dp[2] = 1L;
    for (int i = 3; i <= n; i++) {
        dp[i] = dp[i - 1] + dp[i - 2];
    }
    return dp[n];
}

// 状态压缩，空间复杂度变为O(1)
Long fib4(int n) {
    if (n < 1)  return 0L;
    if (n == 1 || n == 2)   return 1L;
    long prev = 1L, curr = 1L;
    for (int i = 3; i <= n; i++) {
        long sum = prev + curr;
        prev = curr;
        curr = sum;
    }
    return curr;
}
```
