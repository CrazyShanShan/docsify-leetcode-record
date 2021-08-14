# 908. 最大相交区间数量

URL：https://www.acwing.com/problem/content/910/

给定 NN 个闭区间 [ai,bi][ai,bi]，请你在数轴上选择若干区间，使得选中的区间之间互不相交（包括端点）。

输出可选取区间的最大数量。

#### 输入格式

第一行包含整数 NN，表示区间数。

接下来 NN 行，每行包含两个整数 ai,biai,bi，表示一个区间的两个端点。

#### 输出格式

输出一个整数，表示可选取区间的最大数量。

#### 数据范围

1≤N≤1051≤N≤105,
−109≤ai≤bi≤109−109≤ai≤bi≤109

#### 输入样例：

```
3
-1 1
2 4
3 5
```

#### 输出样例：

```
2
```



```java
import java.util.*;
import java.io.*;

class Main {
    public static void main(String[] args ) throws Exception {
        BufferedReader in = new BufferedReader(new InputStreamReader(System.in));
        BufferedWriter out = new BufferedWriter(new OutputStreamWriter(System.out));
        int n = Integer.parseInt(in.readLine());
        String[] tmp = null;
        int[][] a = new int[n][2];
        for (int i = 0; i < n; i++) {
            tmp = in.readLine().split(" ");
            a[i][0] = Integer.parseInt(tmp[0]);
            a[i][1] = Integer.parseInt(tmp[1]);
        }
        Arrays.sort(a, (o1,o2) -> o1[1] - o2[1]);
        int res = 0, ed = Integer.MIN_VALUE;
        for (int i = 0; i < n; i++) {
            if (a[i][0] > ed) {
                ed = a[i][1];
                res++;
            }
        }
        out.write(res+"");
        out.flush();
    }
}
```

