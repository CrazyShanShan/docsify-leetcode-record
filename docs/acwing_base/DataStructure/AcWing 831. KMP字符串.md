## 831. KMP字符串

```java
1. 暴力算法怎么做
2. 如何去优化
S[N]: 长串
P[M]: 短串 pattern。
最少往后移动多少使得，前缀和后缀相等，这样就可以再比较下一段。
相等值越大，往后越少。
因此，以某个点为终点的后缀，后缀和前缀相等，求相等的前缀和后缀的最大值
next[i]: 以i为终点的后缀，与以1为开始的前缀相等的最大值
next[i] = j :  p[1:j] = p[ **i - j + 1** , i] (从1开始的前缀，和以i为终点的后缀)
运用： 对于原串： 到i - 1都是匹配的，从i开始不匹配
			对于模板穿： 到j都是匹配的，从j + 1开始不匹配
			s[i] != p[j + 1] -> 求移动完后的下标，其实就是next[j],令j = next[j],在去看j + 1和s[i]是否相等，如果不相等则递归去做，否则这个就匹配成功了。
char[] s = new int[m];
char[] p = new int[n];
char[] ne = new int[n];

// kmp 求next 过程	
// 同样也是 匹配到了p[:i-1]， p[:j]
// 和追妹子一样： 尝试一次失败了，就退一步再尝试，一定会有成功的一天， 如果成功了就往后走一步
ne[ne[ne[ne[j]]]]
ne[1] = 0; // 第一个失败了，那么就从0开始匹配。
for (int i = 2, j = 0; i <= n; i++) {
  while (j != 0 && p[i] != p[j + 1]) j = ne[j];
  if (p[i] == p[j + 1]) j++;
  ne[i] = j;
}


//kmp 匹配过程
for (int i = 1, j = 0; i <= m; i++) {
  // j == 0 退无可退， j = ne[j]，前缀和后缀相等
  while (j != 0 && s[i] != p[j + 1]) j = ne[j];
  if (s[i] == p[j + 1]) j++;
  if (j == n) {
    //	匹配成功, 启始位置
    print("%d", i - n + 1);
    // 到i已经匹配成功了，j已经不能再往后走了，下一次最少往后移动多少呢？还是最大后缀和前缀相等
    j = ne[j]; //再退一步～
  }
}
```

**code:**

```java
import java.util.*;
import java.io.*;

class Main {
    public static void main(String[] args) throws Exception {
        BufferedReader in = new BufferedReader(new InputStreamReader(System.in));
        BufferedWriter out = new BufferedWriter(new OutputStreamWriter(System.out));
        int n = Integer.parseInt(in.readLine());
        char[] p = new char[n + 1];
        char[] tmp = in.readLine().toCharArray();
        // 使得下表从1开始
        System.arraycopy(tmp, 0, p, 1, n);
        int m = Integer.parseInt(in.readLine());
        tmp = in.readLine().toCharArray();
        char[] s = new char[m + 1];
        // 使得下标从1开始
        System.arraycopy(tmp, 0, s, 1, m);
        // 1. 求next数组
        int[] ne = new int[n + 1];
        for (int i = 2, j = 0; i <= n; i++) {
            while (j != 0 && p[i] != p[j + 1]) j = ne[j];
            if (p[i] == p[j + 1]) j++;
            ne[i] = j;
        }
        // 2. kmp
        for (int i = 1, j = 0; i <= m; i++) {
            while (j != 0 && s[i] != p[j + 1]) j = ne[j];
            if (s[i] == p[j + 1]) j++;
            if (j == n) {
                out.write(i - n + " ");
                j = ne[j];
            }
        }
        out.flush();
        
    }
}
```

