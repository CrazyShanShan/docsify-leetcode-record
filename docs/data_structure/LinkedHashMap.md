# LinkedHashMap

**首先介绍一下Map.Entry<K, V>**

public static interface Map.Entry<K, V>

地图条目（键值对）。Map.entrySet方法返回地图的集合视图，其元素属于此类。获取对应条目的引用的 **唯一**方法是从该集合视图的迭代器。这些Map.Entry 对象仅在迭代期间有效。

| Modifier and Type                                            | Method and Description                                       |
| :----------------------------------------------------------- | :----------------------------------------------------------- |
| `static <K extends Comparable<? super K>,V>Comparator<Map.Entry<K,V>>` | `comparingByKey()`返回一个比较[器](chm://f9eb741e5918db63e053c1445465e3ce/java/util/Map.Entry.html) ，按键自然顺序比较[`Map.Entry`](chm://f9eb741e5918db63e053c1445465e3ce/java/util/Map.Entry.html) 。 |
| `static <K,V> Comparator<Map.Entry<K,V>>`                    | `comparingByKey(Comparator<? super K> cmp)`返回一个比较器，比较[`Map.Entry`](chm://f9eb741e5918db63e053c1445465e3ce/java/util/Map.Entry.html)按键使用给定的[`Comparator`](chm://f9eb741e5918db63e053c1445465e3ce/java/util/Comparator.html) 。 |
| `static <K,V extends Comparable<? super V>>Comparator<Map.Entry<K,V>>` | `comparingByValue()`返回一个比较器，比较[`Map.Entry`](chm://f9eb741e5918db63e053c1445465e3ce/java/util/Map.Entry.html)的自然顺序值。 |
| `static <K,V> Comparator<Map.Entry<K,V>>`                    | `comparingByValue(Comparator<? super V> cmp)`返回一个比较[器](chm://f9eb741e5918db63e053c1445465e3ce/java/util/Map.Entry.html) ，使用给定的[`Comparator`](chm://f9eb741e5918db63e053c1445465e3ce/java/util/Comparator.html)比较[`Map.Entry`](chm://f9eb741e5918db63e053c1445465e3ce/java/util/Map.Entry.html)的值。 |
| `boolean`                                                    | `equals(Object o)`将指定的对象与此条目进行比较以获得相等性。 |
| `K`                                                          | `getKey()`返回与此条目相对应的键。                           |
| `V`                                                          | `getValue()`返回与此条目相对应的值。                         |
| `int`                                                        | `hashCode()`返回此映射条目的哈希码值。                       |
| `V`                                                          | `setValue(V value)`                                          |



## Class LinkedHashMap<K,V>

Class LinkedHashMap<K,V>

java.lang.Object

- java.util.AbstractMap<K,V>
  - java.util.HashMap<K,V>

		      - java.util.LinkedHashMap<K,V>
参数类型
K - 由该地图维护的键的类型
V - 映射值的类型

**参数类型**

`K` - 由该地图维护的键的类型 

`V` - 映射值的类型

哈希表和链表实现的Map接口，具有可预测的迭代次序。这种实现不同于HashMap，它维持于所有条目的运行双向链表。此链接列表定义迭代排序，通常是将键插入到地图中的顺序。请注意，如果将键重新插入到地图中，则插入顺序不受影响。

里面的负载因子为有点看不懂，这里就不抄录了～

