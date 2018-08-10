## Annotation注解
- [ 你必须知道的APT、annotationProcessor、android-apt、Provided、自定义注解](http://blog.csdn.net/xx326664162/article/details/68490059)


### Enum（枚举）使用注解替代
- [android开发Enum （枚举）的完美替代 —— @IntDef的使用](http://blog.csdn.net/young21234/article/details/49962659)


### Java注解的知识点
- [java基础（注解）](https://www.jianshu.com/p/3d353e807dc7)


##### 1、自定义注解

声明一个注解格式：**@interface 注解名 {}**
结论：**注解本质上就是一个接口。**它扩展了java.lang.annotation.Annotation接口;在java中所有注解都是Annotation接口的子接口。

- 1.1、注解的成员
    > 注解本质上就是一个接口，那么它也可以有属性和方法。但是接口中的属性是static final的，在注解中注解没有什么意义。在开发中注解中经常存在的是方法。而在注解中叫做**注解的属性**.  

- 1.2、注解的属性的类型
    > 1 - 基本类型  
    2 - String  
    3 - 枚举类型  
    4 - 注解类型  
    5 - Class类型  
    6 - 以上类型的一维数组类型  
    
- 1.3、关于注解的属性声明后的使用
    > (1) - 如果一个注解有属性，那么在使用注解时，要对属性进行赋值操作。例如：@MyAnnotation3(st = "aaa")  
    >
    > (2) - 如果一个注解的属性有多个，都需要赋值，使用","分开属性。@MyAnnotation3(st = "aaa",i=10)  
    >
    > (3) - 也可以给属性赋默认值 double d() default 1.23;如果属性有默认值，在使用注解时，就可以不用为属性赋值。  
    >
    > (4) - 如果属性是数组类型  
        - a.可以直接使用 属性名={值1,值2,。。。}方式,例如 @MyAnnotation3(st = "aaa",i=10,sts={"a","b"})  
        - b.如果数组的值只有一个也可以写成下面方式 @MyAnnotation3(st = "aaa",i=10,sts="a"),注意sts属性它是数组类型，也就是说，只有一个值时，可以省略"{}"  
    >
    > (5) - 对于属性名称value的操作.  
        - a.如果属性名称叫value,那么在使用时，可以省略属性名称 @MyAnnotation3("hello")  
        - b.如果有多个属性，都需要赋值，其中一个叫value,这时，必须写属性名称@MyAnnotation3(value="hello",i=10)  
        - c.如果属性名称叫value,它的类型是数组类型.  
            - 1.只有这个value属性可以直接赋值，不能写属性名称,但是，如果只有一个值@MyAnnotation3({"abc"})或@MyAnnotation3("abc"),但是如果有多个值@MyAnnotation3({"abc","def"})  
            - 2.如果有多个属性，属性名称叫value所有属性都需要赋值，那么必须写属性名称.    


##### 2、元注解

**元注解是指注解的注解。**包括 `@Retention` `@Target` `@Document` `@Inherited`四种。

- 2.1、@Retention: 定义注解的保留策略
    > @Retention(RetentionPolicy.SOURCE) // 注解仅存在于源码中，在class字节码文件中不包含  
    @Retention(RetentionPolicy.CLASS) // 默认的保留策略，注解会在class字节码文件中存在，但运行时无法获得  
    @Retention(RetentionPolicy.RUNTIME) // 注解会在class字节码文件中存在，在运行时可以通过反射获取到  
				 
- 1.2、@Target：定义注解的作用目标
    > @Target(ElementType.TYPE) // 接口、类、枚举、注解  
    @Target(ElementType.FIELD) // 字段、枚举的常量  
    @Target(ElementType.METHOD) // 方法  
    @Target(ElementType.PARAMETER) // 方法参数  
    @Target(ElementType.CONSTRUCTOR) // 构造函数  
    @Target(ElementType.LOCAL_VARIABLE) // 局部变量  
    @Target(ElementType.ANNOTATION_TYPE) // 注解  
    @Target(ElementType.PACKAGE) // 包    
    > 
    > 由以上的源码可以知道，他的elementType可以有多个，一个注解可以为类的，方法的，字段的等等  

- 1.3、@Document：说明该注解将被包含在javadoc中
- 1.4、@Inherited：说明子类可以继承父类中的该注解