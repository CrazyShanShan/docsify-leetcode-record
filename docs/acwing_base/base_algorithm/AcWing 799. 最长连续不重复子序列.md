# 799. 最长连续不重复子序列

URL： https://www.acwing.com/problem/content/801/

给定一个长度为 nn 的整数序列，请找出最长的不包含重复的数的连续区间，输出它的长度。

#### 输入格式

第一行包含整数 nn。

第二行包含 nn 个整数（均在 0∼1050∼105 范围内），表示整数序列。

#### 输出格式

共一行，包含一个整数，表示最长的不包含重复的数的连续区间的长度。

#### 数据范围

1≤n≤1051≤n≤105

#### 输入样例：

```
5
1 2 2 3 5
```

#### 输出样例：

```
3
```



```java
import java.util.*;

class Main {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        int n = sc.nextInt();
        int[] q = new int[n];
        for (int i = 0; i < n; i++) q[i] = sc.nextInt();
        int N = 100010;
        int[] s = new int[N];
        int res = 0;
        for (int i = 0, j = 0; i < n; i++) {
            s[q[i]]++;
            while (s[q[i]] > 1) {
                s[q[j]]--;
                j++;
            }
            res = Math.max(res, i - j + 1);
        }
        System.out.println(res);
    }
}

作者：CrazyShanShan
链接：https://www.acwing.com/solution/content/50314/
来源：AcWing
著作权归作者所有。商业转载请联系作者获得授权，非商业转载请注明出处。
```

