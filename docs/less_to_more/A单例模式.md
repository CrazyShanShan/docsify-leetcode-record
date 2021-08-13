# 单例模式

摘抄URL： https://mp.weixin.qq.com/s?__biz=MzI4Njg5MDA5NA==&mid=2247484239&idx=1&sn=6560be96e456b513cb1e4f78a740a258&chksm=ebd7424edca0cb584906fb97679cf2ca557f430fbc87d2c86ce0652d2e3c36c2528466942df5&scene=21#wechat_redirect

## 前言

原来粗略学过一点单例，自己最近在看3y的博客，看到有单例，就来看一看。

## 概述

单例模式定义很简单：  **一个类中能创建一个实例**， 所以被称之为单例

什么时候用到单例模式：

- 类的状态与对象无关。
- 频繁创对象、管理对象是一件耗费资源的事。

Java Web:

- Servlet 是单例的
- Struts2 是多例多
- SpringMVC是单例多

Struts2为什么要多例：

- Struts2是基于Filter拦截类，ognl引擎对变量注入。

能使用一个对象来做就不用实例化，就能减少我们空间和内存的开销。

那么使用静态类.doSomething()和单例对象调用方法的效果是一样的啊。

- 但是静态类.doSomething()体现的是 基于对象， 而使用单例模式体现的是 面向对象。

## 编写单例模式的代码

编写单例模式的代码其实很简单，就分了三步：

- 将构造函数私有化
- 在类的内部创建实例
- 提供获取唯一实例的方法

### 饿汉式

```java
public class Java3y {
	private Java3y(){};
	
	private static Java3y java3y = new Java3y();
	
	public static Student getJava3y() {
		return java3y;
	}
	
}
```

这种代码被我们称之为：  “饿汉式”

- 一上来就创建对象了， **如果该实例从始至终都没被使用过，则会造成内存浪费。**

### 简单懒汉式

- 设计成 **用到的时候再创建对象**

```java
public class Java3y {

    // 1.将构造函数私有化，不可以通过new的方式来创建对象
    private Java3y(){}

    // 2.1先不创建对象，等用到的时候再创建
    private static Java3y java3y = null;

    // 2.1调用到这个方法了，证明是要被用到的了
    public static Java3y getJava3y() {

        // 3. 如果这个对象引用为null，我们就创建并返回出去
        if (java3y == null) {
            java3y = new Java3y();
        }

        return java3y;
    }
}

```

该代码，在单线程环境下是可以的，但是 **在多线程环境下就不行了。**

解决这个问题也很简单，只要加锁就可以了

```java
 public static synchronized Java3y getJava3y() {
```

### 双重检测机制DCL 懒汉式

上面那种直接在方法上枷锁的方式其实不够好，因为 **在方法上加了内置锁** 在多线程环境下性能会比较低下，  因此，我们可以 **将锁的范围缩小。**

```java
public class Java3y {
	private Java3y() {} ;
	
	private static Java3y java3y = null;
	
	public static Javay3 getJava3y() {
		if (java3y == null) {
				
			synchronized(Java3y.class) {
				java3y = new Java3y();
			}
		}
					return java3y;


	}
}
```

上面的代码还是不可行。 

- 线程A和B同时调用getJava3y()方法，同时判断 java == null。
- 此时线程A得到CPU的控制权-->进入同步代码块-->创建对象-->返回对象
- 线程A完成了以后，此时线程B得到了CPU的控制权。同样是-->进入同步代码块-->创建对象-->返回对象
- 很明显的是：Java3y类**返回了不止一个实例**！所以上面的代码是不行的！



： 那 **再判断一下对象是否存在是否就稳了？**

```java
public class Java3y {
	private Java3y(){};
	
	private static Java3y java3y = null;
	
	private staic Java3y getJavay3() {
		if (java3y == null) {
     	synchronized(Java3y.class) {
       	if (java3y == null) {
          java3y = new Java3y();
        } 
      }
    }
	}
}
```



: **还是不可以，这里会有。重排序的问题**

```sh
线程A：Helper helper=new Helper()
线程B：return helper;
线程A：helper内属性初始化
导致线程B获得的对象没有被完整的初始化。

是因为指令重排造成的。直接原因也就是 初始化一个对象并使一个引用指向他 这个过程不是原子的。导致了可能会出现引用指向了对象并未初始化好的那块堆内存，使用volatile修饰对象引用，防止重排序即可解决。

1、栈内存开辟空间给help引用
2、堆内存开辟空间准备初始化对象
3、初始化对象
4、栈中引用指向这个堆内存空间地址
3和4可能会重排序

加入volatile之后查看汇编代码可以发现多了一句 lock addl $0x0,(%esp)
相当于一个内存屏障。

volatile的作用：
保证内存可见性，防止指令重排序，并不保证操作原子性。

保证可见性：使用该变量必须重新去主内存读取，修改了该变量必须立刻刷新主内存。
防止重排序：通过插入内存屏障。
```



要解决可以，加上 volatile关键字， **volatile有内存屏障功能**

```java
public class Java3y {
    private Java3y() {
    }

    private static volatile Java3y java3y = null;

    public static Java3y getJava3y() {
        if (java3y == null) {

            // 将锁的范围缩小，提高性能
            synchronized (Java3y.class) {

                // 再判断一次是否为null
                if (java3y == null) {
                    java3y = new Java3y();
                }
            }
        }
        return java3y;
    }
}
```



#### 静态内部类 懒汉式

还可以使用 **静态内部类这种巧妙的方式** 来实现单例模式！原理如下：

- 当任何一个线程 **第一次调用getInstance()时**， 都会使SingletonHolder被加载和被初始化，此时静态初始化器将执行Singleton的初始化操作。（**被调用才进行初始化！**）
- 初始化静态数据时，Java提供了线程安全性保证。

### 枚举方式实现

使用枚举就非常简单了：

```java
public enum Java3y {
	Java_3_y_3_y;
}
```

好处：

- 简单，非常简单
-  ** 放置多次实例化**， 即使再面对复杂的序列化或者反射攻击的时候



### 总结

单例模式的写法有5中：

- 饿汉式

- 简单懒汉式
- DCL双重检测加锁

```java
pulic class Demo { 
	private Demo() {};
	
	private static volatile Demo demo;
	
	public static Demo getDemo() {
		if (demo == null) {
			synchronized(Demo.class) {
				if (demo == null) {
					return new Demo();
				}
				
				
			}
		}
	
	}
	
}




```



- 静态内部类实现懒汉式

```java
public class Demo {
  private Demo(){};
 
  private static class LazyHolder {
    private static final Java3y INSTANCE = new Java3y();
  }
  
 	public static final Demo getDemo(){
    return LazyHolder.INSTANCE;
  }
  
}
```



- 枚举方式

