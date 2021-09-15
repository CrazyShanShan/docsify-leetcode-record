## **AcWing 847. 图中点的层次**

```
BFS、 图的邻接表存储
1. queue <- 1
2. while queue 不空
		t <- 队头
		拓展t所有的邻点 x
		if (x 没有遍历过) queue <- x
		d[x] = d[t] + 1
```

**code:**

 ```java
import java.io.*;
import java.util.*;

class Main {
    
    static int N = 100010;
    static int n;
    static int[] e = new int[N];
    static int[] ne = new int[N];
    static int[] h = new int[N];
    static int[] d = new int[N];
    static int[] q = new int[N];
    static int idx = 0;
    
    
    
    private static void add(int a, int b) {
        e[idx] = b;
        ne[idx] = h[a];
        h[a] = idx++;
    }
    
    
    private static int bfs() {
        int hh = 0, tt = 0;
        q[0] = 1;
        Arrays.fill(d, -1);
        d[1] = 0;
        
        while (hh <= tt) {
            int t = q[hh++];
            
            for (int i = h[t]; i != -1; i = ne[i]) {
                int j = e[i];
                if (d[j] == -1) {
                    d[j] = d[t] + 1;
                    q[++tt] = j;
                }
            }
        }
        return d[n];
    }
    
    
    public static void main(String[] args) throws Exception {
        BufferedReader in = new BufferedReader(new InputStreamReader(System.in));
        BufferedWriter out = new BufferedWriter(new OutputStreamWriter(System.out));
        String[] tmp = in.readLine().split(" ");
        n = Integer.parseInt(tmp[0]);
        int m = Integer.parseInt(tmp[1]);
        Arrays.fill(h, -1);
        while (m-- > 0) {
            tmp = in.readLine().split(" ");
            int a = Integer.parseInt(tmp[0]);
            int b = Integer.parseInt(tmp[1]);
            add(a, b);
        }
        out.write(bfs() + "");
        out.flush();
    }
}
 ```

