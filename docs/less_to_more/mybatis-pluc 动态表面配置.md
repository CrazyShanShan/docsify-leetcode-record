## Mybatis-plus动态表名配置

1. 默认

   数据库表使用的是标准下划线命名，并且能对应上实体类的类名，我们不需要去手动匹配

   user_info -> UserInfo

2. 前缀

   t_user_info ->userInfo

   ```
   mybatis-plus.``global``-config.db-config.table-prefix=t_
   ```

3. 添加全局配置

   ```
   mybatis-plus.global-config.db-config.table-underline=false
   ```

4. 指定当前类所对应的表名

   ```javaUs
   @Data
   @TableName(value = "user")
   public class UserInfo {
       private Integer id;
       private String userName;
       private String passWord;
   }
   ```

   

