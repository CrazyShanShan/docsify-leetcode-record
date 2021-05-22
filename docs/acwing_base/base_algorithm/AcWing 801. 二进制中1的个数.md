n 的二进制表示中第k位是几？

1. 先把第k位移到最后一位	n >> k
2. 看个位是几      x & 1

n >> k & 1

lowbit(x) :  返回x的最后一位 1

1010 lowbit(x) = 10

101000 lowbit(x) = 1000

```
x & - x = x & (-x + 1)

x = 1010 ...  100... 0 
-x = 0101...  01111111
- x + 1 = 0101... 100... 0 
x & (- x) = 000...   100... 000
```



# 801. 二进制中1的个数

URL：https://www.acwing.com/problem/content/803/

给定一个长度为 nn 的数列，请你求出数列中每个数的二进制表示中 11 的个数。

#### 输入格式

第一行包含整数 nn。

第二行包含 nn 个整数，表示整个数列。

#### 输出格式

共一行，包含 nn 个整数，其中的第 ii 个数表示数列中的第 ii 个数的二进制表示中 11 的个数。

#### 数据范围

1≤n≤1000001≤n≤100000,
0≤数列中元素的值≤1090≤数列中元素的值≤109

#### 输入样例：

```
5
1 2 3 4 5
```

#### 输出样例：

```
1 1 2 1 2
```



```java
import java.util.*;

class Main {
    
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        int n = sc.nextInt();
        for (int i = 0; i < n; i++) {
            int k = sc.nextInt();    
            int tmp = 0;
            while (k != 0) {
                k = k & (k - 1);
                tmp++;
            }
            System.out.print(tmp + " ");
        }
    }
}
```

 