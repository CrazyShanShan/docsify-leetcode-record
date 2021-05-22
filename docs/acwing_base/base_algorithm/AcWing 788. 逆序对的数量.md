# 788. 逆序对的数量

给定一个长度为 n 的整数数列，请你计算数列中的逆序对的数量。

逆序对的定义如下：对于数列的第 i 个和第 j 个元素，如果满足 i<j 且 a[i]>a[j] ]，则其为一个逆序对；否则不是。

#### 输入格式

第一行包含整数 n，表示数列的长度。

第二行包含 n 个整数，表示整个数列。

#### 输出格式

输出一个整数，表示逆序对的个数。

#### 数据范围

1≤n≤100000

#### 输入样例：

```
6
2 3 4 5 6 1
```

#### 输出样例：

```
5
```



```java
import java.util.*;

class Main {
    
    static int[] tmp = new int[100010];
    
    public static long mergeSort(int[] q, int l, int r) {
        if (l >= r) return 0;
        int mid = l + r >> 1;
        long res = mergeSort(q, l , mid) + mergeSort(q, mid + 1, r);
        int k = 0, i = l, j = mid + 1;
        while (i <= mid && j <= r) {
            if (q[i] <= q[j]) tmp[k++] = q[i++];
            else {
                tmp[k++] = q[j ++];
                res += mid - i + 1;
            }
        }
        while (i <= mid) tmp[k++] = q[i++];
        while (j <= r) tmp[k++] = q[j++];
        for (i = l, j = 0; i <= r; i++, j++) q[i] = tmp[j];
        return res;
    }
    
    public static void main(String[] args) {
        int N = 100010;
        Scanner sc = new Scanner(System.in);
        int n = sc.nextInt();
        int[] q = new int[N];
        for (int i = 0; i < n; i++) {
            q[i] = sc.nextInt();
        }
        System.out.println(mergeSort(q, 0, n - 1));
    }
}
```

