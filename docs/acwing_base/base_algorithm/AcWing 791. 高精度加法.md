# 791. 高精度加法

给定两个正整数，计算它们的和。

#### 输入格式

共两行，每行包含一个整数。

#### 输出格式

共一行，包含所求的和。

#### 数据范围

1≤整数长度≤1000001≤整数长度≤100000

#### 输入样例：

```
12
23
```

#### 输出样例：

```
35
```



```java
import java.util.*;
import java.io.*;

class Main {

    public static List<Integer> add(List<Integer> A, List<Integer> B) {
        List<Integer> res = new ArrayList<>();
        int t = 0;
        for (int i = 0; i < A.size() || i < B.size(); i++) {
            if (i < A.size()) t += A.get(i);
            if (i < B.size()) t += B.get(i);
            res.add(t % 10);
            t /= 10;
        }
        // 如果还有进位，需要加入答案
        if (t > 0) res.add(1);
        return res;
    }

    public static void main(String[] args) throws Exception {
        BufferedReader in = new BufferedReader(new InputStreamReader(System.in));
        String a = in.readLine();
        String b = in.readLine();
        List<Integer> A = new ArrayList<>();
        List<Integer> B = new ArrayList<>();

        for (int i = a.length() - 1; i >= 0; i--) A.add(a.charAt(i) - '0');
        for (int i = b.length() - 1; i >= 0; i--) B.add(b.charAt(i) - '0');

        List<Integer> list = add(A, B);

        for (int i = list.size() - 1; i >= 0; i-- ) System.out.print(list.get(i));
    }
}

作者：CrazyShanShan
链接：https://www.acwing.com/activity/content/code/content/1255975/
来源：AcWing
著作权归作者所有。商业转载请联系作者获得授权，非商业转载请注明出处。
```





``` java
import java.util.*;
import java.io.*;
import java.math.*;


class Main {
    public static void main(String[] args) throws Exception{
        BufferedReader in = new BufferedReader(new InputStreamReader(System.in));
        BigInteger a = new BigInteger(in.readLine());
        BigInteger b = new BigInteger(in.readLine());
        System.out.println(a.add(b));
        in.close();
    }
}
```

