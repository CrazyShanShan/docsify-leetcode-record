# 2816. 判断子序列

URL：https://www.acwing.com/problem/content/2818/

给定一个长度为 nn 的整数序列 a1,a2,…,ana1,a2,…,an 以及一个长度为 mm 的整数序列 b1,b2,…,bmb1,b2,…,bm。

请你判断 aa 序列是否为 bb 序列的子序列。

子序列指序列的一部分项按**原有次序排列**而得的序列，例如序列 {a1,a3,a5}{a1,a3,a5} 是序列 {a1,a2,a3,a4,a5}{a1,a2,a3,a4,a5} 的一个子序列。

#### 输入格式

第一行包含两个整数 n,mn,m。

第二行包含 nn 个整数，表示 a1,a2,…,ana1,a2,…,an。

第三行包含 mm 个整数，表示 b1,b2,…,bmb1,b2,…,bm。

#### 输出格式

如果 aa 序列是 bb 序列的子序列，输出一行 `Yes`。

否则，输出 `No`。

#### 数据范围

1≤n≤m≤1051≤n≤m≤105,
−109≤ai,bi≤109−109≤ai,bi≤109

#### 输入样例：

```
3 5
1 3 5
1 2 3 4 5
```

#### 输出样例：

```
Yes
```



```java
import java.util.*;

class Main {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        int n = sc.nextInt();
        int m = sc.nextInt();
        int[] a = new int[n];
        int[] b = new int[m];
        for (int i = 0; i < n; i++) a[i] = sc.nextInt();
        for (int j = 0; j < m; j++) b[j] = sc.nextInt();
        int i = 0;
        for (int j = 0; j < m; j++) {
            if (i < n && a[i] == b[j]) i++;
        }
        if (i == n) System.out.println("Yes");
        else System.out.println("No");
    }
}
```

