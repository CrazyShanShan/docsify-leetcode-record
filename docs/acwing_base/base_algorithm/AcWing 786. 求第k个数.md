# 786. 第k个数 easy

给定一个长度为 nn 的整数数列，以及一个整数 kk，请用快速选择算法求出数列从小到大排序后的第 kk 个数。

#### 输入格式

第一行包含两个整数 n 和 k。

第二行包含 n 个整数（所有整数均在 1∼109范围内），表示整数数列。

#### 输出格式

输出一个整数，表示数列的第 k 小数。

#### 数据范围

1≤n≤100000
1≤k≤n

#### 输入样例：

```
5 3
2 4 1 5 3
```

#### 输出样例：

```
3
```



```java
import java.util.*;
import java.io.*;

class Main {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        int n = sc.nextInt();
        int k = sc.nextInt();
        int[] nums = new int[n];
        for (int i = 0; i < n; i++) {
            nums[i] = sc.nextInt();
        }
        int res = quickSort(nums, 0, n - 1, k);
        System.out.println(res);
    }
    public static int quickSort(int[] nums, int l, int r, int k) {
        if (l == r) return nums[l];
        int i = l - 1, j = r + 1, x = nums[l + r >> 1];
        while (i < j) {
            while ( nums[++i] < x);
            while ( nums[--j] > x);
            if (i < j) {
                int tmp = nums[i];
                nums[i] = nums[j];
                nums[j] = tmp;
            }    
        }
        int len = j - l + 1;
        if (k <= len) return quickSort(nums, l, j, k);
        return quickSort(nums, j + 1, r, k - len);
        
    }
}
```

