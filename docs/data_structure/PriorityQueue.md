# PriorityQueue 学习

> java.lang.Object
>
> ​	java.util.AbstractCollection
>
> ​		java.util.AbstractQueue
>
> ​			java.util.PriorityQueue

**All Implemented Interfaces:**

Serializable Iterable Collection Queue

public class PriorityQueue<E> extends AbstractQueue<E> implements Serializable

基于优先级堆的无限优先级queue。优先级队列的元素根据它们的有序natural ordering,或者由一个Compartor在队列构造的时候提供，这取决于构造方法。**优先级队列不允许null元素**。依靠自然排序的优先级队列也不允许插入不可比较的对象。

该队列的头部是相对于指定顺序的**最小元素**。如果多个元素被绑定到最小值，那么头就是这些元素之一-关系被任意破坏。队列检索操作poll、remove、peek、element访问在队列的头部的元件。

优先级队列是无限制的。但是具有管理用于在队列上存储元素的数组的大小的内部容量。它始终至少与队列大小一样大。当元素被添加到优先级队列中，其容量会自动增长，没有规定增长政策的细节。

该类及其迭代器实现Collection和Iterator接口的所有可选方法。方法iterator（）中提供的迭代器不能保证任何特定顺序遍历优先队列的元素。如果需要有序遍历，请考虑使用Arrays.sort(pq.toArray())。

请注意，**此实现不同步**。如果需要线程安全，请使用**PriorityBlockingQueue类**。

实现注意事项：提供了O（n)的时间入队和出队方法（offer、poll、remove和add）。remove和contains方法的线性时间和恒定时间检索方法(peek,elemtns和size)。



 **构造方法**

| Constructor and Description                                  |
| :----------------------------------------------------------- |
| `PriorityQueue()`创建一个`PriorityQueue` ，具有默认的初始容量（11），根据它们的[natural ordering](chm://f9eb741e5918db63e053c1445465e3ce/java/lang/Comparable.html)对其元素进行[排序](chm://f9eb741e5918db63e053c1445465e3ce/java/lang/Comparable.html) 。 |
| `PriorityQueue(Collection<? extends E> c)`创建一个 `PriorityQueue`集合中的元素的PriorityQueue。 |
| `PriorityQueue(Comparator<? super E> comparator)`创建具有默认初始容量的 `PriorityQueue` ，并根据指定的比较器对其元素进行排序。 |
| `PriorityQueue(int initialCapacity)`创建`PriorityQueue`与根据它们的排序其元素指定的初始容量[natural ordering](chm://f9eb741e5918db63e053c1445465e3ce/java/lang/Comparable.html) 。 |
| `PriorityQueue(int initialCapacity, Comparator<? super E> comparator)`创建具有 `PriorityQueue`初始容量的PriorityQueue，根据指定的比较器对其元素进行排序。 |
| `PriorityQueue(PriorityQueue<? extends E> c)`创建包含 `PriorityQueue`优先级队列中的元素的PriorityQueue。 |
| `PriorityQueue(SortedSet<? extends E> c)`创建一个 `PriorityQueue`指定排序集中的元素的PriorityQueue。 |

Methods:

| Modifier and Type       | Method and Description                                       |
| :---------------------- | :----------------------------------------------------------- |
| `boolean`               | `add(E e)`将指定的元素插入到此优先级队列中。                 |
| `void`                  | `clear()`从此优先级队列中删除所有元素。                      |
| `Comparator<? super E>` | `comparator()`返回用于为了在这个队列中的元素，或比较`null`如果此队列根据所述排序[natural ordering](chm://f9eb741e5918db63e053c1445465e3ce/java/lang/Comparable.html)的元素。 |
| `boolean`               | `contains(Object o)`如果此队列包含指定的元素，则返回 `true` 。 |
| `Iterator<E>`           | `iterator()`返回此队列中的元素的迭代器。                     |
| `boolean`               | `offer(E e)`将指定的元素插入到此优先级队列中。               |
| `E`                     | `peek()`检索但不删除此队列的头，如果此队列为空，则返回 `null` 。 |
| `E`                     | `poll()`检索并删除此队列的头，如果此队列为空，则返回 `null` 。 |
| `boolean`               | `remove(Object o)`从该队列中删除指定元素的单个实例（如果存在）。 |
| `int`                   | `size()`返回此集合中的元素数。                               |
| `Spliterator<E>`        | `spliterator()`在此队列中的元素上创建*[late-binding](chm://f9eb741e5918db63e053c1445465e3ce/java/util/Spliterator.html#binding)*和*失败快速*[`Spliterator`](chm://f9eb741e5918db63e053c1445465e3ce/java/util/Spliterator.html) 。 |
| `Object[]`              | `toArray()`返回一个包含此队列中所有元素的数组。              |
| `<T> T[]`               | `toArray(T[] a)`返回一个包含此队列中所有元素的数组; 返回的数组的运行时类型是指定数组的运行时类型。 |



// 变大根堆

```java
PriorityQueue<Integer> pq = new riorityQueue<Integer>(
	new Comparator<Integer>() {
		public int compare(Integer num1, Integer num2) {
			return num2 - num1;
		}
	}
);
```

