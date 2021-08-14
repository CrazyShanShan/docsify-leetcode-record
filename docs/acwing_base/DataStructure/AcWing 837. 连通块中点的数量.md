# 837. 连通块中点的数量

URL：https://www.acwing.com/problem/content/839/

给定一个包含 nn 个点（编号为 1∼n1∼n）的无向图，初始时图中没有边。

现在要进行 mm 个操作，操作共有三种：

1. `C a b`，在点 aa 和点 bb 之间连一条边，aa 和 bb 可能相等；
2. `Q1 a b`，询问点 aa 和点 bb 是否在同一个连通块中，aa 和 bb 可能相等；
3. `Q2 a`，询问点 aa 所在连通块中点的数量；

#### 输入格式

第一行输入整数 nn 和 mm。

接下来 mm 行，每行包含一个操作指令，指令为 `C a b`，`Q1 a b` 或 `Q2 a` 中的一种。

#### 输出格式

对于每个询问指令 `Q1 a b`，如果 aa 和 bb 在同一个连通块中，则输出 `Yes`，否则输出 `No`。

对于每个询问指令 `Q2 a`，输出一个整数表示点 aa 所在连通块中点的数量

每个结果占一行。

#### 数据范围

1≤n,m≤1051≤n,m≤105

#### 输入样例：

```
5 5
C 1 2
Q1 1 2
Q2 1
C 2 5
Q2 5
```

#### 输出样例：

```
Yes
2
3
```



对于两个集合的合并，要先更新size再进行根结点更新，不然根节点更新后由于其中一个树的根结点发生了改变，导致结果错误

```java
import java.util.*;
import java.io.*;

class Main {
    
    static int N = 100010;
    static int[] p = new int[N];
    static int[] cnt = new int[N];
    
    static int find(int x) {
        if (x != p[x]) p[x] = find(p[x]);
        return p[x];
    }
    
    public static void main(String[] args) throws Exception {
        BufferedReader in = new BufferedReader(new InputStreamReader(System.in));
        BufferedWriter out = new BufferedWriter(new OutputStreamWriter(System.out));
        
        String[] tmp = in.readLine().split(" ");
        int n = Integer.parseInt(tmp[0]);
        int m = Integer.parseInt(tmp[1]);
        
        for (int i = 1; i <= n; i++) {
            p[i] = i;
            cnt[i] = 1;
        }
        
        while (m-- > 0) {
            tmp = in.readLine().split(" ");
            int a = Integer.parseInt(tmp[1]);
            // out.write(a+","+"b");
            if (tmp[0].equals("C")) {
                int b = Integer.parseInt(tmp[2]);
                if (find(a) != find(b)) {
                    cnt[find(b)] += cnt[find(a)];
                    p[find(a)] = find(b);
                }
            } else if (tmp[0].equals("Q1")) {
                int b = Integer.parseInt(tmp[2]);
                if (find(a) == find(b)) out.write("Yes");
                else out.write("No");
                out.write("\n");
            } else if (tmp[0].equals("Q2")) {
                out.write(cnt[find(a)]+"");
                out.write("\n");
            }
        }
        out.flush();
    }
}
```

