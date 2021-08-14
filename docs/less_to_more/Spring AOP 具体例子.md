# Spring Aop具体例子

从码神之路 博客项目中学到的，下面主要介绍两个例子

- log记录方法运行时间
- redis进行缓存处理，提高效率

## 



## Log记录方法运行时间

1. 定义注解

```java
package org.example.common.aop;


import java.lang.annotation.*;

/**
 * 注解
 * @author crazys
 */
@Target(ElementType.METHOD)  // 
@Retention(RetentionPolicy.RUNTIME)
@Documented
public @interface LogAnnotation {

    String module() default "";
    
    String operator() default "";
}

```

2. 定义切面类

```java
package org.example.common.aop;

import com.alibaba.fastjson.JSON;
import lombok.extern.slf4j.Slf4j;
import org.aspectj.lang.ProceedingJoinPoint;
import org.aspectj.lang.annotation.Around;
import org.aspectj.lang.annotation.Aspect;
import org.aspectj.lang.annotation.Pointcut;
import org.aspectj.lang.reflect.MethodSignature;
import org.example.utils.HttpContextUtils;
import org.example.utils.IpUtils;
import org.springframework.stereotype.Component;

import javax.servlet.http.HttpServletRequest;
import java.lang.reflect.Method;

/***
 * @Description: "log aspect"
 * @Author: ZBZ
 * @Date: 2021/8/7
 */

@Component
@Aspect
@Slf4j
public class LogAspect {

    @Pointcut("@annotation(org.example.common.aop.LogAnnotation)")
    public void pt(){}


    /**
     *
     * @Author: ZBZ
     * @Date: 2021/8/7
     * @param joinPoint:
     * @return: java.lang.Object
     **/
    @Around("pt()")
    public Object log(ProceedingJoinPoint joinPoint) throws Throwable {
        long beginTime = System.currentTimeMillis();
        // 执行方法
        Object result = joinPoint.proceed();

        long time = System.currentTimeMillis() - beginTime;
        // 保存日志
        recordLog(joinPoint, time);
        return result;
    }




    private void recordLog(ProceedingJoinPoint joinPoint, long time) {
        MethodSignature signature = (MethodSignature) joinPoint.getSignature();
        Method method = signature.getMethod();
        LogAnnotation logAnnotation = method.getAnnotation(LogAnnotation.class);

        log.info("================ log start ================");
        log.info("module:{}", logAnnotation.module());
        log.info("operation:{}", logAnnotation.operator());

        // 请求类名和方法名
        String className = joinPoint.getTarget().getClass().getName();
        String methodName = signature.getName();
        log.info("request method:{}", className +"." +methodName + "()");

        // 请求的参数 和方法名
        Object[] args = joinPoint.getArgs();
        String params;
        params = args.length > 0 ? JSON.toJSONString(args[0]) : "";
        log.info("params:{}", params);

        // 获取Request 设置IP地址
        HttpServletRequest request = HttpContextUtils.getHttpServletRequest();
        log.info("ip{}", IpUtils.getIpAddr(request));

        log.info("execute time: {} ms" + time);
        log.info("================ log end ================");


    }

}

```

3. 具体使用   @LogAnnotation(module = "文章", operator = "获取文章列表")

```java
 /**
     * 首页文章 列表
     * @Author: ZBZ
     * @Date: 2021/8/5
     * @param pageParams: page pageNum
     * @return: org.example.vo.Result
     **/
    @PostMapping
    @LogAnnotation(module = "文章", operator = "获取文章列表")
    @ApiOperation("根据传来的 page pageNUm 。返回首页文章 列表")
    @Cache(expire = 5 * 60 * 1000,name = "listArticle")
    public Result listArticles(@RequestBody PageParams pageParams) {
        return articleService.listArticles(pageParams);
    }
```



## REDIS缓存全局实现

1. Annotation

```java
package org.example.common.cache;


import java.lang.annotation.*;

/**
 * Cacche
 * @Author: ZBZ
 * @Date: 2021/8/12
 **/
@Target(ElementType.METHOD)
@Retention(RetentionPolicy.RUNTIME)
@Documented
public @interface Cache {

    long expire() default 1*60*1000;

    // 缓存标识 key
    String name() default "";


}

```

2. Aspect类

```java
package org.example.common.cache;

import com.alibaba.fastjson.JSON;
import lombok.extern.slf4j.Slf4j;
import org.apache.commons.codec.digest.DigestUtils;
import org.apache.commons.lang3.StringUtils;
import org.apache.ibatis.annotations.Arg;
import org.aspectj.lang.ProceedingJoinPoint;
import org.aspectj.lang.Signature;
import org.aspectj.lang.annotation.Around;
import org.aspectj.lang.annotation.Aspect;
import org.aspectj.lang.annotation.Pointcut;
import org.example.vo.Result;
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.data.redis.core.RedisTemplate;
import org.springframework.stereotype.Component;

import javax.annotation.Resource;
import java.lang.reflect.Method;
import java.time.Duration;

/***
 * @Description: "cache aspect"
 * @Author: ZBZ
 * @Date: 2021/8/12
 */

@Aspect
@Component
@Slf4j
public class CacheAspect {

    @Resource
    private RedisTemplate<String, String> redisTemplate;

    @Pointcut("@annotation(org.example.common.cache.Cache)")
    public void pt() {
    }


    @Around("pt()")
    public Object around(ProceedingJoinPoint pjp) {
        try {
            Signature signature = pjp.getSignature();
            // className
            String className = pjp.getTarget().getClass().getSimpleName();
            // 调用的方法
            String methodName = signature.getName();

            Class[] parameterTypes = new Class[pjp.getArgs().length];
            Object[] args = pjp.getArgs();

            String params = "";
            for (int i = 0; i < args.length; i++) {
                if (args[i] != null) {
                    params += args[i].getClass();
                    parameterTypes[i] = args[i].getClass();
                } else {
                    parameterTypes[i] = null;
                }
            }
            log.info("params: {}", params);

            if (StringUtils.isNotEmpty(params)) {
                // 加密，以放置出现key过长以及字符串转义获取不到的情况
                params = DigestUtils.md5Hex(params);
            }

            Method method = signature.getDeclaringType().getMethod(methodName, parameterTypes);

            // 获取Cache注释
            Cache annotation = method.getAnnotation(Cache.class);
            // 缓存过期时间
            long expire = annotation.expire();
            // 缓存名称
            String name = annotation.name();
            ;
            // key
            String redisKey = name + "::" + className + "::" + methodName + "::" + params;
            String redisValue = redisTemplate.opsForValue().get(redisKey);
            if (StringUtils.isNotEmpty(redisValue)) {
                log.info("走的缓存: {},{}", className, methodName);
                Result result = JSON.parseObject(redisValue, Result.class);
                return result;
            }

            Object proceed = pjp.proceed();

            // 存入缓存
            redisTemplate.opsForValue().set(redisKey, JSON.toJSONString(proceed), Duration.ofMillis(expire));
            log.info("存入缓存～～:{},{}", className, methodName);
            return proceed;
        } catch (Throwable throwable) {
            throwable.printStackTrace();
        }
        return Result.fail(-999, "系统错误");
    }


}

```

3. 具体使用

```java
 /**
     * 首页文章 列表
     * @Author: ZBZ
     * @Date: 2021/8/5
     * @param pageParams: page pageNum
     * @return: org.example.vo.Result
     **/
    @PostMapping
    @LogAnnotation(module = "文章", operator = "获取文章列表")
    @ApiOperation("根据传来的 page pageNUm 。返回首页文章 列表")
    @Cache(expire = 5 * 60 * 1000, name = "listArticle")
    public Result listArticles(@RequestBody PageParams pageParams) {
        return articleService.listArticles(pageParams);
    }
```

