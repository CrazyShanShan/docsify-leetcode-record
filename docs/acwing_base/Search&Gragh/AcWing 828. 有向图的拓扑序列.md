## AcWing 828. 有向图的拓扑序列

```
有向图  	拓扑序列
若一个由图中所有点构成的序列A满足：对于图中的每条边（x,y)，x在A中都出现在y之前，则称A是该图的一个拓扑序列
比如
(1,2) (1,3) (2,3)
1，2，3 就是一个拓扑序列
只有由环，就说明一定不存在拓扑序列，对于有向无环图一定存在拓扑序列，有向无环图也被称为拓扑图
入度为0的点可以作为起点，意味着没有任何一条边在自己前面。
一个有向无环图，一定至少存在一个入度为0的点
```

算法流程：

```python 
queue <-- 所有入度为0的电
while q 不空
		t <- 队头
		枚举t的所有出边	t ->j
			删除t->j，d[j]--;
			if d[j] == 0 
				queue <- j
```

邻接表实现

```java
import java.util.*;

class Main {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        int n = sc.nextInt();
        int m = sc.nextInt();
        int[] d = new int[n + 1];
        int cnt = 0;
        List<Integer> res = new ArrayList<>();
        List<List<Integer>> g = new ArrayList<>();
        for (int i = 0; i <= n; i++) g.add(new ArrayList<>());
        while (m-- > 0) {
            int a = sc.nextInt();
            int b = sc.nextInt();
            g.get(a).add(b);
            d[b]++;
        }

        Deque<Integer> q = new LinkedList<>();

        for (int i = 1; i <= n; i++) 
            if (d[i] == 0) q.offer(i);

        while (q.size() != 0) {
            int t = q.poll();   
            cnt++;
            res.add(t);
            for (int e: g.get(t)) {
                if (--d[e] == 0) q.offer(e);
            }
        }

        if (cnt == n) {
            res.forEach(item -> System.out.print(item+" "));
        } else System.out.println(-1);
    }
}
```

```java
import java.util.*;

class Main {
    
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        int n = sc.nextInt();
        int m = sc.nextInt();
        int[][] g = new int[n + 1][n + 1];
        int[] d = new int[n + 1];
        int[] res = new int[n + 1];
        int cnt = 0;
        while (m-- > 0) {
            int a = sc.nextInt();
            int b = sc.nextInt();
            if (g[a][b] == 0) d[b]++;
            g[a][b] = 1;

        }
        
        Deque<Integer> q = new LinkedList<>();
        // for (int i = 1; i <= n; i++) 
        //     if (d[i] == 0) q.offer(i);
        for (int i = 1; i <= n; i++) {
            if (d[i] == 0) q.offer(i);
        }

        
        while (q.size() != 0) {
            int t = q.poll();
            res[cnt++] = t;

            for (int i = 1; i <= n; i++) {
                if (g[t][i] == 1) {
                    // g[t][i] = 0;
                    if (--d[i] == 0) q.offer(i);
                }
            }
        }
        
        
        if (cnt == n) {
            for (int i = 0; i < n; i++) System.out.print(res[i] + " ");
        } else System.out.println(-1);
        
        
        
    }
}

```

