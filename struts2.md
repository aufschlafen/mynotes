# struts2

## 一，概述

作用于javaee的web层框架上

struts2在strurts1和webwork基础上发展全新的框架

![1569230911973](C:\Users\wxj123\AppData\Roaming\Typora\typora-user-images\1569230911973.png)

web层常见框架：springMVC strurts2

## 二、入门

**MVC**:模型：主要负责数据维护；视图：负责向用户呈现全部或部分数据；控制器通过软件代码控制模型和视图之间的交互

**structsMVC**:![1569288544325](C:\Users\wxj123\AppData\Roaming\Typora\typora-user-images\1569288544325.png)

Actions,Interceptors,value stack/OGNL,Result,视图技术

### HelloWorld

```java
<%@ taglib prefix="s" uri="/struts-tags" %>//写在jsp开头
```

​	告知servlet这个容器将使用struts2,并且这些标签会被s放在前面。s:property 标签显示Action类“name”属性的值，这个值是使用HelloWorldAction类的 getName() 方法返回的。