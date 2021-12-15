## Springboot中读取配置文件

### 几种数据格式的表示方式

1. 普通的值

   ```
   age: 18
   name: shanshan
   ```

   

2. 对象、Map

   ```
   person:
   	age: 18
   	name: shanshan
   ```

   

3. 数组（List、Set)

   ```\
   hands:
   	- left
   	- right
   ```

### 第一种读取方式@value

```
server: 
	port: 8081
```

```
@Value(${server.port})
public String port;
```

### 第二种读取方式@ConfigurationProperties

如果需要一个JavaBean 来专门映射配置的话,我们一般会使用**@ConfigurationProperties**来读取.

```java
student:
    age: 18
    name: mysgk
@Component
@ConfigurationProperties(prefix = "student")
public class Student {

    private String name;

    private Integer age;

    public String getName() {
        return name;
    }

    public void setName(String name) {
        this.name = name;
    }

    public Integer getAge() {
        return age;
    }

    public void setAge(Integer age) {
        this.age = age;
    }

    @Override
    public String toString() {
        return "Student{" +
                "name='" + name + '\'' +
                ", age=" + age +
                '}';
    }
}
```

使用**@ConfigurationProperties**,需要配置一个prefix (前缀) 参数, 即写上 key 就可以了.

