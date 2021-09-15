## AcWing 849. Dijkstra求最短路 I

```
朴素Dijkstra
S： 当前已确定最短距离的点
1. dist[1] = 0, dist[i] = +无穷
2. for i : 1-n
	t <- 不在S中的距离最近的点
	s <- t
	用t更新到其他所有点的距离
```



**code:**

```java
import java.io.*;
import java.util.*;

class Main {
    static int N = 510;
    static int n, m;    // n点的个数， 边的个数
    static int[] dist = new int[N];   // dist数组： 每个位置到点1的距离
    static int[][] g = new int[N][N]; // 稠密图使用邻接矩阵存储
    static boolean[] st = new boolean[N];   // 相当于S集合，确定某个点到店1的最短距离
    
    
    private static int dijkstra() {
        Arrays.fill(dist, 100001);
        dist[1] = 0;
        // 循环n次
        for (int i = 1; i <= n; i++) {
            // 找到当前距离1号点最近的点
            int t = -1;
            for (int j = 1; j <= n; j++) 
                if (!st[j] && (t == -1 || dist[t] > dist[j])) 
                    t = j;
        
            st[t] = true;
            
            // 更新其他点到1号点的最近距离
            for (int j = 1; j <= n; j++) 
                dist[j] = Math.min(dist[j], dist[t] + g[t][j]);
            
        }
        
        if (dist[n] == 100001) return -1;
        else return dist[n];
    }
    
    public static void main(String[] args) throws Exception {
        BufferedReader in = new BufferedReader(new InputStreamReader(System.in));
        BufferedWriter out = new BufferedWriter(new OutputStreamWriter(System.out));
        
        String[] tmp = in.readLine().split(" ");
        n = Integer.parseInt(tmp[0]);
        m = Integer.parseInt(tmp[1]);
        
        for (int i = 1; i <= n; i++) Arrays.fill(g[i], 100001);
        
        while (m-- > 0) {
            tmp = in.readLine().split(" ");
            int a = Integer.parseInt(tmp[0]);
            int b = Integer.parseInt(tmp[1]);
            int c = Integer.parseInt(tmp[2]);
            g[a][b] = Math.min(c, g[a][b]);
        }
        
        out.write(dijkstra() + "");
        out.flush();
    }
}
```

