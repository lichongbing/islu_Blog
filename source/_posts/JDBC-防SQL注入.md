---
title: JDBC-防SQL注入
author: 闲花
img: "https://files.islu.cn/article/JDBCSQLInjection"
top: false
toc: true
mathjax: false
categories: Java
tags:
  - JDBC
  - JDBC-防SQL注入
keywords: "JDBC,JDBC-防SQL注入,防SQL注入,PreparedStatement"
essay: false
summary: JDBC-防SQL注入(PreparedStatement)
abbrlink: 57350
date: 2021-03-24 13:08:19
update: 2021-03-24 13:08:19
---

# JDBC-防 SQL 注入

## SQL 注入

> SQL 注入是指 web 应用程序对用户输入数据的合法性没有判断或过滤不严，攻击者可以在 web 应用程序中事先定义好的查询语句的结尾上添加额外的 SQL   语句，在管理员不知情的情况下实现非法操作，以此来实现欺骗数据库服务器执行非授权的任意查询，从而进一步得到相应的数据信息，甚至篡改数据库

### 正确账户密码案例代码

```java
    // 使用正确的用户名和密码登录成功
    @Test
    public void testLogin() {
        String sql = "select * from account where username = '张三' and password = '123456';";

        ResultSet resultSet = JdbcUtils.executeQuery(sql);

        try {
            if (resultSet.next()) {
                System.out.println("登录成功");
            } else {
                System.out.println("登录失败");
            }
        } catch (SQLException e) {
            e.printStackTrace();
        } finally {
            JdbcUtils.close(resultSet);
        }
    }
```

### 错误账户密码案例代码

```java
// 通过SQL注入使用异常的密码登录成功
    @Test
    public void testSqlInject() {
        String sql = "select * from account where username = '张三' and (password = 'iglrne' or 1 = 1);";

        ResultSet resultSet = JdbcUtils.executeQuery(sql);

        try {
            if (resultSet.next()) {
                System.out.println("登录成功");
            } else {
                System.out.println("登录失败");
            }
        } catch (SQLException e) {
            e.printStackTrace();
        } finally {
            JdbcUtils.close(resultSet);
        }
    }
```

### 重点总结

> 【注意】Statement 存在 SQL 注入问题，而 PreparedStatement 可以有效的避免 SQL 注入！
>
> 以后只能使用 PreparedStatement ，因为操作性更强，并且安全性更高

## 通过 PreparedStatement 操作 SQL 语句

PreparedStatement 实例包含已编译的 SQL 语句。这就是使语句“准备好”。包含于 PreparedStatement 对象中的 SQL 语句可具有一个或多个  IN 参数。IN 参数的值在 SQL 语句创建时未被指定。相反的，该语句为每个 IN 参数保留一个问号（“？”）作为[占位符](https://baike.baidu.com/item/%E5%8D%A0%E4%BD%8D%E7%AC%A6)。每个问号的值必须在该语句执行之前，通过适当的 setXXX 方法来提供。

由于 PreparedStatement 对象已[预编译](https://baike.baidu.com/item/%E9%A2%84%E7%BC%96%E8%AF%91)过，所以其执行速度要快于 Statement 对象。因此，多次执行的 SQL 语句经常创建为 PreparedStatement 对象，以提高效率。

作为 Statement 的子类，PreparedStatement 继承了 Statement 的所有功能。另外它还添加了一整套方法，用于设置发送给数据库以取代 IN 参数[占位符](https://baike.baidu.com/item/%E5%8D%A0%E4%BD%8D%E7%AC%A6)的值。同时，三种方法 execute、 executeQuery 和 executeUpdate 已被更改以使之不再需要参数。这些方法的 Statement 形式（接受 SQL 语句参数的形式）不应该用于 PreparedStatement 对象。

> 【注意】应该始终以 PreparedStatement 代替 Statement，也就是说，在任何时候都不要使用 Statement。

### PreparedStatement 查询操作

```java
@Test
    public void testPreparedStatement() {
        // 获取数据库连接
        Connection connection = JdbcUtils.getConnection();

        // 提取资源
        PreparedStatement preparedStatement = null;
        ResultSet resultSet = null;

        // 准备SQL语句，? 是占位符
        String sql = "select * from account where username = ? and password = ?;";

        try {
            // 获取预处理搬运工对象，并对SQL语句进行预处理
            preparedStatement = connection.prepareStatement(sql);

            // 设置参数
            preparedStatement.setObject(1, "张三");
            preparedStatement.setObject(2, "123456");

            // 执行SQL语句
            resultSet = preparedStatement.executeQuery();

            // 判断是否还有数据
            if (resultSet.next()) {
                System.out.println("登录成功");
            } else {
                System.out.println("登录失败");
            }

        } catch (SQLException e) {
            e.printStackTrace();
        } finally {
            // 关闭资源
            JdbcUtils.close(resultSet, preparedStatement, connection);
        }
    }
```

### PreparedStatement 增加操作

```java
 @Test
    public void testInsert() {
        // 准备SQL语句
        String sql = "insert into student(name, age, gender, info) values(?, ?, ?, ?)";

        // 获取连接
        Connection connection = JdbcUtils.getConnection();

        PreparedStatement preparedStatement = null;

        try {
            // 获取预处理对象
            preparedStatement = connection.prepareStatement(sql);

            // 设置参数
            preparedStatement.setObject(1, "赵四");
            preparedStatement.setObject(2, 17);
            preparedStatement.setObject(3, "男");
            preparedStatement.setObject(4, "你愁啥");

            // 执行SQL语句
            int affectedRows = preparedStatement.executeUpdate();

            System.out.println("受影响的行数：" + affectedRows);
        } catch (SQLException e) {
            e.printStackTrace();
        } finally {
            // 关闭资源
            JdbcUtils.close(preparedStatement, connection);
        }
    }
```

### PreparedStatement 修改操作

```java
 @Test
    public void testUpdate() {
        // 准备SQL语句
        String sql = "update student set age = ? where id = ?";

        // 获取连接
        Connection connection = JdbcUtils.getConnection();

        PreparedStatement preparedStatement = null;

        try {
            // 获取预处理对象
            preparedStatement = connection.prepareStatement(sql);

            // 设置参数
            preparedStatement.setObject(1, 61);
            preparedStatement.setObject(2, 6);

            // 执行SQL语句
            int affectedRows = preparedStatement.executeUpdate();

            System.out.println("受影响的行数：" + affectedRows);
        } catch (SQLException e) {
            e.printStackTrace();
        } finally {
            // 关闭资源
            JdbcUtils.close(preparedStatement, connection);
        }
    }
```

### PreparedStatement 删除操作

```java
@Test
    public void testDelete() {
        // 准备SQL语句
        String sql = "delete from student where id = ?";

        // 获取连接
        Connection connection = JdbcUtils.getConnection();

        PreparedStatement preparedStatement = null;

        try {
            // 获取预处理对象
            preparedStatement = connection.prepareStatement(sql);

            // 设置参数
            preparedStatement.setObject(1, 3);

            // 执行SQL语句
            int affectedRows = preparedStatement.executeUpdate();

            System.out.println("受影响的行数：" + affectedRows);
        } catch (SQLException e) {
            e.printStackTrace();
        } finally {
            // 关闭资源
            JdbcUtils.close(preparedStatement, connection);
        }
    }
```
