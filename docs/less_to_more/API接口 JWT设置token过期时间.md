## JWT 设置token过期时间

### 1. 什么是JWT

jwt是json web tokens的简称，是一种token，可以理解为一种生成token的框架或者规范。

### 2. 什么是token

token是服务端生成的一串字符串，以作客户端进行请求的一个令牌，当第一次登录后，服务器生成一个token，便将此token返回给客户端，以后客户端只需带上这个token前来请求数据即可，无需再次带上用户名和密码。

### 3. 为什么要使用token

用服务器的session_id存储搭配cookies中也能够做到，为什么非要使用token呢？开发web应用其实使用哪种都可以，但如果是开发api接口，前后端分离，最好使用token，因为session + cookies是基于web的，但是针对api接口，可能会考虑到移动端，app是没有cookies和session的。

### 4. 如何实现token

其实token是一个概念模型，就是为了方便用户不用每次访问页面都输入用户密码来做验证，开发者可以针对自己开发的应用定义自己的token。只要做到不让黑客或者无聊的人钻系统的漏洞即可。设想一下，我们自定义的token只是通过简单的md5加密，很简单就找到了token的加密规则，那么他就可以伪造其他用户登录的token，可以随意的获取数据，所以个人自定义的token，没有太多的加密经验，还是很不安全的。再加上，自己定义token加密解密无形增加了工作量，可以使用现成的。

通过对token的模型总结,jwt作者总结了一套比较完善的token生成方案，它的加密方式非常安全，可以方便用户生存自己token。那么我们看下token的流程和jwt的组成。

1. 客户端携带用户名密码向服务端发送认证请求 
2. 服务端将token返回给客户端
3. 客户端每次请求都再次将请求头header携带token
4. 服务端每次刷新token，并返回给客户

Simply put , a JWT is a just string with the following format:

**header.payload.signature**

header: exp:

```
{
"typ": "JWT:,
"alg": "HS256"
}
```

typ 就是type的意思，alg 就是algorithm的意思

payload: exp:

```
{
"userId": "asdadsadsad"
}
```

这部分的本质是用户数据，就是JWT的目的是认证身份来源。

payload用来承载要传递的数据，其json结果实际上是对JWT要传递的数据的一组声明，这些声明被JWT标准称为 **claims**，它的一个属性值就是对一个claim(要求)，每一个claim的都代表特定的含义和作用。

**根据JWT的标准*，claims可以分为以下三种类型**

```
iss(Issuser): 代表这个JWT的签发主题;
sub(Subject): 代表这个JWT的主题，即它的所有人
and(Audience):代表这个JWT的接受对象
exp(Expiration time): 代表这个JWT的过期时间
nbf(Not Before): 在这个时间之前验证JWT是会失败的
iat(issued at): 代表这个JWT的签发时间
jti(JWT ID): JWT的唯一标识
```



signature:

```
// signature algrithm
data = base64urlEncode(header) +"." + base64Encode(payload)
hashedData = hash(data, secret)
signature = base64urlEncode(hashedData)
```

signature顾名思义就是签名，签名一般就是用一些算法生成一个能够认证身份的字符串，具体算法就是上面表示的，也比较简单，不赘述，唯一说明的一点是上面hash方法用到了一个secret，这个东西需要application server和authentication server双方都知道，相当于约好了同一把验证的钥匙，最终才好做认证。

最后再解释一下application server如何认证用户发来的JWT是否合法，首先服务端和客户端必须要有个约定，例如双方同时知道加密用的secret（这里假设用的就是简单的对称加密算法），那么在服务端 收到这个JWT是，就可以利用JWT前两段（别忘了JWT是个三段的拼成的字符串哦）数据作为输入，用同一套hash算法和同一个secret自己计算一个签名值，然后把计算出来的签名值和收到的JWT第三段比较，如果相同则认证通过，如果不相同，则认证不通过。就这么简单，当然，上面是假设了这个hash算法是对称加密算法,其实如果用非对称加密算法也是可以的，比方说我就用非对称的算法，那么对应的key就是一对，而非一个，那么一对公钥+私钥可以这样分配：私钥由客户端保存，公钥由服务端保存，服务端验证的时候，用公钥解密收到的signature,这样就得到了header和payload的拼接值，用这个拼接值跟前两段比较，相同就验证通过。总之，方法略不同，但大方向完全一样。

简单案例

```java
public class Demo03 {
 
    private String secret = "a1g2y47dg3dj59fjhhsd7cnewy73j";
    private SimpleDateFormat sdf = new SimpleDateFormat("yyyy-MM-dd HH:mm:ss.SSS");
 
    @Test
    public void test1() {// 生成JWT
        Map<String, Object> claims = new HashMap<String, Object>();
        claims.put("username", "zss");
        claims.put("age", 18);
 
        //生成token
        String token = Jwts.builder()
                .setClaims(claims)
                .setId("666")  //登录用户的id
                .setSubject("小马")  //登录用户的名称
                .setExpiration(new Date(System.currentTimeMillis() + 30*1000))//过期时间
                .setIssuedAt(new Date(System.currentTimeMillis()))//当前时间
                .signWith(SignatureAlgorithm.HS512, this.secret)//头部信息 第一个参数为加密方式为哈希512  第二个参数为加的盐为secret字符串
                .compact();
 
        System.out.println("token令牌是："+token);
 
        Claims claims1 = Jwts.parser()
                .setSigningKey(this.secret)
                .parseClaimsJws(token)
                .getBody();
 
        Date d1 = claims1.getIssuedAt();
        Date d2 = claims1.getExpiration();
        System.out.println("username参数值：" + claims1.get("username"));
        System.out.println("登录用户的id：" + claims1.getId());
        System.out.println("登录用户的名称：" + claims1.getSubject());
        System.out.println("令牌签发时间：" + sdf.format(d1));
        System.out.println("令牌过期时间：" + sdf.format(d2));
    }
 
}
```

