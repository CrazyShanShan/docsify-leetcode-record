

1. 01 背包问题： 每件物平最多只能用一次

   > 状态表示f(i, j) 
   >
   > - 集合
   >
   >   - 所有宣发
   >   - 条件 1. 从前i个物品中选，总体积<=j
   >
   > - 属性： max, min, 数量
   >
   >   return:  f (N, V) 
   >
   > 状态计算— 集合的划分 ： 1. 不漏 2. 不重

   

# 2. 01背包问题

URL : https://www.acwing.com/problem/content/2/

有 NN 件物品和一个容量是 VV 的背包。每件物品只能使用一次。

第 ii 件物品的体积是 vivi，价值是 wiwi。

求解将哪些物品装入背包，可使这些物品的总体积不超过背包容量，且总价值最大。
输出最大价值。

#### 输入格式

第一行两个整数，N，V，用空格隔开，分别表示物品数量和背包容积。

接下来有 NN行，每行两个整数 vi,wi，用空格隔开，分别表示第 i 件物品的体积和价值。

#### 输出格式

输出一个整数，表示最大价值。

#### 数据范围

0<N,V≤1000
0<vi,wi≤1000

#### 输入样例

```
4 5
1 2
2 4
3 4
4 5
```

#### 输出样例：

```
8
```



**二维动态规划**

```java
import java.util.*;
import java.io.*;

class Main {
    static final int N = 1010;
    static int[] v = new int[N];
    static int[] w = new int[N];
    static int[][] dp = new int[N][N];
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        int n, m;
        n = sc.nextInt();
        m = sc.nextInt();
        
        for (int i = 1; i <= n; i++) {
            v[i] = sc.nextInt();
            w[i] = sc.nextInt();
        }
        
        for (int i = 1; i <= n; i++) {
            for (int j = 0; j <= m; j++) {
                dp[i][j] = dp[i - 1][j];
                if (j >= v[i]) dp[i][j] = Math.max(dp[i][j], dp[i - 1][j - v[i]] + w[i]); 
            }
        }
        
        System.out.println(dp[n][m]);
    }
}
```

优化空间后

```
import java.util.*;
import java.io.*;

class Main {
    static final int N = 1010;
    static int[] v = new int[N];
    static int[] w = new int[N];
    static int[] dp = new int[N];
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        int n, m;
        n = sc.nextInt();
        m = sc.nextInt();
        
        for (int i = 1; i <= n; i++) {
            v[i] = sc.nextInt();
            w[i] = sc.nextInt();
        }
        
        for (int i = 1; i <= n; i++) {
            for (int j = m; j >= v[i]; j--) {
                dp[j] = Math.max(dp[j], dp[j - v[i]] + w[i]); 
            }
        }
        
        System.out.println(dp[m]);
    }
}
```



