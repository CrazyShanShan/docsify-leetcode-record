# 离散化

值域比较大0～10^9， 个数10^5。

a[] : 1， 3 ， 100， 2000， 50000， 500000

需要把这个序列映射到从0开始的连续的自然数

映射到 i : 0 ， 1， 2， 3， 4

这个过程称为离散化

1. **目的：排序➕去重** a[]中可能重复元素 去重（erase，将重复元素去重，并且返回去重之后的尾端点）
2. 如何算出x离散化后的值 二分



# 802. 区间和

URL： https://www.acwing.com/activity/content/problem/content/836/1/

假定有一个无限长的数轴，数轴上每个坐标上的数都是 00。

现在，我们首先进行 nn 次操作，每次操作将某一位置 xx 上的数加 cc。

接下来，进行 mm 次询问，每个询问包含两个整数 ll 和 rr，你需要求出在区间 [l,r][l,r] 之间的所有数的和。

#### 输入格式

第一行包含两个整数 nn 和 mm。

接下来 nn 行，每行包含两个整数 xx 和 cc。

再接下来 mm 行，每行包含两个整数 ll 和 rr。

#### 输出格式

共 mm 行，每行输出一个询问中所求的区间内数字和。

#### 数据范围

−10^9≤x≤10^9
1≤n,m≤10^5
−10^9≤l≤r≤10^9
−10000≤c≤10000

---



```java
import java.util.*;
import java.io.*;
class Main {
    
            // 存储 将要离散化的数据
    static List<Integer> alls = new ArrayList<>();
    
    public static int find(int x) {
        int l = 0, r = alls.size() - 1;
        while (l < r) {
            int mid = l + r >> 1;
            if (alls.get(mid) >= x) r = mid;
            else l = mid + 1;
        }
        return r + 1;
    }
    
    public static int unique(List<Integer> list) {
        // 将list中排好序的元素，进行去重，最后返回长度，用于remove
        int j = 0;
        for (int i = 0; i < list.size(); i++) {
            if (i == 0 || list.get(i) != list.get(i - 1)) list.set(j++, list.get(i));
        }
        return j;
    }
    
    public static void main(String[] args) {
        Scanner sc = new Scanner(new InputStreamReader(System.in));
        int n = sc.nextInt();
        int m = sc.nextInt();
        

        // 存储 用于add的数据
        List<int[]> addc = new ArrayList<>();
        // 存储 用于查询的数据
        List<int[]> query = new ArrayList<>();
        
        for (int i = 0; i < n; i++) {
            int x = sc.nextInt();
            int c = sc.nextInt();
            addc.add(new int[]{x , c});
            alls.add(x);
        }
        
        for (int i = 0; i < m; i++) {
            int l = sc.nextInt();
            int r = sc.nextInt();
            query.add(new int[]{l, r});
            alls.add(l);
            alls.add(r);
        }
        
        // 排序
        Collections.sort(alls);
        // 去重
        int tmp = unique(alls);
        alls.subList(tmp, alls.size()).clear();
        
        int N = alls.size() + 1;
        int[] a = new int[N];
        int[] s = new int[N];
        
        // 处理插入
        for (int[] item: addc) {
            int x = find(item[0]);
            a[x] += item[1];
        }
        
        // 预处理前缀和
        for (int i = 1; i <= alls.size(); i++) s[i] = s[i - 1] + a[i];

        // 处理询问
        for (int[] item: query) {
            int l = find(item[0]), r = find(item[1]);
            System.out.println(s[r] - s[l - 1]);
        }
        
    }
}
```



