**二维前缀和**

<img src="../_ac_base_images/image-20210522110044680.png" alt="image-20210522110044680" style="zoom:50%;" />

<img src="../_ac_base_images/image-20210522105539073.png" alt="image-20210522105539073" style="zoom:50%;" />

# 796. 子矩阵的和

URL： https://www.acwing.com/problem/content/798/

输入一个 n 行 m 列的整数矩阵，再输入 q 个询问，每个询问包含四个整数 x1,y1,x2,y2，表示一个子矩阵的左上角坐标和右下角坐标。

对于每个询问输出子矩阵中所有数的和。

#### 输入格式

第一行包含三个整数 n，m，q。

接下来 n 行，每行包含 m 个整数，表示整数矩阵。

接下来 q 行，每行包含四个整数 x1,y1,x2,y2，表示一组询问。

#### 输出格式

共 q 行，每行输出一个询问的结果。

#### 数据范围

1≤n,m≤1000
1≤q≤200000,
1≤x1≤x2≤n,
1≤y1≤y2≤m,
−1000≤矩阵内元素的值≤1000

#### 输入样例：

```
3 4 3
1 7 2 4
3 6 2 8
2 1 2 3
1 1 2 2
2 1 3 4
1 3 3 4
```

#### 输出样例：

```
17
27
21
```



```java
import java.util.*;

class Main {
    public static void main(String[] args ){
        Scanner sc = new Scanner(System.in);
        int n = sc.nextInt();
        int m = sc.nextInt();
        int q = sc.nextInt();
        int[][] a = new int[n + 1][m +1];
        for (int i = 1; i <= n; i++) {
            for (int j = 1; j <= m; j++) {
                a[i][j] = sc.nextInt();
            }
        }

        // 前缀和
        int[][] s = new int[n + 1][m +1];
        for (int i = 1; i <= n; i++) {
            for (int j = 1; j <= m; j++) {
                s[i][j] = a[i][j] + s[i - 1][j] + s[i][j - 1] - s[i - 1][j - 1];
            }
        }

        while (q-- > 0) {
            int x1 = sc.nextInt();
            int y1 = sc.nextInt();
            int x2 = sc.nextInt();
            int y2 = sc.nextInt();
            System.out.println(s[x2][y2] - s[x1 - 1][y2] - s[x2][y1 - 1] + s[x1 - 1][y1 - 1]);
        }
    }
}

作者：CrazyShanShan
链接：https://www.acwing.com/activity/content/code/content/1261749/
来源：AcWing
著作权归作者所有。商业转载请联系作者获得授权，非商业转载请注明出处。
```

