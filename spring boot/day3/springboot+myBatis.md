# Springoot + MyBatis的配置
周日过去了，算是MyBitis入了门，话不多说，开始记录一天的所学<br/>
中途看了纯洁的微笑大神的文章,也参考了自己的书，自己也就学会了一种配置，通过注解来配置，置于关于XML的配置，等后面再学。再这先记录一下这几天所学的。<br/>
一个完整的工程，首先是介绍一下文件的分布吧。  
初始化一个springboot 在resources下建立static用于存放js，css,images的资源
在包下建立mapper，dao,entity（实体）,controller,service（业务逻辑处理类）,config(关于factory配置文件),repository(定义数据访问包)...  
关于bean的配置，一般建立专门的factory类来初始化,在方法体上使用@Bean("这里是名称"),初始化的化使用@Autowired来注解

* 关于配置mybatis  
在pom.xml里添加
      <dependency>
          <groupId>org.mybatis.spring.boot</groupId>
          <artifactId>mybatis-spring-boot-starter</artifactId>
          <version>1.3.2</version>
      </dependency>

      <dependency>
          <groupId>mysql</groupId>
          <artifactId>mysql-connector-java</artifactId>
      </dependency>

      <dependency>
		   	  <groupId>org.springframework.boot</groupId>
			    <artifactId>spring-boot-starter-thymeleaf</artifactId>
		  </dependency>

在application.properties里添加
    #thymeleaf start
    spring.thymeleaf.prefix=classpath:/templates/
    spring.thymeleaf.suffix=.html
    spring.thymeleaf.mode=HTML5
    spring.thymeleaf.encoding=UTF-8
    spring.thymeleaf.servlet.content-type=text/html
    spring.thymeleaf.cache=false
    #thymeleaf end

    mybatis.type-aliases-package=com.example.ecxetest
    spring.datasource.driverClassName = com.mysql.jdbc.Driver
    spring.datasource.url = jdbc:mysql://localhost:3306/user?useUnicode=true&characterEncoding=utf-8
    spring.datasource.username = root
    spring.datasource.password = 159357

  * mapper的编写  
  创建mapper类
      public interface UserReponsitory{
        @Select("select * from user where id=#{id}")
        //引用id="userResult"的Result
        @ResultMap("userResult")
        public User findUserById(int id);
      }

这里应该是自动映射变量的。很赞。还有关于#{name}和@{name}的使用方法的区别。  

    / This example creates a prepared statement, something like select * from teacher where name = ?;
    @Select("Select * from teacher where name = #{name}")
    Teacher selectTeachForGivenName(@Param("name") String name);

    // This example creates n inlined statement, something like select * from teacher where name = 'someName';
    @Select("Select * from teacher where name = '${name}'")
    Teacher selectTeachForGivenName(@Param("name") String name);


* 关于mapper里@Results的基本用法 <br/>
  MyBatis中使用@Results注解来映射查询结果集到实体类属性。  
  (1)@Results的基本用法。当数据库字段名与实体类对应的属性名不一致时，可以使用@Results映射来将其对应起来。column为数据库字段名，porperty为实体类属性名，jdbcType为数据库字段数据类型，id为是否为主键。
这里主要是映射是是驼峰和下划线命名的方式。数据库一般是下划线命名。

    @Results(id = "userResult", value={
      @Result(id=true,column = "id",property = "id"),
      @Result(column="username" ,property="username"),
      @Result(column = "sex", property = "sex"),
      @Result(column = "birthday", property = "birthday"),
      @Result(column = "address", property = "address")
      })
      public List<User> findAll();

（2）@ResultMap的用法。当这段@Results代码需要在多个方法用到时，为了提高代码复用性，我们可以为这个@Results注解设置id，然后使用@ResultMap注解来复用这段代码。  
      @ResultMap("userResult")

（3）@One 和 @Many我还没有弄明白，后面遇到再学.
