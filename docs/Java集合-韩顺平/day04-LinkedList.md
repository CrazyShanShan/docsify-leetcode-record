----

**LInkedList:**

1. LinkedList底层实现了双向 **链表** 和 双端 **队列** 特点
2. 可以添加任意元素，包括null
3. 线程不安全，没有实现同步

---

**LinkedList底层结构**

LinkedList的底层操作机制

1. LinkedList底层维护了一个双向链表
2. LinkedList中维护了两个属性first和last分别指向首节点和尾节点
3. 每个节点(Node对象)， 里面又维护了prev,next,item三个属性，其中prev指向前1个，通过next指向后一个节点。最终实现双向链表
4. LinkedList的元素的添加和删除，不是通过数组完成的，相对来说效率较高

----

源码解读：

比较简单

