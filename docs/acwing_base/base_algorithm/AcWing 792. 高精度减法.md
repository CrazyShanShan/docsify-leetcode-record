# 792. 高精度减法

URL： https://www.acwing.com/activity/content/punch_the_clock/11/

给定两个正整数，计算它们的差，计算结果可能为负数。

#### 输入格式

共两行，每行包含一个整数。

#### 输出格式

共一行，包含所求的差。

#### 数据范围

1≤整数长度≤105

#### 输入样例：

```
32
11
```

#### 输出样例：

```
21
```



```java
import java.util.*;
import java.io.*;

class Main {
    
    public static boolean compare(List<Integer> A, List<Integer> B) {
        if (A.size() != B.size()) return A.size() > B.size();
        
        for (int i = A.size() - 1; i >= 0; i--) {
            if (A.get(i) != B.get(i)) return A.get(i) > B.get(i);
        }
        
        return true;
    }
    
    public static List<Integer> sub(List<Integer> A, List<Integer> B) {
        List<Integer> res = new ArrayList<>();
        for (int i = 0, t = 0; i < A.size(); i++ ) {
            t = A.get(i) - t;
            if (i < B.size()) t -= B.get(i);
            res.add((t + 10) % 10);
            if (t < 0) t = 1;
            else t = 0;
        }
        
        // for (int i = res.size() - 1; i >= 0; i--) {
        //     if (res.get(i) == 0) res.remove(i);
        //     else break;
        // }
        
        int i = res.size() -1;
        while (i > 0 && res.get(i) == 0) res.remove(i--);
        
        
        return res;
    }
    
    public static void main(String[] args) throws Exception {
        BufferedReader in = new BufferedReader(new InputStreamReader(System.in));
        BufferedWriter out = new BufferedWriter(new OutputStreamWriter(System.out));
       
        String a = in.readLine();
        String b = in.readLine();
        
        List<Integer> A = new ArrayList<>();
        List<Integer> B = new ArrayList<>();
        
        for (int i = a.length() - 1; i >= 0; i--) A.add(a.charAt(i) - '0');
        for (int i = b.length() - 1; i >= 0; i--) B.add(b.charAt(i) - '0');
        
        List<Integer> C = new ArrayList<>();
        
        if (compare(A, B)) {
            C = sub(A, B);
        } else { 
            C = sub(B, A);
            out.write("-");
        }

        for (int i = C.size() -1; i >= 0; i--) {
            out.write(""+C.get(i));
        }
        // if (C.size() == 0) out.write("0");
        out.flush();
        in.close();
        out.close();
    }
    
}
```

