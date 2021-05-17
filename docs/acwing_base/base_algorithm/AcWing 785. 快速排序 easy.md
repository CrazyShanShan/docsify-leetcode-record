# 快速排序 - 分治

1. 确定分界点：选择的方法有如下4种
   - 左边界 q[l]
   - 中间值 q[l + r / 2]
   - 右边界 q[r]
   - 随机
2. **调整区间： 第一个区间的数都小于等于x, 第二个区间的数都大于等于x**
3. 递归处理左、右两段



调整区间的实现方法：一个很暴力的做法

1. a[]  b[]
2. 扫描q[l-r] ： q[i] <= x x插入到a[]； q[i] > x  x插入b[]
3. a[] - > q[], b[]->q[]



比较优美的做法：

遍历q[l-r]：while q[i] < 分界点，i++:  while q[j] > 分界点 j--，然后swap 



# 785. 快速排序 easy

url:https://www.acwing.com/problem/content/description/787/

给定你一个长度为 nn 的整数数列。

请你使用快速排序对这个数列按照从小到大进行排序。

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



照着y总的板子打的

```java
import java.util.*;
import java.io.*;

class Main {
    public static void main(String[] args) {
        Scanner sc = new Scanner(new BufferedInputStream(System.in));
        int n = sc.nextInt();
        int[] nums = new int[n];
        for (int i = 0; i < n; i++) {
            nums[i] = sc.nextInt();
        }
        quickSort(nums, 0, n - 1);
        for (int i = 0; i < n; i++) {
            System.out.print(nums[i] + " ");
        }
    }
    public static void quickSort(int[] nums, int l, int r) {
        if (l >= r) return;
        int i = l - 1, j = r + 1, x = nums[l + r >> 1];
        while (i < j) {
            do i++; while (nums[i] < x);
            do j--; while (nums[j] > x);
            if (i < j) {
                int tmp = nums[i];
                nums[i] = nums[j];
                nums[j] = tmp;
            }
        }
        quickSort(nums, l, j);
        quickSort(nums, j + 1, r);
    }
}
```

