# 798. 差分矩阵

URL：https://www.acwing.com/problem/content/800/

输入一个 n 行 m 列的整数矩阵，再输入 q 个操作，每个操作包含五个整数x1,y1,x2,y2,c，其中(x1,y1) 和(x2,y2) 表示一个子矩阵的左上角坐标和右下角坐标。

每个操作都要将选中的子矩阵中的每个元素的值加上 c。

请你将进行完所有操作后的矩阵输出。

#### 输入格式

第一行包含整数 n,m,q。

接下来 n 行，每行包含 m 个整数，表示整数矩阵。

接下来 q 行，每行包含 5 个整数x1,y1,x2,y2,c，表示一个操作。

#### 输出格式

共 n 行，每行 m 个整数，表示所有操作进行完毕后的最终矩阵。

#### 数据范围

1≤n,m≤1000,
1≤q≤100000,
1≤x1≤x2≤n,
1≤y1≤y2≤m,
−1000≤c≤1000,
−1000≤矩阵内元素的值≤1000

#### 输入样例：

```
3 4 3
1 2 2 1
3 2 2 1
1 1 1 1
1 1 2 2 1
1 3 2 3 2
3 1 3 4 1
```

#### 输出样例：

```
2 3 4 1
4 3 4 1
2 2 2 2
```



```java
import java.util.*;
import java.io.*;

class Main {

    public static void insert(int[][] b, int x1, int y1, int x2, int y2, int c) {
        b[x1][y1] += c;
        b[x2 + 1][y1] -= c;
        b[x1][y2 + 1] -= c;
        b[x2 + 1][y2 + 1] += c;
    }

    public static void main(String[] args) throws Exception {
        BufferedReader in = new BufferedReader(new InputStreamReader(System.in));
        BufferedWriter out = new BufferedWriter(new OutputStreamWriter(System.out));
        String[] tmp = in.readLine().split(" ");
        int n = Integer.parseInt(tmp[0]);
        int m = Integer.parseInt(tmp[1]);
        int q = Integer.parseInt(tmp[2]);
        int[][] a = new int[n + 10][m + 10];
        int[][] b = new int[n + 10][m + 10];

        for (int i = 1; i <= n; i++) {
            tmp = in.readLine().split(" ");
            for (int j = 1; j <= m; j++) {
                a[i][j] = Integer.parseInt(tmp[j - 1]);
            }
        }

        for (int i = 1; i <= n; i++) {
            for (int j = 1; j <= m; j++) {
                insert(b, i, j, i, j, a[i][j]);
            }
        }

        while (q-- > 0) {
            tmp = in.readLine().split(" ");
            int x1 = Integer.parseInt(tmp[0]);
            int y1 = Integer.parseInt(tmp[1]);
            int x2 = Integer.parseInt(tmp[2]);
            int y2 = Integer.parseInt(tmp[3]);
            int c = Integer.parseInt(tmp[4]);
            insert(b, x1, y1, x2, y2, c);
        }

        for (int i = 1; i <= n; i++) {
            for (int j = 1; j <= m; j++) {
                b[i][j] += b[i - 1][j] + b[i][j - 1] - b[i - 1][j - 1];
            }
        }

        for (int i = 1; i <= n; i++) {
            for (int j = 1; j <= m; j++) {
                out.write(b[i][j] + " ");
            }
            out.write("\n");
        }
        out.flush();
        in.close();
        out.close();
    }
}

作者：CrazyShanShan
链接：https://www.acwing.com/activity/content/code/content/1262356/
来源：AcWing
著作权归作者所有。商业转载请联系作者获得授权，非商业转载请注明出处。
```

