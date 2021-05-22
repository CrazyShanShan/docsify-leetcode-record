# 803. 区间合并

URL： https://www.acwing.com/problem/content/805/

给定 nn 个区间 [li,ri][li,ri]，要求合并所有有交集的区间。

注意如果在端点处相交，也算有交集。

输出合并完成后的区间个数。

例如：[1,3][1,3] 和 [2,6][2,6] 可以合并为一个区间 [1,6][1,6]。

#### 输入格式

第一行包含整数 nn。

接下来 nn 行，每行包含两个整数 ll 和 rr。

#### 输出格式

共一行，包含一个整数，表示合并区间完成后的区间个数。

#### 数据范围

1≤n≤1000001≤n≤100000,
−109≤li≤ri≤109−109≤li≤ri≤109

#### 输入样例：

```
5
1 2
2 4
5 6
7 8
7 9
```

#### 输出样例：

```
3
```



```java
import java.util.*;

class Main {

    public static List<int[]> merge(List<int[]> segs) {
        List<int[]> res = new LinkedList<>();
        Collections.sort(segs, (o1, o2) -> o1[0] - o2[0]);
        int st = (int)-2e9, ed = (int)-2e9;

        int n = segs.size();
        for (int i = 0; i < n; i++) {
            int[] cur = segs.get(i);
            if (ed < cur[0]) {
                if (st != (int)-2e9) {
                    res.add(new int[]{st, ed});    
                }
                st = cur[0];
                ed = cur[1];
            } else {
                ed = Math.max(cur[1], ed);
            }
        }
        if (st != (int)-2e9) res.add(new int[]{st, ed});
        return res;
    }

    public static void main(String[] agrs) {
        Scanner sc = new Scanner(System.in);
        int n = sc.nextInt();
        List<int[]> segs = new ArrayList<>();
        while (n-- > 0) {
            int[] tmp = new int[2];
            tmp[0] = sc.nextInt();
            tmp[1] = sc.nextInt();
            segs.add(tmp);
        }
       System.out.println(merge(segs).size());
    }
}

```

