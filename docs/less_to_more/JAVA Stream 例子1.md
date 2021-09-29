## Java Stream 操作 例子1

**对数组构造流：**

```
Arrays.stream(nums)
```



1. 取出User对象中的主键ID

   ```
   list<User>
   List<Long> userIdList = new ArrayList<>();
   lambda : list.forEach()
   stream : userIdList = list.stream().map(User:getId).collect(Collectors.toList());
   
   ```

2. 创建下面要操作的实体类

   ```java
   class User{
   private Long id;       //主键id
   private String name;   //姓名
   private Integer age;   //年龄
   private String school; //学校
   public User(Long id, String name, Integer age, String school) {
      this.id = id;
      this.name = name;
      this.age = age;
      this.school = school;
   }
   List<User> list = new ArrayList<User>(){
       {
           add(new User(1l,"张三",10, "清华大学"));
           add(new User(2l,"李四",12, "清华大学"));
           add(new User(3l,"王五",15, "清华大学"));
           add(new User(4l,"赵六",12, "清华大学"));
           add(new User(5l,"田七",25, "北京大学"));
           add(new User(6l,"小明",16, "北京大学"));
           add(new User(7l,"小红",14, "北京大学"));
           add(new User(8l,"小华",14, "浙江大学"));
           add(new User(9l,"小丽",17, "浙江大学"));
           add(new User(10l,"小何",10, "浙江大学"));
       }
   };
   ```

   1. 过滤

   筛选所有学校是清华大学的user

   ```java
   List<User> userList1 = list.stream().filter(user -> "清华大学".equals(user.getSchool())).collect(Collectors.toList());
   ```

   2. 去重

   获取所有user的年龄

   ```java
   List<Integer> userAgeList = list.stream().map(User::getAge).distinct().collect(Collectors.toList());
   ```

   3. limit

   范围年龄是偶数的前2名

   ```java
   List<User> userList3 = list.stream().filter(user -> user.getAge() % 2 == 0).limit(2).collect(Collectors.toList());
   ```

   4. 排序

   按年龄排序

   ```java
   List<User> userList4 = list.stream().sorted((s1,s2) -> s2.age - s1.age).collect(Collectors.toList());
   ```

   5. skip 

   跳过n个元素再输出

   ```java
   List<User> userList5 = list.stream().skip(2).collect(Collectors.toList());
   ```

   6. map

   想得到所有"清华大学"的学生的姓名

   ```java
   List<String> userList6 = list.stream().filter(user -> "清华大学".equals(user.school)).map(User::getName).collect(Collectors.toList());
   ```

   7. mapToDouble ，mapToInt, mapToLong，返回对应类型的流

   查询学校是清华大学的user的年龄总和：

   ```java
   int` `userList7 = list.stream().filter(user -> ``"清华大学"``.equals(user.school)).mapToInt(User::getAge).sum();
   ```

   8. flatMap

   flatMap与map的区别在于 flatMap是将一个流中的每个值都转成一个个流，然后再将这些流扁平化成为一个流 。

   假设我们有一个字符串数组String[] strs = {"hello", "world"};，我们希望输出构成这一数组的所有非重复字符，那么我们用map和flatMap 实现如下：

   ```java
   List l11 = Arrays.stream(strings).map(str -> str.split(``""``)).map(str2->Arrays.stream(str2)).distinct().collect(Collectors.toList());
   List l2 = Arrays.asList(strings).stream().map(s -> s.split(``""``)).flatMap(Arrays::stream).distinct().collect(Collectors.toList());
   
   [java.util.stream.ReferencePipeline$Head@4c203ea1, java.util.stream.ReferencePipeline$Head@27f674d]
   [H, e, l, o, W, r, d]　　
   ```

   由上我们可以看到使用map并不能实现我们现在想要的结果，而flatMap是可以的。这是因为在执行map操作以后，我们得到是一个包含多个字符串（构成一个字符串的字符数组）的流，此时执行distinct操作是基于在这些字符串数组之间的对比，所以达不到我们希望的目的；flatMap将由map映射得到的Stream<String[]>，转换成由各个字符串数组映射成的流Stream<String>，再将这些小的流扁平化成为一个由所有字符串构成的大流Steam<String>，从而能够达到我们的目的。

   9. allMatch

   用于检测是否全部都满足指定的参数行为，如果全部满足则返回true，例如我们判断是否所有的user年龄都大于9岁

   ```
   Boolean b = list.stream().allMatch(user -> user.age >9);
   ```

   10. anyMatch

   anyMatch则是检测是否存在一个或多个满足指定的参数行为，如果满足则返回true，例如判断是否有user的年龄大于15岁，

   ```
   Boolean bo = list.stream().anyMatch(user -> user.age >15);
   ```

   11. noneMatch

   noneMatch用于检测是否不存在满足指定行为的元素，如果不存在则返回true，例如判断是否不存在年龄是15岁的user

   ```
   Boolean boo = list.stream().noneMatch(user -> user.age == 15);
   ```

   12. findFirst

   findFirst用于返回满足条件的第一个元素，比如返回年龄大于12岁的user中的第一个，实现如下:

   ```
   Optional<User> first = list.stream().filter(u -> u.age > 10).findFirst();
   User user = first.get();
   ```

   13.  findAny

   ```
   Optional<User> anyOne = list.stream().filter(u -> u.age > 10).findAny();
   User user2 = anyOne.get();
   ```

   14. reduce

   现在我的目标不是返回一个新的集合，而是希望对经过参数化操作后的集合进行进一步的运算，那么我们可用对集合实施归约操作。java8的流式处理提供了reduce方法来达到这一目的。

   比如我现在要查出学校是清华大学的所有user的年龄之和：

   ```
   Integer ages = list.stream().filter(student -> "清华大学".equals(student.school)).mapToInt(User::getAge).sum();
   ```

   ```
   Integer ages2 = list.stream().filter(student -> "清华大学".equals(student.school)).map(User::getAge).reduce(0,(a,c)->a+c);
   
   Integer ages3 = list.stream().filter(student -> "清华大学".equals(student.school)).map(User::getAge).reduce(0,Integer::sum);
   
   Integer ages4 = list.stream().filter(student -> "清华大学".equals(student.school)).map(User::getAge).reduce(Integer::sum).get();
   ```

   15. collect

   前面利用collect(Collectors.toList())是一个简单的收集操作，是对处理结果的封装，对应的还有toSet、toMap，以满足我们对于结果组织的需求。这些方法均来自于java.util.stream.Collectors，我们可以称之为收集器。

   收集器也提供了相应的归约操作，但是与reduce在内部实现上是有区别的，收集器更加适用于可变容器上的归约操作，这些收集器广义上均基于Collectors.reducing()实现。

   

   16. counting

   计算user的总人数

   ```
   long COUNT = list.stream().count();//简化版本
   long COUNT2 = list.stream().collect(Collectors.counting());//原始版本
   ```

   

   17. maxBy、minBy

   计算最大值和最小值

   ```
   Integer maxAge = list.stream().collect(Collectors.maxBy((s1, s2) -> s1.getAge() - s2.getAge())).get().age;
   Integer maxAge2 = list.stream().collect(Collectors.maxBy(Comparator.comparing(User::getAge))).get().age;
   Integer minAge = list.stream().collect(Collectors.minBy((S1,S2) -> S1.getAge()- S2.getAge())).get().age;
   Integer minAge2 = list.stream().collect(Collectors.minBy(Comparator.comparing(User::getAge))).get().age;
   ```

   

   18. averageInt、averageLong、averageDouble

   如计算user的年龄平均值：

   ```
   double averageAge = list.stream().collect(Collectors.averagingDouble(User::getAge));
   ```

   

   19. summarizingInt、summarizingLong、summarizingDouble

   一次性查询元素个数、总和、最大值、最小值和平均值

   ```
   IntSummaryStatistics summaryStatistics = list.stream().collect(Collectors.summarizingInt(User::getAge));
   System.out.println("summaryStatistics = " + summaryStatistics);
   summaryStatistics = IntSummaryStatistics{count=10, sum=145, min=10, average=14.500000, max=25}
   ```

    

   20.  joining

   字符串拼接

   ```
   String names = list.stream().map(User::getName).collect(Collectors.joining(","));
   ```



​	   21. groupingBy

​	    如将user根据学校分组、先按学校分再按年龄分、每个大学的user人数、每个大学不同年龄的人数：

```java
System.out.println("分组");
Map<String, List<User>> collect1 = list.stream().collect(Collectors.groupingBy(User::getSchool));

Map<String, Map<Integer, Long>> collect2 = list.stream().collect(Collectors.groupingBy(User::getSchool, Collectors.groupingBy(User::getAge, Collectors.counting())));

Map<String, Map<Integer, Map<String, Long>>> collect4 = list.stream().collect(Collectors.groupingBy(User::getSchool, Collectors.groupingBy(User::getAge, Collectors.groupingBy(User::getName,Collectors.counting()))));

Map<String, Long> collect3 = list.stream().collect(Collectors.groupingBy(User::getSchool, Collectors.counting()));

System.out.println("collect1 = " + collect1);
System.out.println("collect2 = " + collect2);
System.out.println("collect3 = " + collect3);
System.out.println("collect4 = " + collect4);

collect1 = {
  浙江大学=[User{id=8, name='小华', age=14, school='浙江大学'},
        User{id=9, name='小丽', age=17, school='浙江大学'}, 
        User{id=10, name='小何', age=10, school='浙江大学'}], 
            北京大学=[User{id=5, name='田七', age=25, school='北京大学'},
                  User{id=6, name='小明', age=16, school='北京大学'},
                  User{id=7, name='小红', age=14, school='北京大学'}], 
            清华大学=[User{id=1, name='张三', age=10, school='清华大学'},
                  User{id=2, name='李四', age=12, school='清华大学'},
                  User{id=3, name='王五', age=15, school='清华大学'},
                  User{id=4, name='赵六', age=12, school='清华大学'}]}

collect2 = {浙江大学={17=1, 10=1, 14=1}, 北京大学={16=1, 25=1, 14=1}, 清华大学={10=1, 12=2, 15=1}}

collect3 = {浙江大学=3, 北京大学=3, 清华大学=4}

collect4 = {浙江大学={17={小丽=1}, 10={小何=1}, 14={小华=1}}, 北京大学={16={小明=1}, 25={田七=1}, 14={小红=1}}, 清华大学={10={张三=1}, 12={李四=1, 赵六=1}, 15={王五=1}}}
```





​        22. partitioningBy

​		分区，分区可以看做是分组的一种特殊情况，在分区中key只有两种情况：true或false，目的是将待分区集合按照条件一分为二，java8的流式处理利用ollectors.partitioningBy()方法实现分区。

如按照是否是清华大学的user将左右user分为两个部分：

```java
System.out.println("分区");
Map<Boolean, List<User>> collect5 = list.stream().collect(
  Collectors.partitioningBy(user1 -> "清华大学".equals(user1.school)));
System.out.println("collect5 = " + collect5);


collect5 = {false=[User{id=5, name='田七', age=25, school='北京大学'}, User{id=6, name='小明', age=16, school='北京大学'}, User{id=7, name='小红', age=14, school='北京大学'}, User{id=8, name='小华', age=14, school='浙江大学'}, User{id=9, name='小丽', age=17, school='浙江大学'}, User{id=10, name='小何', age=10, school='浙江大学'}], true=[User{id=1, name='张三', age=10, school='清华大学'}, User{id=2, name='李四', age=12, school='清华大学'}, User{id=3, name='王五', age=15, school='清华大学'}, User{id=4, name='赵六', age=12, school='清华大学'}]}

```

