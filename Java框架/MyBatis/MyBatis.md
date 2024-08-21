# MyBatis

## 目录

- [1、Mybatis中#和\$的区别？](#1Mybatis中和的区别)
- [2、Mybatis的编程步骤是什么样的？](#2Mybatis的编程步骤是什么样的)
- [3、JDBC编程有哪些不足之处，MyBatis是如何解决这些问题的？](#3JDBC编程有哪些不足之处MyBatis是如何解决这些问题的)
- [4、使用MyBatis的mapper接口调用时有哪些要求？](#4使用MyBatis的mapper接口调用时有哪些要求)
- [5、Mybatis中一级缓存与二级缓存？](#5Mybatis中一级缓存与二级缓存)
- [6、MyBatis在insert插入操作时如何返回主键ID？](#6MyBatis在insert插入操作时如何返回主键ID)
- [7、简述 Mybatis 的插件运行原理，如何编写一个插件](#7简述-Mybatis-的插件运行原理如何编写一个插件)

## 1、Mybatis中#和\$的区别？

在MyBatis中，`#`和`$`是两种不同的参数占位符使用方式。

1. `#`占位符：`#`占位符是使用预编译的方式进行参数传递。在SQL语句中，使用`#`可以将参数值安全地替换到SQL语句中，并自动进行参数类型转换和防止SQL注入攻击。使用`#`占位符时，MyBatis会将参数值作为一个整体传递给数据库，因此可以有效地防止SQL注入问题。

   例如：

   `SELECT * FROM users WHERE id = #{userId}`&#x20;

   在上述示例中，`#{userId}`会被替换为具体的参数值，并且会根据参数类型进行合适的转换。
2. `$`占位符：`$`占位符是使用字符串拼接的方式进行参数传递。在SQL语句中，使用`$`可以将参数值直接拼接到SQL语句中，不进行预编译和参数类型转换。使用`$`占位符时，需要注意潜在的安全风险，因为参数值直接拼接到SQL语句中，可能会导致SQL注入攻击。

   例如：

   `SELECT * FROM users WHERE id = ${userId}`&#x20;

   在上述示例中，`${userId}`会被替换为具体的参数值，但不会进行参数类型转换和安全检查。

总结：

- 使用`#`占位符可以提供更安全和可靠的参数传递方式，适用于大多数情况。
- 使用`$`占位符可以提供更灵活的参数传递方式，但需要注意安全性和潜在的SQL注入问题。

在选择使用`#`还是`$`时，需要根据具体的需求和安全考虑来决定。一般来说，推荐使用`#`占位符，除非有特殊的需求需要使用`$`占位符。

## 2、Mybatis的编程步骤是什么样的？

● 创建SqlSessionFactory

● 通过SqlSessionFactory创建SqlSession

● 通过sqlsession执行数据库操作

● 调用session.commit()提交事务

● 调用session.close()关闭会话

## 3、JDBC编程有哪些不足之处，MyBatis是如何解决这些问题的？

JDBC编程在某些方面存在一些不足之处，而MyBatis通过提供一种更高级的抽象层来解决这些问题。以下是JDBC编程的一些不足之处以及MyBatis是如何解决这些问题的：

1. **繁琐的代码**：JDBC编程需要编写大量的重复代码，包括连接数据库、创建和释放资源、处理结果集等。这使得代码冗长、难以维护和理解。
   - MyBatis通过提供一个简洁的配置文件和映射文件，将数据库操作的细节抽象出来，使得开发者只需关注SQL语句和参数映射，大大减少了繁琐的代码量。
2. **SQL与Java代码的耦合**：在JDBC编程中，SQL语句通常直接嵌入在Java代码中，导致SQL与Java代码紧密耦合，不易于维护和修改。
   - MyBatis使用了面向SQL的思想，将SQL语句与Java代码分离，通过映射文件将SQL语句与Java对象进行映射，使得SQL与Java代码解耦，提高了代码的可维护性和可读性。
3. **手动参数设置和结果集处理**：在JDBC编程中，需要手动设置参数并处理结果集，包括类型转换、结果集遍历等，增加了开发的工作量和出错的可能性。
   - MyBatis通过提供参数映射和结果集映射的功能，自动处理参数设置和结果集转换，开发者只需定义映射关系，MyBatis会自动完成参数设置和结果集处理，简化了开发过程。
4. **缺乏对象关系映射（ORM）支持**：JDBC编程需要手动将数据库查询结果映射到Java对象中，缺乏对对象关系映射的支持，增加了开发的复杂性。
   - MyBatis提供了强大的对象关系映射（ORM）功能，可以将查询结果自动映射到Java对象中，支持一对一、一对多、多对一等复杂的关系映射，简化了数据操作的过程。
5. **缺乏缓存支持**：JDBC编程没有内置的缓存机制，每次查询都需要访问数据库，降低了性能。
   - MyBatis提供了一级缓存和二级缓存的支持。一级缓存是在同一个会话中的缓存，可以减少对数据库的访问；二级缓存是在多个会话中的缓存，可以共享缓存结果，提高了查询性能。

总的来说，MyBatis通过提供简洁的配置和映射文件、解耦SQL与Java代码、自动处理参数和结果集、支持对象关系映射和缓存等功能，弥补了JDBC编程的不足之处，提供了更便捷、高效和可维护的数据库访问解决方案。

## 4、使用MyBatis的mapper接口调用时有哪些要求？

● Mapper接口方法名和mapper.xml中定义的每个sql的id相同

● Mapper接口方法的输入参数类型和mapper.xml中定义的每个sql的parameterType的类型相同

● Mapper接口方法的输出参数类型和mapper.xml中定义的每个sql的resultType的类型相同

● Mapper.xml文件中的namespace即是mapper接口的类路径。

## 5、Mybatis中一级缓存与二级缓存？

在 MyBatis 中，存在一级缓存和二级缓存两种缓存机制。

1. 一级缓存：
   - 一级缓存是 MyBatis 默认开启的缓存机制，也被称为本地缓存。
   - 一级缓存的作用范围是在同一个 SqlSession 内部，即在同一个会话期间，多次执行相同的查询语句，第一次查询结果会被缓存到一级缓存中，后续的查询会直接从缓存中获取结果，而不再去查询数据库。
   - 一级缓存是基于对象引用的方式实现的，因此在同一个会话期间，如果对查询结果进行了修改（例如更新、插入、删除等操作），则会清空一级缓存，以保证数据的一致性。
2. 二级缓存：
   - 二级缓存是 MyBatis 的全局缓存机制，作用范围是在同一个 Mapper 的 namespace 中，即多个 SqlSession 共享同一个 Mapper 的缓存。
   - 二级缓存可以跨越多个会话，当多个会话执行相同的查询语句时，第一个会话的查询结果会被缓存到二级缓存中，后续的会话可以直接从缓存中获取结果，而不再去查询数据库。
   - 二级缓存是基于序列化的方式实现的，因此要求缓存的对象必须是可序列化的。
   - 默认情况下，二级缓存是关闭的，需要在 Mapper 的配置文件中显式配置开启。

需要注意的是：

- 一级缓存和二级缓存是独立的，互不影响。
- 二级缓存是可选的，可以根据需要选择是否开启。
- 二级缓存的使用需要注意数据的一致性和并发访问的问题，特别是在多线程环境下。

总结： &#x20;
一级缓存是在同一个会话期间的缓存，而二级缓存是在同一个 Mapper 的命名空间中的缓存。一级缓存是默认开启的，二级缓存是可选的。在实际应用中，可以根据需求选择合适的缓存机制来提高查询性能。

## 6、MyBatis在insert插入操作时如何返回主键ID？

在 MyBatis 中，可以通过以下几种方式来获取插入操作后生成的主键 ID：

1. 使用数据库的自增主键：
   - 如果你的表使用了数据库的自增主键（如 MySQL 的 AUTO\_INCREMENT），则在执行插入操作后，可以通过 `SELECT LAST_INSERT_ID()` 来获取最后插入的主键 ID。
   - 在 MyBatis 的映射文件（Mapper XML）中，可以使用 `<selectKey>` 元素来配置获取主键的语句，例如：
   ```纯文本
   <insert id="insertUser" parameterType="User">
     <selectKey keyProperty="id" resultType="Long" order="AFTER">
       SELECT LAST_INSERT_ID()
     </selectKey>
     INSERT INTO user (username, password) VALUES (#{username}, #{password})
   </insert>
   ```
   - 在执行插入操作后，MyBatis 会自动执行 `<selectKey>` 中配置的语句，并将获取到的主键值设置到对应的属性（`keyProperty`）中。
2. 使用数据库的序列（Sequence）：
   - 如果你的表使用了数据库的序列（如 Oracle 的序列），则可以通过调用序列的 `NEXTVAL` 函数来获取下一个序列值作为主键 ID。
   - 在 MyBatis 的映射文件中，可以使用 `<selectKey>` 元素来配置获取序列值的语句，例如：
   ```纯文本
   <insert id="insertUser" parameterType="User">
     <selectKey keyProperty="id" resultType="Long" order="BEFORE">
       SELECT user_seq.NEXTVAL FROM DUAL
     </selectKey>
     INSERT INTO user (id, username, password) VALUES (#{id}, #{username}, #{password})
   </insert>
   ```
   - 在执行插入操作前，MyBatis 会先执行 `<selectKey>` 中配置的语句，并将获取到的序列值设置到对应的属性（`keyProperty`）中。
3. 使用数据库的触发器（Trigger）：
   - 如果你的表使用了数据库的触发器，在触发器中可以获取插入操作后生成的主键 ID，并将其设置到对应的列中。
   - 在 MyBatis 中，执行插入操作后，可以通过查询插入的记录来获取主键 ID，例如：
   ```纯文本
   // 执行插入操作
   sqlSession.insert("insertUser", user);

   // 获取插入后的主键 ID
   Long id = user.getId();
   ```

根据你所使用的数据库和表的配置，选择适合的方式来获取插入操作后的主键 ID。

## 7、简述 Mybatis 的插件运行原理，如何编写一个插件

答： Mybatis 只支持针对 ParameterHandler、ResultSetHandler、StatementHandler、Executor 这4 种接口的插件， Mybatis 使用 JDK 的动态代理， 为需要拦截的接口生成代理对象以实现接口方法拦截功能， 每当执行这 4 种接口对象的方法时，就会进入拦截方法，具体就是 InvocationHandler 的invoke() 方法， 拦截那些你指定需要拦截的方法。

编写插件： 实现 Mybatis 的 Interceptor 接口并复写 intercept()方法， 然后在给插件编写注解， 指定
要拦截哪一个接口的哪些方法即可， 在配置文件中配置编写的插件。

```java
@Intercepts({@Signature(type = StatementHandler.class, method = "query", args =
{Statement.class, ResultHandler.class}),
@Signature(type = StatementHandler.class, method = "update", args =
{Statement.class}),
@Signature(type = StatementHandler.class, method = "batch", args = {
Statement.class })})
@Component
invocation.proceed()执行具体的业务逻辑
```
