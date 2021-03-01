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
