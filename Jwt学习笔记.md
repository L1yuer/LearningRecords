# JWT笔记

## 概念

**`JWT token`**

**`JSON Web Token`** 是目前最流行的跨域身份验证解决方案.
**`JWT`** 的本质就是一个字符串，它是将用户信息保存到一个Json字符串中，然后进行编码后得到一个 **`JWT token`** ，并且这个 **`JWT token`** 带有签名信息，接收后可以校验是否被篡改，所以可以用于在各方之间安全地将信息作为Json对象传输。

**`JWT`** 的认证流程如下：

首先，前端通过Web表单将自己的用户名和密码发送到后端的接口，这个过程一般是一个POST请求。建议的方式是通过SSL加密的传输(HTTPS)，从而避免敏感信息被嗅探
后端核对用户名和密码成功后，将包含用户信息的数据作为JWT的Payload，将其与JWT Header分别进行Base64编码拼接后签名，形成一个 **`JWT token`** 。
后端将 **`JWT token`** 字符串作为登录成功的结果返回给前端。前端可以将返回的结果保存在浏览器中，退出登录时删除保存的 **`JWT token`** 即可
前端在每次请求时将 **`JWT token`** 放入HTTP请求头中的Authorization属性中(解决XSS和XSRF问题)
后端检查前端传过来的 **`JWT token`** ，验证其有效性，比如检查签名是否正确、是否过期、token的接收方是否是自己等等
验证通过后，后端解析出 **`JWT token`** 中包含的用户信息，进行其他逻辑操作(一般是根据用户信息得到权限等)，返回结果

![](https://img-blog.csdnimg.cn/img_convert/900b3e81f832b2f08c2e8aabb540536a.png)


