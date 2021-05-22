# 归并排序-分治

1. 确定分界点 mid = (l + r) >> 1;
2. 递归排序left ,right
3. **归并 - 合二唯一**



# 787. 归并排序

URL： https://www.acwing.com/activity/content/punch_the_clock/11/

给定你一个长度为 nn 的整数数列。

请你使用归并排序对这个数列按照从小到大进行排序。

并将排好序的数列按顺序输出。

#### 输入格式

输入共两行，第一行包含整数 nn。

第二行包含 nn 个整数（所有整数均在 1∼1091∼109 范围内），表示整个数列。

#### 输出格式

输出共一行，包含 nn 个整数，表示排好序的数列。

#### 数据范围

1≤n≤1000001≤n≤100000

#### 输入样例：

```
5
3 1 2 4 5
```

#### 输出样例：

```
1 2 3 4 5
```



```java
import java.util.*;

class Main {
    
    static final int N = 100010;
    static int[] tmp = new int[N];
    
    public static void mergeSort(int[] q, int l , int r) {
        if (l >= r) return;
        int mid = l + r >> 1;
        mergeSort(q, l, mid);
        mergeSort(q, mid + 1, r);
        
        int k = 0, i = l, j = mid + 1;
        while (i <= mid && j <= r) {
            if (q[i] <= q[j]) tmp[k ++] = q[i++];
            else tmp[k ++] = q[j ++];
        }
        while (i <= mid) tmp[k ++] = q[i ++];
        while (j <= r) tmp[k ++] = q[j ++];
        for (i = l, j = 0; i <= r; i++, j++) q[i] = tmp[j];
    }
    
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        int n = sc.nextInt();
        int[] q = new int[n];
        for (int i = 0; i < n; i++) q[i] = sc.nextInt();
        mergeSort(q, 0, n - 1);
        for (int i = 0; i < n; i++) System.out.print(q[i] + " ");
    }
}
```

