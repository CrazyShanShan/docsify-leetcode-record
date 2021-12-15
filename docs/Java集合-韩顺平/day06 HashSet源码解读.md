----

HashSet的源码解读：

1. 执行 map = new HashMap<>();

2. 执行add, map.put(e, PREESENT) == null

   ```
   static final Object  PRESENT = new Object()
   return map.put(e, PRESENT) == null
   ```

   

3. 执行put(K key, V value) , 该方法会执行hash(key)，得到key对应的hash值， 避免hash碰撞, 这个值不是hashCode

   ```
   return putVal(hash(key), key ,value, false, true)
   ```

   hash(key)

   ```
   stastic final int hash(Object key) {
   	int h;
   	return (key == null) ? 0 : (h = key.hashCode()) ^ (h >>> 16) // 无符号右移16位
   }
   ```

4. 执行 final V putVal(int hash, K key, V value, boolean onlyIfAbsent, boolean evict) 

   ```java
   
       /**
        * Implements Map.put and related methods.
        *
        * @param hash hash for key
        * @param key the key
        * @param value the value to put
        * @param onlyIfAbsent if true, don't change existing value
        * @param evict if false, the table is in creation mode.
        * @return previous value, or null if none
        */
       final V putVal(int hash, K key, V value, boolean onlyIfAbsent,
                      boolean evict) {
         	// 定义了辅助变量
           Node<K,V>[] tab; Node<K,V> p; int n, i;
           // table 就是HashMap的一个数组，类型就是一个Node<K, V>[]
           if ((tab = table) == null || (n = tab.length) == 0)
   						// 执行到这里的时候，要么这个table没有被创建，要么table中没有元素
             	// 第一次扩容，到16个空间
             	n = (tab = resize()).length;
         	
           // 1. 根据传入的key，得到的hash值，计算该key应该存放到table表的哪个索引位置
         	// 并把这个位置的对象，赋给辅助变量p，
         	// 2. 判定p是否为null 
         	// 2.1 如果p为null，表示还没有存放过元素， 就创建一个Node(hash, Key,Value, next)
           if ((p = tab[i = (n - 1) & hash]) == null)
               tab[i] = newNode(hash, key, value, null);
           else {
             	// 开发提示： 在需要局部变量的时候进行创建
               Node<K,V> e; K k;
             	
             	 // p = table[i]
   						 // case1: 如果当前索引位置对应的链表的第一个元素和准备添加的key的hash值一样
             	 // 并且满足下面两个条件之一： 
             	 //	（1）准备加入的 key和 p指向的Node结点的key 是同一个对象
             	 // （2）或者p指向的Node节点的key的equals()和准备加入的key比较后相同
             	 // 就不能加入
               if (p.hash == hash && 
                   ((k = p.key) == key || (key != null && key.equals(k))))
                   e = p;
               // 再判断： p是不是一颗红黑树
             	// case2: 如果是一颗红黑树，就调用另外的方法进行添加
               else if (p instanceof TreeNode)
                   e = ((TreeNode<K,V>)p).putTreeVal(this, tab, hash, key, value);
               else {
                 	// case3: 如果table对应索引位置，已经是一个链表，就使用for循环比较
                 	// 1. 依次和该链表的每一个元素比较后，都不相同， 则加入到该链表的最后
                 	// 	 	注意把元素添加到链表后，立即判断，该链表是否已经有8个结点
                 	// 		就调用treeifBin()，对当前的链表进行树化，转成红黑树
                 	// 		注意， 在转成红黑树时，要进行判断：当table数组的大小 < 64，则不进行树化，如下：
                 	//         if (tab == null || (n = tab.length) < MIN_TREEIFY_CAPACITY)
   								//            resize();
                 	//				如果上面条件成立，先table扩容。
                 	// 				只有上面条件不成立时，才进行转成红黑树
                  	// 2.  依次和该链表的每一个元素比较过程中，如果有相同元素，就直接break
                   for (int binCount = 0; ; ++binCount) {
                       if ((e = p.next) == null) {
                         	// 最后一个元素了,然后挂载在最后面
                           p.next = newNode(hash, key, value, null);
                           // >= 7 (其实有8个)
                           if (binCount >= TREEIFY_THRESHOLD - 1) // -1 for 1st
                               treeifyBin(tab, hash);
                           break;
                       }
                       if (e.hash == hash &&
                           ((k = e.key) == key || (key != null && key.equals(k))))
                         	// 放弃添加了
                           break;
                       p = e;
                   }
               }
               if (e != null) { // existing mapping for key
                   V oldValue = e.value;
                   if (!onlyIfAbsent || oldValue == null)
                       e.value = value;
                   afterNodeAccess(e);
                   return oldValue;
               }
           }
         
           ++modCount;
         	// 放入了一个元素之后，如果大于threshold，则需要扩容，第一次这里的threshold为12
           if (++size > threshold)
               resize();
         	// 留给子类去使用的，比如LinkedHashMap中去使用，形成有序链表呀，等等
           afterNodeInsertion(evict);
           return null;
       }
   ```

   ```java
       /**
        * Initializes or doubles table size.  If null, allocates in
        * accord with initial capacity target held in field threshold.
        * Otherwise, because we are using power-of-two expansion, the
        * elements from each bin must either stay at same index, or move
        * with a power of two offset in the new table.
        *
        * @return the table
        */
       final Node<K,V>[] resize() {
           Node<K,V>[] oldTab = table;
           int oldCap = (oldTab == null) ? 0 : oldTab.length;
           int oldThr = threshold;
           int newCap, newThr = 0;
           if (oldCap > 0) {
               if (oldCap >= MAXIMUM_CAPACITY) {
                   threshold = Integer.MAX_VALUE;
                   return oldTab;
               }
               else if ((newCap = oldCap << 1) < MAXIMUM_CAPACITY &&
                        oldCap >= DEFAULT_INITIAL_CAPACITY)
                   newThr = oldThr << 1; // double threshold
           }
           else if (oldThr > 0) // initial capacity was placed in threshold
               newCap = oldThr;
           else {               // zero initial threshold signifies using defaults
   					// 第一次都为0的时候
             newCap = DEFAULT_INITIAL_CAPACITY; 	// 1 << 4,  16
             	// 0.75 * 16 = 12， 如果使用了12个空间，那么就需要扩容了呀～， 防止阻塞（操作量比较大的时候）
               newThr = (int)(DEFAULT_LOAD_FACTOR * DEFAULT_INITIAL_CAPACITY);
           }
           if (newThr == 0) {
               float ft = (float)newCap * loadFactor;
               newThr = (newCap < MAXIMUM_CAPACITY && ft < (float)MAXIMUM_CAPACITY ?
                         (int)ft : Integer.MAX_VALUE);
           }
         
           threshold = newThr;
           @SuppressWarnings({"rawtypes","unchecked"})
         
           Node<K,V>[] newTab = (Node<K,V>[])new Node[newCap];
   				// 将开辟的空间指向table
         	table = newTab;
           if (oldTab != null) {
               for (int j = 0; j < oldCap; ++j) {
                   Node<K,V> e;
                   if ((e = oldTab[j]) != null) {
                       oldTab[j] = null;
                       if (e.next == null)
                           newTab[e.hash & (newCap - 1)] = e;
                       else if (e instanceof TreeNode)
                           ((TreeNode<K,V>)e).split(this, newTab, j, oldCap);
                       else { // preserve order
                           Node<K,V> loHead = null, loTail = null;
                           Node<K,V> hiHead = null, hiTail = null;
                           Node<K,V> next;
                           do {
                               next = e.next;
                               if ((e.hash & oldCap) == 0) {
                                   if (loTail == null)
                                       loHead = e;
                                   else
                                       loTail.next = e;
                                   loTail = e;
                               }
                               else {
                                   if (hiTail == null)
                                       hiHead = e;
                                   else
                                       hiTail.next = e;
                                   hiTail = e;
                               }
                           } while ((e = next) != null);
                           if (loTail != null) {
                               loTail.next = null;
                               newTab[j] = loHead;
                           }
                           if (hiTail != null) {
                               hiTail.next = null;
                               newTab[j + oldCap] = hiHead;
                           }
                       }
                   }
               }
           }
           return newTab;
       }
   ```

   -----

   HashSet扩容机制

   1. HashSet底层是HashMap，第一次添加时，table数组扩容到16，临界值(threshold)是16 * 加载因子(loadFactor) 是0.75 = 12
   2. 元素的个数大于临界值12，就会扩容到16 * 2 = 32,  新的临界值就是32 * 0.75 = 24，依次类推
   3. 在Java8 中， 如果一条链表的元素个数到达TREEIFY_THRESHOLD(默认是8)，并且table的大小>= MIN_TREEIY_CAPACITY(默认是64)，就会进行树化，否则仍然 **采用数组扩容机制**。

   

