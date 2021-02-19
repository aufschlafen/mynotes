### spb笔记

### 开始

##### 1.父项目

#####  2.导入的依赖

```xml

	 <dependencies>
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-web</artifactId>
        </dependency>
    </dependencies>

```

**spring-boot-starter-web **

spring-boot-starter:spring-boot场景启动器，导入web模块正常运行所依赖的组件

spring boot将所有功能场景都抽取，做成starter(启动器)

### 主程序类，主入口类

@SpringBootApplication :标注在类上说明这个类是SpringBoot主配置类，Springboot应该运行这个类的main方法来启动SpringBoot应用

```
@Target({ElementType.TYPE})
@Retention(RetentionPolicy.RUNTIME)
@Documented
@Inherited
@SpringBootConfiguration
@EnableAutoConfiguration
@ComponentScan(
    excludeFilters = {@Filter(
    type = FilterType.CUSTOM,
    classes = {TypeExcludeFilter.class}
), @Filter(
    type = FilterType.CUSTOM,
    classes = {AutoConfigurationExcludeFilter.class}
)}
)
```

**@SpringBootConfiguration**:SpringBoot配置类：标注在某个类上，这是一个Spring Boot配置类

**@EnableAutoConfiguration** 自动配置

**@AutoConfigurationPackage**  自动配置包 将主配置类所在包及下面所有子包里面的组件扫描到Spring容器

​		**@Import** EnableAutoConfigurationImportSelector:导入那些组件的选择器;将所有需要导入的组件以全类名的方法返回，这些组件就会被添加到容器内

​				(xxxAutoConfiguration)就是给容器中导入这个场景需要的所有组件，配置好这些组件

###Spring Initializaer快速创建Spring Boot项目

@RestController（@ResponseBody,@controller）  将类的所有方法返回的所有数据直接写成浏览器

- resources文件夹中目录结构
  + static: 保存所有静态资源:js css images
  + templates :保存所有模板页面(SpringBoot默认jat包使用嵌入式的Tomcat,默认不支持JSP页面)
  + application properties :Spring Boot应用的配置文件



#### WEB开发

springboot对静态资源的规则

```java
 public void addResourceHandlers(ResourceHandlerRegistry registry) {
            if (!this.resourceProperties.isAddMappings()) {
                logger.debug("Default resource handling disabled");
            } else {
                Duration cachePeriod = this.resourceProperties.getCache().getPeriod();
                CacheControl cacheControl = this.resourceProperties.getCache().getCachecontrol().toHttpCacheControl();
                if (!registry.hasMappingForPattern("/webjars/**")) {
                    this.customizeResourceHandlerRegistration(registry.addResourceHandler(new String[]{"/webjars/**"}).addResourceLocations(new String[]{"classpath:/META-INF/resources/webjars/"}).setCachePeriod(this.getSeconds(cachePeriod)).setCacheControl(cacheControl));
                }

                String staticPathPattern = this.mvcProperties.getStaticPathPattern();
                if (!registry.hasMappingForPattern(staticPathPattern)) {
                    this.customizeResourceHandlerRegistration(registry.addResourceHandler(new String[]{staticPathPattern}).addResourceLocations(WebMvcAutoConfiguration.getResourceLocations(this.resourceProperties.getStaticLocations())).setCachePeriod(this.getSeconds(cachePeriod)).setCacheControl(cacheControl));
                }

            }
        }
```

（1）所有/webjars/**  ，都去classpath:/META-INF/resources/webjars找资源

​			webjars:以jar包方法引入静态资源

​			https://www.webjars.org/

寻找jquery资源：localhost:8080/webjars/jquery

（2）"/**"访问当前任何资源

```java
"classpath:/META-INF/resources/"
 "classpath:/resources/"
 "classpath:/static/" 
   "classpath:/public"
  "/" 当前项目的根路径

```



localhost:8080/abc 去静态资源文件夹中找abc

(3) 欢迎页：静态页面所有index.html页面，被"/**"映射

(4)所有**/favicon.ico都是在静态资源下找



### ##thymeleaf

eg:JSP Velocity Freemarker 

**thymeleaf语法**

1.引入   dependecies

```java
public class ThymeleafProperties {
    private static final Charset DEFAULT_ENCODING;
    public static final String DEFAULT_PREFIX = "classpath:/templates/";
    public static final String DEFAULT_SUFFIX = ".html";
//只要将html页面放在templates中，就能自动渲染
```

**导入thymeleaf名称空间**

```java
<!DOCTYPE html>
<html lang="en"  xmlns:th="http://www.thymeleaf.org">
<head>
    <meta charset="UTF-8" >
    <title>Title</title>
</head>
<body>
<h1>success</h1>
<div th:text="${hello}">bla</div>
</body>
</html>
```

（1）th:text更改当前元素里面的文本内容

（2）表达式

```properties
Simple expressions:(表达式语法)
Variable Expressions: ${...}
（1）获取对象的属性和值和方法
（2）使用内置对象
（3）内置的工具对象
Selection Variable Expressions: *{...}
Message Expressions: #{...}
Link URL Expressions: @{...}
Fragment Expressions: ~{...}
Literals
Text literals: 'one text' , 'Another one!' ,…（文本操作）
Number literals: 0 , 34 , 3.0 , 12.3 ,…
Boolean literals: true , false（布尔）
Null literal: null
Literal tokens: one , sometext , main ,…
Text operations:
String concatenation: +
Literal substitutions: |The name is ${name}|
Arithmetic operations:
Binary operators: + , - , * , / , %
Minus sign (unary operator): -
Boolean operations:
Binary operators: and , or
Boolean negation (unary operator): ! , not
Comparisons and equality:（比较运算）
Comparators: > , < , >= , <= ( gt , lt , ge , le )
Equality operators: == , != ( eq , ne )
Conditional operators:
If-then: (if) ? (then)
If-then-else: (if) ? (then) : (else)
Default: (value) ?: (defaultvalue)
Special tokens:（特殊操作）
Page 17 of 106
No-Operation: _

```

**springMvc自动配置**

spring mvc auto-configuration

1. 自动配置了ViewResources（视图解析器：根据方法的返回值得到视图对象（view）,视图对象决定如何渲染（转发？重定义？））

2. ContentNegotiaingViewResovler:组合所有视图解析器

3. 如何定制：我们自己给容器定义一个视图解析器：自动的将组合进来

4. 自动注册了Converter Generic GenricConverter Formatter

   - converter 转换器；public String hello(User user) 类型转换使用Converter

   - Formatter 格式化器  2017.12.17---Date

   - HttpMessageConverters 只需要将自己的组件注册到容器中(@Bean,@component)  

   - 可以配置一个ConfigurableWebBindingInitializer来替换默认的：（添加到容器中）

     ```java
     初始化WebDataBinder
     请求数据=====javaBean
     
     ```
   
5. 扩展SpringMVC  
	@WebMvcConfigurationAdapter可以扩展SpringMVC的功能



​		全面接管SpringMVC:

@EnableWebMVC

##### 5.如何修改springboot默认配置
模式：
	1.spb自动配置时先看用户是否自己已配置@bean,@component







