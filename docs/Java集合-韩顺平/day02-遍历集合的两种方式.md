-----

Collection接口和常用方法：

- Collection接口遍历元素方式1 - 使用Iterator(迭代器)

- 基本介绍
  - Iterator对象成为迭代器，主要用于遍历Collection集合中的元素。
  - 所有实现了Collection接口的集合类都有一个iterator()方法，用以返回一个实现了Iterator接口的对象，即可以返回一个迭代器。
  - Ierator的结构
  - Iterator仅用于遍历集合，Iterator本身并不存放对象

执行原理： 

```
Iterator it = col .iterator(); # 得到迭代器对象
# hasNext()： 判断是否还有下一个元素
while (it.hasNext()) {
	//next() 1. 下移， 返回下移以后集合位置上的元素
}
```

Itertor接口中的方法：

- boolean hasNext() : Returns true if the iteration has more elements
- T next(): returns the next element in the iteration
- void remove(): removes from the underlying collection the last element returned by the iterator

----

遍历元素方式2 - 使用增强for循环

// 1. 使用增强for,在Collection集合

// 2. 底层也是使用iterator()

//3 . 增强for可以理解成简化版本的迭代器

```
for (Object book: col) {

}
```

