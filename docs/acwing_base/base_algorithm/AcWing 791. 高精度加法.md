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