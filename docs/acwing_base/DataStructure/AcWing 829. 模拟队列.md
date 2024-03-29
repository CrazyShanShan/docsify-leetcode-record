#  829. 模拟队列

URL：https://www.acwing.com/problem/content/831/

实现一个队列，队列初始为空，支持四种操作：

1. `push x` – 向队尾插入一个数 xx；
2. `pop` – 从队头弹出一个数；
3. `empty` – 判断队列是否为空；
4. `query` – 查询队头元素。

现在要对队列进行 MM 个操作，其中的每个操作 33 和操作 44 都要输出相应的结果。

#### 输入格式

第一行包含整数 MM，表示操作次数。

接下来 MM 行，每行包含一个操作命令，操作命令为 `push x`，`pop`，`empty`，`query` 中的一种。

#### 输出格式

对于每个 `empty` 和 `query` 操作都要输出一个查询结果，每个结果占一行。

其中，`empty` 操作的查询结果为 `YES` 或 `NO`，`query` 操作的查询结果为一个整数，表示队头元素的值。

#### 数据范围

1≤M≤1000001≤M≤100000,
1≤x≤1091≤x≤109,
所有操作保证合法。

#### 输入样例：

```
10
push 6
empty
query
pop
empty
push 3
push 4
pop
query
push 6
```

#### 输出样例：

```
NO
6
YES
4
```



```java
import java.util.*;
import java.io.*;

class Main {
    public static void main(String[] args) throws Exception {
        BufferedReader in = new BufferedReader(new InputStreamReader(System.in));
        BufferedWriter out = new BufferedWriter(new OutputStreamWriter(System.out));
        
        int[] q = new int[100010];
        int tt = -1 , hh = 0;
        
        int M = Integer.parseInt(in.readLine());
        String[] tmp = null;
        while (M-- > 0) {
            tmp = in.readLine().split(" ");
            switch (tmp[0]) {
                case "push" : 
                    int a = Integer.parseInt(tmp[1]);
                    q[++tt] = a;
                    break;
                case "pop" : hh++;  break;
                case "empty" : if (hh <= tt) out.write("NO\n"); else out.write("YES\n");  break;  
                case "query" : out.write(q[hh]+"\n"); break;
            }
        }
        out.flush();
        
    }
}
```

