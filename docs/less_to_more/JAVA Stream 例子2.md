## 计算数组中元素的最大值、最小值、平均值、和

```java

import java.util.Arrays;
import java.util.stream.IntStream;
int [] intArr = new int[]{9,8,4};
IntStream is = Arrays.stream(intArr);
int sum = is.sum();
is =Arrays.stream(intArr);
int max = is.max().getAsInt();
is =Arrays.stream(intArr);
int min = is.min().getAsInt();
is =Arrays.stream(intArr);
double avg = is.average().getAsDouble();

System.out.println("最大值："+max+"小："+min+"和："+sum+"平均："+avg);
```

