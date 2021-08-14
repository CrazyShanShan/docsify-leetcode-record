# 数组模拟栈

1. 定义： int[] stk ,tt。

2. 插入： stk[++tt] = x;

3. 弹出 tt--;

4. 判断栈是否为空： 

   if (tt > 0) not empty else empty

5. 栈顶： stk[tt];

# 828. 模拟栈

URL：https://www.acwing.com/problem/content/830/

实现一个栈，栈初始为空，支持四种操作：

1. `push x` – 向栈顶插入一个数 xx；
2. `pop` – 从栈顶弹出一个数；
3. `empty` – 判断栈是否为空；
4. `query` – 查询栈顶元素。

现在要对栈进行 MM 个操作，其中的每个操作 33 和操作 44 都要输出相应的结果。

#### 输入格式

第一行包含整数 MM，表示操作次数。

接下来 MM 行，每行包含一个操作命令，操作命令为 `push x`，`pop`，`empty`，`query` 中的一种。

#### 输出格式

对于每个 `empty` 和 `query` 操作都要输出一个查询结果，每个结果占一行。

其中，`empty` 操作的查询结果为 `YES` 或 `NO`，`query` 操作的查询结果为一个整数，表示栈顶元素的值。

#### 数据范围

1≤M≤1000001≤M≤100000,
1≤x≤1091≤x≤109
所有操作保证合法。

#### 输入样例：

```
10
push 5
query
push 6
pop
query
pop
empty
push 4
query
empty
```

#### 输出样例：

```
5
5
YES
4
NO
```



```java
import java.util.*;
import java.io.*;

class Main {
    public static void main(String[] args) throws Exception {
        BufferedReader in = new BufferedReader(new InputStreamReader(System.in));
        BufferedWriter out = new BufferedWriter(new OutputStreamWriter(System.out));
        int M = Integer.parseInt(in.readLine());
        String[] tmp = null;
        
        // 栈
        int[] stk = new int[100010]; 
        // 栈顶指针： tt = 0 表示栈为空
        int tt = 0;                
        int a = 0;
        while (M-- > 0) {
            tmp = in.readLine().split(" ");
            switch (tmp[0]) {
                case "push" : 
                    a = Integer.parseInt(tmp[1]);
                    stk[++tt] = a;
                    break;
                case "pop" : tt--; break;
                case "empty" : if (tt > 0) out.write("NO\n"); else out.write("YES\n"); break;
                case "query" : out.write(stk[tt]+"\n"); break;
            }
        }
        out.flush();
    }
}
```

