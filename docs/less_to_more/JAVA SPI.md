# JAVASPI

URL：https://www.cnblogs.com/huzi007/p/6679215.html

## 1. 什么是JAVA的SPi

SPI全程为（Service Provider interface )， 是JDK内置的一种服务提供发现机制。目前有不少框架用它来做服务的扩展发现，简单来说，其就是一种动态替换发现的机制，举个例子来说，有个接口，想运行时动态的给它添加实现，

具体是在JAR包的“src/META_INFA/services/”目录下建立一个文件，文件名是接口的全限定名，文件的内容可以有多行，每行都是该接口对应的具体实现类的全限定名。

## 2. 运用场景

比如你想扩展一些框架，比如Spring的一些功能，就是要实现它接口，然后自己配置。



## 3. 例子代码

```java
package com.ming.spi.service;

/**
 * 定义一个dog的接口
 * @author ming
 *
 */
public interface DogService {

    void sleep();
}

package com.ming.spi.service.imp;

import com.ming.spi.service.DogService;

public class BlackDogServiceImpl implements DogService{

    @Override
    public void sleep() {
        System.out.println("黑色dog。。。汪汪叫，不睡觉...");
        
    }
    
}

package com.ming.spi.service.imp;

import com.ming.spi.service.DogService;

public class WhilteDogServiceImpl implements DogService{

    @Override
    public void sleep() {
        System.out.println("白色dog。。。呼呼大睡觉...");
        
    }

}

测试代码
  
package com.ming.spi.service;

import java.util.ServiceLoader;

public class Test {

    public static void main(String[] args) throws Exception {
        ServiceLoader<DogService> loaders = ServiceLoader.load(DogService.class);
        for (DogService d : loaders) {
            d.sleep();
        }
    }
}


```

然后是在src/META-INF/services/com.ming.spi.service.DogService文件中的代码：

```java
com.ming.spi.service.imp.BlackDogServiceImpl
com.ming.spi.service.imp.WhilteDogServiceImpl

```

最后运行结果就是你需要的两个实现



## 总结：

Java的spi运行流程是运用java.util.ServiceLoader这个类的load方法在src/META-INF/services寻找对应的全路径接口名称的文件，然后在文件中找到对应的实现方法并注入实现，然后就可以运用了

