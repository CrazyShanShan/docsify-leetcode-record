# 工厂模式

摘抄：https://mp.weixin.qq.com/s?__biz=MzI4Njg5MDA5NA==&mid=2247484243&idx=1&sn=972cbe6cdb578256e4d4771e7ca25de3&chksm=ebd74252dca0cb44419903758e8ca52d9ab287562f80be9365e305d6dcc2deaa45b40f9fd2e9&scene=21#wechat_redirect

## 概述

工厂模式一般分为：

- 简单/静态工厂模式
- 工厂方法模式
- 抽象工厂模式

### 为什么使用工厂模式

例如，文件IO我们经常会使用到，如果BufferedReader对象 **经常要创建** 的：

```java
BufferedReader by = new BuffearedReader(new FileReader("aa.txt"));
```

总写这样的代码，就很麻烦。

然后突然，换了一个Reader，整个人就绝望了。

- 不熟悉IDEA的就到处改
- 熟悉IDEAD的就全局替换。

**那么问题来了，有没有一种方法能够上创建对象变得简单而且修改对象时能很方便呢？**

- 采用工厂模式就可以了。

### 体验工厂模式

什么是工厂？ 将我们的产品都交给工厂去生产。 工厂如何生存，我们不需要知道。

因此，我们改造一样上面的例子，首先创建一个工厂类，可以 **生产Reader对象**！

```java
public class ReaderFactory {
	public static Reader getReader() {
		return new BufferedReader(new FileReader("aa.txt"));
	}
}
```

使用

```java
Reader reader = ReaderFactory.getReader();
```

**工厂将我们创建对象的过程给屏蔽了。**

调用接口这些类就完全不用变

### 使用工厂方法的好处

- 修改了具体的实现类，对客户端而言是 **完全不用修改的。**

- 如果我们使用new的方式来创建对象的话，那么我们就说： new出来的这个对象和当前客户端 **耦合**了！
  - 也就是说，当前客户端 **依赖着** 这个new 出来的对象。

**这就是解耦合的好处！**

我现在有一个DaoFactory, 逻辑很简单就是专门创建Dao对象的

```java
public class DaoFactory {
	private static final DaoFactory factory = new DaoFactory();
	private DaoFactory(){}
	
	public static DaoFatory getInstance() {
		return factory;
	}
	public <T> T createDao(String className, class<T> claszz) {
		T t = (T) class.forName(className).newInstance();
		return t;
	}
}
```

此时，我们的Service与Dao的对象是 **低耦合**的。

## 如何使用工厂模式

### 工厂方法模式

1. 构建宠物的工厂

```java
public interface AnimalFactory {
	Animal createAnimal();
}
```

2. 构建猫和狗的工厂

```java
public class CatFactory implements AnimalFactory {
	@Override
	public Animal createAnimal() {
		return new Cat();
	}
}
```

优点：

- 客户端不需要在负责对象的创建，明确了 各个类的指责
- 如果有新的对象增加，只需要增加一个具体的类和具体的工厂类即可
- 不会影响已有的代码，尤其维护容器，增强系统的扩展性

缺点：

- 需要额外的编写代码，增加了工作量

### 简单工厂模式

店主只卖两种常见宠物

```java
public class AnimalFactory {
	public static Dog createDog() {
		return Dog();
	}
	public static Cat createCat() {
		return new Cat();
	}
	
	public static Animal createAnimal(String types) {
		if ("dog".equals(type)) {
			return new Dog();
		}
	}
	
}
```



问题：

- 需求来了，我就需要修改代码

优点：

- 只有一个具体的工厂来创建对象，代码量少。

### 抽象工厂模式

**一般的应用都写不到**

- 我们之前给每个动物都开了一个工厂，如果动物过多的话，那么就有很多的工厂。
- 那么现在可以抽象出来： 每个动物不是公的就是母的
- 那么我们有两个工厂就足够了。

1. 最大工厂

```java
public interface AnimalFatory {
	Animal createDog();
	Animal createCat();
}
```

2. 母工厂

```java
public class FemaleAnimalFactory implements AnimalFactory {
	Override
	public Animal createDog() {
		return new FemalDog();
	}
	
	@Override
	public Animal createCat() {
		return new FemaleCat();
	}
}
```

3. 公 工厂

```java
public class MaleAnimalFactory implements AnimalFactory {
	Override
	public Animal createDog() {
		return new MaleDog();
	}
	
	@Override
	public Animal createCat() {
		return new MaleCat();
	}
}
```

4. 动物普遍行为

```java
public abstract class Animal {
	public abtract void eat();
	
	public abstract void gender();
}
```

5. 猫的普遍行为

```java
public abstract class Cat extends Animal {
    // 猫喜欢吃鱼
    @Override
    public void eat() {
        System.out.println("猫吃鱼");
    }
}
```

6. 狗的普遍行为

```java
public abstract class Dog extends Animal {

    // 狗喜欢吃肉
    @Override
    public void eat() {
        System.out.println("狗吃肉");
    }

}

```

7. 猫分为公猫，猫，狗分为公狗和母狗

```java
public class FemaleCat extends Cat {

    public void gender() {
        System.out.println("I am a female Cat");
    }

}
```

...

简单来说： 工厂方法模式的工厂是创建出一种产品，而抽象工厂是创建出一类产品。

- 一类产品被称为 产品族
  - 猫一类，狗一类。
- 产品的继承结构称为产品等级
  - 狗会吃肉
    - 分别公狗和母狗
  - 猫会吃鱼
    - 分为公猫和母猫
- 具体的工厂是 **面向多个产品等级结构进行生产。**
  - 所以FemaleAnimalFactory定义了`createDog()`和`createCat()`生产母狗和母猫
  - 所以MaleAnimalFactory定义了`createDog()`和`createCat()`生产公狗和共猫

## 总结

总的来说，我们使用 **简单工厂模式比较多**， 工厂方式模式的话代码量是会比较大，抽象工厂模式的话需要业比较大的情况下才会用到。

- 工厂模式配合反射来使用也是极好的。