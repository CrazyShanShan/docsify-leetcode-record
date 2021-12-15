----

​						底层结构		增删的效率		改3查的效率

ArrayList: 		可变数组		较低、数组扩容		较高

LinkedList	双向链表		较高、通过链表追加	较低

如何选择ArrayList和LinkedList:

1. 如果改查的操作多，选择arrayList
2. 如果增删的操作多，选择LinkedList
3. 一般来说，在程序中，80%的都是查询，大部分情况下会选择Arraylist
4. 在一个项目中，可以根据业务灵活选择，可能某些模块使用ArrayList，另外一个模块中使用De shi LinkedLIs t，也就是说，要根据业务来选择。

