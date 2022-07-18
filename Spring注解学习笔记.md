# Spring常用注解笔记

## @ApiOperation

`@ApiOperation`是Swagger包中的一种注解.

使用`@ApiOperation`注解用来描述我们写的接口。

`@ApiOperation` 注解提供了丰富的属性来允许我们自定义接口描述信息，包括接口名称，接口所属分组等。

## @ApiParam

`@ApiParam`可以作用在接口方法上面以及接口方法中的参数位置。

其主要是用来给接口中的参数定义相关参数说明，帮助相关人员理解接口中每个参数的含义。

`@ApiParam` 注解同样也提供了丰富的属性，来允许我们对接口中的参数添加描述信息，包括该参数的具体含义、参数是否必须传递等。

## @Order

`@Order`控制配置类的加载顺序

**待深入理解用途**

## @Autowired

依赖注入。`@Autowired` 可以用在以下地方：

- 用在方法上（构造方法、setter方法、普通方法上）
- 用在字段上（单个字段、字段数组、集合类型）
- 用在Spring内部的接口上
- 用在参数上。如：void func(@Autowired Animal animal)

## @PostConstruct

`@PostContruct`是Spring框架的注解，在方法上加该注解会在Spring容器初始化的时候执行该方法。
