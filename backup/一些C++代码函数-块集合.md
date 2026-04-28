#### 判断素数 $O(\sqrt n)$
```cpp
bool isprime(int n) {
    if (n < 2) return false;
    for (int i = 2; i <= n / i; i ++)
        if (n % i == 0) return false;
    return true;
}
```

#### 最大公约数GCD $O(log n)$
```cpp
int gcd(int a, int b) {
    if (!b) return a;
    return gcd(b, a % b);
}
int lcm = (long long)a * b / gcd(a, b); // 最小公倍数
```

#### 分解质因数 $O(\sqrt n)$

```cpp
for (int j = 2; j <= x / j; j ++)
    while (x % j == 0) {
        cnt[j] ++;
        x /= j;
    }
if (x > 1) cnt[x] ++;
```

#### 欧拉筛 $O(n)$ 
```cpp
int primes[N / 10], f[N], cnt;
for (int i = 2; i < N; i ++) {
    if (!st[i]) primes[ ++ cnt] = i;
    for (int j = 1; i * primes[j] < N; j ++) {
        st[i * primes[j]] = true;
        if (i % primes[j] == 0) break;
    }
}
```

#### 快速幂 $O(log k)$
```cpp
int qmi(int a, int k) {
    int ans = 1;
    while (k) {
        if (k & 1) ans = (LL)ans * a % mod;
        k >>= 1;
        a = (LL)a * a % mod;
    }
    return ans;
}
```

#### 快速幂预处理阶乘/阶乘逆元求组合数 $O(nlogn + m)$
```cpp
int qmi(int a, int k) {
    int ans = 1;
    while (k) {
        if (k & 1) ans = (LL)ans * a % mod;
        k >>= 1;
        a = (LL)a * a % mod;
    }
    return ans;
}
int fact[N], infact[N];
void init(int n) {
    fact[0] = infact[0] = 1;
    for (int i = 1; i <= n; i ++) {
        fact[i] = (LL)fact[i - 1] * i % mod;
        infact[i] = qmi(fact[i], mod - 2);
    }
}
int C(int n, int m) {
    return (LL)fact[n] * infact[n - m] % mod * infact[m] % mod;
}
```

#### 递推预处理阶乘/阶乘逆元求组合数 $O(n + m)$
```cpp
int fact[N], inv[N], infact[N];
void init(int n) {
    fact[0] = infact[0] = fact[1] = infact[1] = inv[1] = 1;
    for (int i = 2; i <= n; i ++) {
        fact[i] = (LL)fact[i - 1] * i % mod;
        inv[i] = (mod - (LL)mod / i * inv[mod % i] % mod) % mod;
        infact[i] = (LL)infact[i - 1] * inv[i] % mod;
    }
}
int C(int n, int m) {
    return (LL)fact[n] * infact[n - m] % mod * infact[m] % mod;
}
```