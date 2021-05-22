**整数二分：** 其本质并不是单调性

找到一个性质，可以将整个区间一分为2。

1. mid = (l + r ) / 2;
2. if (check(mid)) :
   1. true： [mid , r]

# 789. 数的范围

URL：https://www.acwing.com/problem/content/791/

给定一个按照升序排列的长度为 nn 的整数数组，以及 qq 个查询。

对于每个查询，返回一个元素 kk 的起始位置和终止位置（位置从 00 开始计数）。

如果数组中不存在该元素，则返回 `-1 -1`。

#### 输入格式

第一行包含整数 nn 和 qq，表示数组长度和询问个数。

第二行包含 nn 个整数（均在 1∼100001∼10000 范围内），表示完整数组。

接下来 qq 行，每行包含一个整数 kk，表示一个询问元素。

#### 输出格式

共 qq 行，每行包含两个整数，表示所求元素的起始位置和终止位置。

如果数组中不存在该元素，则返回 `-1 -1`。

#### 数据范围

1≤n≤1000001≤n≤100000
1≤q≤100001≤q≤10000
1≤k≤100001≤k≤10000

#### 输入样例：

```
6 3
1 2 2 3 3 4
3
4
5
```

#### 输出样例：

```
3 4
5 5
-1 -1
```

left -> right

```java
import java.util.*;

class Main {
    
    public static void binarySearch(int[] q, int k) {
        int l = 0, r = q.length - 1;
        // 搜索左边 nums[l] >= k
        while (l < r) {
            int mid = l + r >> 1;
            if (q[mid] >= k) r = mid;
            else l = mid + 1;
        }
        if (q[l] != k) System.out.print("-1 -1");
        else {
            System.out.print(l+" ");
            r = q.length - 1;
            while (l < r) {
                int mid = l + r + 1 >> 1;
                if (q[mid] <= k) l = mid;
                else r = mid - 1;
            }
            System.out.print(r);
        }
   
    }
    
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        int n = sc.nextInt();
        int m = sc.nextInt();
        int[] q = new int[n];
        for (int i = 0; i < n; i++) q[i] = sc.nextInt();
        while (m-- > 0) {
            int k = sc.nextInt();
            binarySearch(q, k);
            System.out.println();
        }
    }
}
```

right - > left

```java
import java.util.*;
import java.io.*;

class Main {
    
    public static String help(int[] q, int k) {
        int l = 0, r = q.length - 1;
        while (l < r) {
            int mid = l + r >> 1;
            if (q[mid] <= k) {
                r = mid;
            } else {
                l = mid + 1;
            }
        }
        System.out.println(l +"," + r);
        if (q[r] != k) return "-1 -1";
        else {
            while (r < q.length && q[r] == k) r++;
            return l + " " + r;
        }
    }
        
    
    public static void main(String[] args) {
        Scanner sc = new Scanner(new BufferedInputStream(System.in));
        int n = sc.nextInt();
        int q = sc.nextInt();
        System.out.println(n + "," + q);
        int[] nums = new int[n];
        for (int i = 0; i < n; i++) nums[i] = sc.nextInt();
        for (int i = 0; i < q; i++) {
            System.out.println(help(nums, sc.nextInt()));
        }
    }
}
```

