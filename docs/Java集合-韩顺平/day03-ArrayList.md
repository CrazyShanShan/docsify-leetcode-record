-----

## ArrayList<>注意事项：

1. permits all elements, including null, ArrayList可以加入null，并且多个
2. ArrayList是由数组来实现存储的
3. ArrayList基本等同于Vector，除了ArrayList是线程不安全。 在多线程情况下， 不建议使用ArrayList

-----

## ArrayList扩容机制

1. Arraylist中维护了一个Object类型的数组elemntData。

   transient Object[] elementData

   transient表示瞬间，该属性不会被序列化

2. 当创建ArrayList对象时，如果使用的是无参构造器，则初始elementData容量为0，第一次添加，则扩容elementData为10，如需要再次扩容，则扩容elementData为1.5倍

3. 如果使用过的是指定大小的构造器，则初始elementData容量为指定大小，如果需要扩容，则直接扩容elementData为1.5倍。

---

## ArrayList源码解读

这里主要需要听懂啦。 

**构造方法：**

```
1. 0 或者无参数构造器
	创建了一个elementData数组={}
2. 有参数构造器，且n : int 不为0
	创建了一个指定大小的elementData = new elementData[capacity]
```

**add:**

```
1. 先确定是否要扩容
	1. 确定一个minCapacity: 1 + size
	2. 然后看一下elementDat的大小够不够，如果不够就需要调用grow()去扩容
	
	1. 如果是有参数的构造器，扩容机制
		第一次扩容，就按照elementDat的1.5倍扩容
	2. 如果是无参数的构造器，第一次扩容的大小为10
2. 然后在执行 赋值
```

这里放一些关键的代码吧

**elementData**

```
 /**
     * The array buffer into which the elements of the ArrayList are stored.
     * The capacity of the ArrayList is the length of this array buffer. Any
     * empty ArrayList with elementData == DEFAULTCAPACITY_EMPTY_ELEMENTDATA
     * will be expanded to DEFAULT_CAPACITY when the first element is added.
     */
    transient Object[] elementData; // non-private to simplify nested class access
```



**EMPTY_ELEMENTDATA**

```

    /**
     * Shared empty array instance used for empty instances.
     */
    private static final Object[] EMPTY_ELEMENTDATA = {};
```

**DEFAULTCAPACITY_EMPTY_ELEMENTDATA**

```
    /**
     * Shared empty array instance used for default sized empty instances. We
     * distinguish this from EMPTY_ELEMENTDATA to know how much to inflate when
     * first element is added.
     */
    private static final Object[] DEFAULTCAPACITY_EMPTY_ELEMENTDATA = {};
```

**ArrayLIst()**

```

    /**
     * Constructs an empty list with an initial capacity of ten.
     */
    public ArrayList() {
        this.elementData = DEFAULTCAPACITY_EMPTY_ELEMENTDATA;
    }
```

**public ArrayList(int initialCapacity)**

```
   /**
     * Constructs an empty list with the specified initial capacity.
     *
     * @param  initialCapacity  the initial capacity of the list
     * @throws IllegalArgumentException if the specified initial capacity
     *         is negative
     */
    public ArrayList(int initialCapacity) {
        if (initialCapacity > 0) {
            this.elementData = new Object[initialCapacity];
        } else if (initialCapacity == 0) {
            this.elementData = EMPTY_ELEMENTDATA;
        } else {
            throw new IllegalArgumentException("Illegal Capacity: "+
                                               initialCapacity);
        }
    }
```

**public boolean add(E e)**

```
/**
 * Appends the specified element to the end of this list.
 *
 * @param e element to be appended to this list
 * @return <tt>true</tt> (as specified by {@link Collection#add})
 */
public boolean add(E e) {
    ensureCapacityInternal(size + 1);  // Increments modCount!!
    elementData[size++] = e;
    return true;
}
```

****

**private void ensureCapacityInternal(int minCapacity)**

```

    private void ensureCapacityInternal(int minCapacity) {
        ensureExplicitCapacity(calculateCapacity(elementData, minCapacity));
    }
```

```
   private static int calculateCapacity(Object[] elementData, int minCapacity) {
        if (elementData == DEFAULTCAPACITY_EMPTY_ELEMENTDATA) {
            return Math.max(DEFAULT_CAPACITY, minCapacity);
        }
        return minCapacity;
    }
```

**private void ensureExplicitCapacity(int minCapacity) **

```
   private void ensureExplicitCapacity(int minCapacity) {
        modCount++;

        // overflow-conscious code
        if (minCapacity - elementData.length > 0)
            grow(minCapacity);
    }
```

**private void grow(int minCapacity)**

```
    /**
     * Increases the capacity to ensure that it can hold at least the
     * number of elements specified by the minimum capacity argument.
     *
     * @param minCapacity the desired minimum capacity
     */
    private void grow(int minCapacity) {
        // overflow-conscious code
        int oldCapacity = elementData.length;
        int newCapacity = oldCapacity + (oldCapacity >> 1);
        if (newCapacity - minCapacity < 0)
            newCapacity = minCapacity;
        if (newCapacity - MAX_ARRAY_SIZE > 0)
            newCapacity = hugeCapacity(minCapacity);
        // minCapacity is usually close to size, so this is a win:
        elementData = Arrays.copyOf(elementData, newCapacity);
    }
```











