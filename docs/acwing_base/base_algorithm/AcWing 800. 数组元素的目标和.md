# 800. 数组元素的目标和

URL： https://www.acwing.com/problem/content/802/

给定两个升序排序的有序数组 AA 和 BB，以及一个目标值 xx。

数组下标从 00 开始。

请你求出满足 A[i]+B[j]=xA[i]+B[j]=x 的数对 (i,j)(i,j)。

数据保证有唯一解。

#### 输入格式

第一行包含三个整数 n,m,xn,m,x，分别表示 AA 的长度，BB 的长度以及目标值 xx。

第二行包含 nn 个整数，表示数组 AA。

第三行包含 mm 个整数，表示数组 BB。

#### 输出格式

共一行，包含两个整数 ii 和 jj。

#### 数据范围

数组长度不超过 105105。
同一数组内元素各不相同。
1≤数组元素≤1091≤数组元素≤109

#### 输入样例：

```
4 5 6
1 2 4 7
3 4 6 8 9
```

#### 输出样例：

```
1 1
```



```java
import java.util.*;
import java.io.*;

class Main {
    public static void main(String[] args) {
        Scanner sc = new Scanner(new InputStreamReader(System.in));
        int n = sc.nextInt();
        int m = sc.nextInt();
        int k = sc.nextInt();
        int[] q = new int[n];
        int[] s = new int[m];
        for (int i = 0; i < n; i++) q[i] = sc.nextInt();
        for (int j = 0; j < m; j++) s[j] = sc.nextInt();
        
        for (int i = 0, j = m - 1; i < n; i++) {
            while (j >= 0 && q[i] + s[j] > k) j--;
            if (q[i] + s[j] == k ) {
                System.out.println(i + " " + j);
                break;
            }
        }
        
    }
}
```

