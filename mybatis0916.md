### mybatis注解

*Mybatis教程IDEA版-4天-2018黑马SSM-01-p9*

1.把UserDao.xml移除，在dao接口上使用@Select注解，并且制定sql语句，同时需要在SqlMapConfig.xml的Mapper配置，使用class属性指定dao接口的全限定类名

在开发中都是不写dao实现类，但是mybatis中支持实现类

```java
  public static void main(String[] args) throws IOException {
        //1.读取配置文件
        InputStream in = Resources.getResourceAsStream("SqlMapConfig.xml");
  //使用类加载器，它只能读取类路径的配置文件
   //使用ServletContext对象的getRealPath()
        //2.创建SqlSessionFactory工厂
        SqlSessionFactoryBuilder builder = new SqlSessionFactoryBuilder();
        SqlSessionFactory factory = builder.build(in);
      //创建工厂mb使用了构建者模式（把对象的创建过程隐藏），builder就是构建者
        //3.使用工厂生产SqlSession对象
        SqlSession session = factory.openSession();//生产SqlSession使用了工厂模式（解耦）
        //4.使用SqlSession创建Dao接口的代理对象
        UserDao userDao = session.getMapper(UserDao.class);//创建代理模式（不修改源码基础上对已有方法的增强）
        //5.使用代理对象执行方法
        List<UserEntity> users = userDao.findAll();
        for(UserEntity user : users){
            System.out.println(user);
        }
        //6.释放资源
        session.close();
        in.close();
    }
```

###### 6.自定义mb的分析

mb在使用代理dao的方式实现crud做的事：

（1）创建代理对象

（2）在代理对象中调用selectList

![连接数据库，创建Connection对象](C:\Users\wxj123\AppData\Roaming\Typora\typora-user-images\1568603274740.png "")

![创建映射配置信息](C:\Users\wxj123\AppData\Roaming\Typora\typora-user-images\1568603334962.png)

![有了执行的sql语句，可以获取preparedStatement,还有封装的实体类全限定名](C:\Users\wxj123\AppData\Roaming\Typora\typora-user-images\1568603649655.png)

读取配置文件：用到的技术就是解析xml技术，此处使用的是的dom4j解析xml技术

---

（1）.根据配置文件的信息创建Connection对象，注册驱动，获取连接

（2）获取预处理对象PreparedStatement此时需要sql语句conn.prepareStatement(sql)

(3)执行查询 Resultset resultset = preparedStatement.executeQuery();

(4)遍历结果用于封装

```
List<E> list = new ArrrayList();
while(resultSet.next()){
	E element = (E)Class.forName(配置的全限定名).newInstance()
	进行封装，把每个rs的内容都添加到element中
	我们的实体类属性和表中的列名是一致的
	于是我们就可以把表的列名看成实体类的属性名称
	就可以使用反射的方式根据名称获取每个属性并把值扶进去
	吧element加入到list中
	list.add(element); 
}
```

---

**selectList()**:1.连接信息2.映射信息：（1）执行的sql语句（2）封装结果的实体类全限定类名（两个信息组合起来成一个对象）

| String     | Mapper                 |
| ---------- | ---------------------- |
| com.entity | Mapper对象             |
| com.dao    | String sql             |
| findAll    | String domainClassPath |

自定义mb能通过入门案例看到类

class Resources

class SqlSessionFactoryBuilder

interface SqlSessionFactory

## mb CRUD操作

select last_insert_id();//查询最后插入的id	

**新增用户id的返回值**

配置插入操作后，获取插入数据的id

```xml
 <!--保存用户-->
    <insert id="saveUser" parameterType="com.pmh.entity.UserEntity">
        <selectKey keyProperty="id" keyColumn="id" resultType="int" order="AFTER">
            select last_insert_id();
        </selectKey>
        insert into user(username,address,sex,birthday) values (#{username},#{address},#{sex},#{birthday});
    </insert>
```

#### **mb参数**

##### 1.parameterType

###### 2.简单类型

###### 3.pojo对象

mb中使用ognl表达式解析对象字段的值，${}或#{}括号里面的值为pojo属性的值

OGNL：对象图导航语言,他是通过对象的取值方法来获取数据，在写法上把get省略了

比如我们获取用户的名称：类的写法 user.getUsername();OGNL表达式:user.username

因为在parameterType中已经提供了属性所属的类，所以不需要提供对象名

###### 4.传递pojo包装对象

 开发中通过 pojo 传递查询条件 ，查询条件是综合的查询条件，不仅包括用户查询条件还包括其它的查询条件（比如将用户购买商品信息也作为查询条件），这时可以使用包装对象传递输入参数。 

Pojo 类中包含 pojo。 

需求：根据用户名查询用户信息，查询条件放到 QueryVo 的 user 属性中。

##### resultType

配置查询结果的列名和实体类的属性名的对应关系

```xml
<resultMap id="userMap" type="xxx.xxx.xxx">
<id property="userid" column="id"></id>
 <result property="username" column="username"></result>
</resultMap>
```

