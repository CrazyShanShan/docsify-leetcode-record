# Springboot自动装配原理

摘抄URL： https://www.zhihu.com/search?type=content&q=%E9%9D%A2%E8%AF%95%EF%BC%9ASpringboot%E8%87%AA%E5%8A%A8%E9%85%8D%E7%BD%AE%E5%8E%9F%E7%90%86

## 前言

一直知道springboot有自动装配，但是一直没有去看自动装配是怎们装配的，今天在知乎上找个博客看看。

## 一切从简

太难了，看的我好恶心。

一个简单的回答：

Spring Boot启动的时候会通过@EnableAutoConfiguration注解找到META-INF/spring.factories配置文件中的所有自动配置类，并对其进行加载，而这些自动配置类都是以AutoConfiguration结尾来命名的，它实际上就是一个JavaConfig形式的Spring容器配置类，它能通过以Properties结尾命名的类中取得在全局配置文件中配置的属性如：server.port，而XxxxProperties类是通过@ConfigurationProperties注解与全局配置文件中对应的属性进行绑定的。

- `SpringBoot`启动会加载大量的自动配置类（通过“`SPI`”的方式），然后会根据条件注解保留一些需要的类。
- 我们新引入一个组件，可以先看看springBoot是否已经有默认的提供。
- `SpringBoot`基本实现了“零配置“，并且开箱即用。

