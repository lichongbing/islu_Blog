---
title: JDBC
author: 闲花
img: "https://files.islu.cn/article/JDBC.png"
top: false
toc: true
mathjax: false
categories: Java
tags:
  - JDBC
  - JDBC数据库驱动加载过程
keywords: Hexo
essay: false
summary: JDBC数据库驱动加载过程(MySQL)
abbrlink: 23591
date: 2021-03-24 12:57:52
update: 2021-03-24 12:57:52
---

# JDBC

## 通过 JDBC 连接 MySQL 数据库

#### 前提条件

```
1、jar包：连接驱动包 【mysql-connector-java-5.1.47.jar】

2、url：确定连接的数据库所在网络地址和对应操作哪一个数据库，由协议名+子协议名+数据源名构成，即
        jdbc:mysql://主机地址:端口号/数据库名

        【例】jdbc:mysql://localhost:3306/islu

3、user：用户名 【root】

4、password：密码 【root】
```

#### 步骤

```
1、加载驱动
2、准备必要的连接参数
3、获取数据库连接
4、关闭资源！！！
```

#### 案例代码【测试连接】

```java
package JDBC;

import java.sql.Connection;
import java.sql.DriverManager;
import java.sql.SQLException;

public class Demo1 {
    /**
     * 1、加载驱动
     * 2、准备必要的连接参数
     * 3、获取数据库连接
     * 4、关闭资源！！！
     */
    public static void main(String[] args) {

        Connection connection = null;
        //加载驱动
        try {
            Class.forName("com.mysql.jdbc.Driver");
            //准备必要的连接参数
            //声明连接数据库所需要的参数，包括但不限于IP地址、端口号、连接到哪个数据库以及相关参数、用户名、密码
            String url = "jdbc:mysql://localhost:3306/islu?useSSL=true&characterEncoding=utf8";
            String user = "root";
            String password = "root";
            connection = DriverManager.getConnection(url, user, password);
            System.out.println(connection);
        } catch (ClassNotFoundException | SQLException e) {
            e.printStackTrace();
        } finally {
            try {
                connection.close();
            } catch (SQLException e) {
                e.printStackTrace();
            }
        }
    }

}
```

> 【注意】连接数据库可以配置一些相关的参数，数据库名与参数之间用 [?](file:///C:/Users/islu/Desktop/ialoe.github.io-master/posts/46.html) 进行分隔，参数之间通过 [&](file:///C:/Users/islu/Desktop/ialoe.github.io-master/posts/46.html) 分隔，常用参数及格式如下

| 参数                         | 描述                                                                                                       |
| ---------------------------- | ---------------------------------------------------------------------------------------------------------- |
| characterEncoding=utf8       | 设置字符集为 UTF8                                                                                          |
| serverTimezone=Asia/Shanghai | 设置时区[（JDBC8.0 以上必备）](file:///C:/Users/islu/Desktop/ialoe.github.io-master/posts/46.html)         |
| useSSL=true                  | 使用 SSL[（JDBC8.0 以上要改为 false）](file:///C:/Users/islu/Desktop/ialoe.github.io-master/posts/46.html) |

```java
jdbc:mysql://localhost:3306/FC2020?useSSL=true&characterEncoding=utf8&serverTimezone=Asia/Shanghai
```

## 数据库驱动加载过程

```java
public class Driver extends NonRegisteringDriver implements java.sql.Driver {
    /*
     * Register ourselves with the DriverManager
     * 在.class文件加载到内存时运行，并且有且只执行一次
     * 代码初始化过程！！！
     */
    static {
        try {
            // DriverManager驱动管理器注册了当前com.mysql.jdbc.Driver
            // 相对于当前Java程序拥有了连接MySQL数据库的必要的驱动条件
            java.sql.DriverManager.registerDriver(new Driver());
        } catch (SQLException E) {
            throw new RuntimeException("Can't register driver!");
        }
    }

    /**
     * Construct a new driver and register it with DriverManager
     *
     * @throws SQLException
     *             if a database error occurs.
     */
    public Driver() throws SQLException {
        // Required for Class.forName().newInstance()
    }
}
```

> 【注意】后续会用到静态代码块去完成一些初始化的操作

### JDBC 核心 API

```java
// 驱动管理类
class java.sql.DriverManager

/*
 * 这里是根据数据库连接URL，对应的user用户名和password密码，获取数据库连接对象
 */
static java.sql.Connection getConnection(String url, String user, String password);

// 数据库连接接口
interface java.sql.Connection

/*
 * 获取数据库SQL语句搬运工对象，从Java程序搬运SQL语句到数据库中，同时Statement也是一个资源对象。
 */
java.sql.Statement createStatement();

/*
 * 获取数据库SQL语句【预处理】搬运工对象，Java程序的SQL语句，在创建PreparedStatement对象时，将SQL语句交给数据库预处理操作，可以解决一定的【SQL语句注入问题】，同时提高一定的效率，PreparedStatement也是一个资源对象
 */
java.sql.PreparedStatement prepareStatement(String sql);

// 数据库SQL语句搬运工对象接口
interface java.sql.Statement

/*
 * 执行数据库修改数据，insert,update,delete...，返回值类型是int类型，是当前SQL语句搬运到数据库执行之后，数据库运行对于当前操作受到影响的行数
 * 2 rows affected in 5 ms
 */
int executeUpdate(String sql);

/*
 * 执行数据库查询语句，select操作，执行的结果是一个java.sql.ResultSet，结果集对象，当前操作返回值never null
 */
java.sql.ResultSet executeQuery(String sql);

// 数据库SQL语句【预处理】搬运工对象接口
public interface java.sql.PreparedStatement extends java.sql.Statement

/*
 * 执行数据库修改操作，insert，update，delete...处理的SQL语句是在创建PreparedStatement对象过程预处理的SQL语句，并且返回值是int类型，为当前操作对于数据表中收到影响的行数
 */
int executeUpdate();

/*
 * 执行数据库查询语句，select操作，的SQL语句是在创建PreparedStatement对象过程预处理的SQL语句，执行的结果是一个java.sql.ResultSet，结果集对象，当前操作返回值never null
 */
java.sql.ResultSet executeQuery();

/*
 * PreparedStatement预处理的SQL语句是可以带有参数的，这里是对于SQL语句参数进行赋值操作，这里有指定的操作下标，和对应的数据，数据类型繁多
 */
setXXX(int index, XXX value)

// 数据库结果集接口
interface java.sql.ResultSet

/*
 * 根据查询结果中，字段所处的位置下标获取对应数据，XXX是指定类型(int、String用的最多)
 */
XXX getXXX(int columnIndex);

/*
 * 根据查询结果中，字段所处的字段名获取对应数据，XXX是指定类型(int、String用的最多)
 * 例int getInt(String columnLabel)
 */
XXX getXXX(String columnLabel);

/*
 * 判断当前查询结果集中是否还有数据可以继续遍历，如果没有。或则当前结果集中是无数据情况 Empty Set，直接返回fasle
 */
boolean next();
```

### Statement 操作 SQL 语句

#### 增删改操作步骤【重点】

```
1、加载驱动
2、准备连接数据库所需要的参数
3、获取数据库连接
4、获取Statement搬运工对象
5、准备SQL语句
6、执行SQL语句获取受影响的行数
```

#### Statement 插入 SQL 数据操作

```java
package JDBC;

import java.sql.Connection;
import java.sql.DriverManager;
import java.sql.SQLException;
import java.sql.Statement;

public class Demo2 {
    /**
     * 1、加载驱动
     * 2、准备连接数据库所需要的参数
     * 3、获取数据库连接
     * 4、获取Statement搬运工对象
     * 5、准备SQL语句
     * 6、执行SQL语句获取受影响的行数
     */
    public static void main(String[] args) {
        Connection connection = null;
        Statement statement = null;
        //加载驱动
        try {
            Class.forName("com.mysql.jdbc.Driver");
            //准备连接所需参数
            String url = "jdbc:mysql://localhost:3306/islu?useSSL=true&characterEncoding=utf8";
            String user = "root";
            String password = "root";
            //获取数据库连接
            connection = DriverManager.getConnection(url, user, password);
            // 获取Statement对象
            statement = connection.createStatement();
            //准备SQL语句
            String sql = "insert into user(uname,upassword) values('islu','islu.cn');";
            //执行SQL语句
            int affectedRows = statement.executeUpdate(sql);
            System.out.println("受影响的行数" + affectedRows);
        } catch (ClassNotFoundException | SQLException e) {
            e.printStackTrace();
        } finally {
            try {
                if (statement != null) {
                    statement.close();
                }
                if (connection != null) {
                    connection.close();
                }
            } catch (SQLException e) {
                e.printStackTrace();
            }
        }
    }
}
```

#### Statement 修改 SQL 数据操作

```java
package JDBC;

import java.sql.Connection;
import java.sql.DriverManager;
import java.sql.SQLException;
import java.sql.Statement;

public class Demo3 {
    /**
     * 1、加载驱动
     * 2、准备连接数据库所需要的参数
     * 3、获取数据库连接
     * 4、获取Statement搬运工对象
     * 5、准备SQL语句
     * 6、执行SQL语句获取受影响的行数
     */
    public static void main(String[] args) {
        Connection connection=null;
        Statement statement=null;
        //加载驱动
        try {
            Class.forName("com.mysql.jdbc.Driver");
            //获取连接数据库所需要的参数
            String url="jdbc:mysql://localhost:3306/islu?useSSL=true&characterEncoding=utf8";
            String user="root";
            String password="root";
            //获取数据库连接
            connection = DriverManager.getConnection(url, user, password);
            //获取Statement搬运工对象
            statement = connection.createStatement();
            //准备SQL语句
            String sql="update user set uname = '彭于晏' where uid = 1;";
            //执行SQL语句
            int affectedRows = statement.executeUpdate(sql);
            System.out.println(affectedRows);
        } catch (ClassNotFoundException| SQLException e) {
            e.printStackTrace();
        }finally {
            try {
                if (connection!=null){
                connection.close();
                }
                if (statement!=null){
                    statement.close();
                }
            } catch (SQLException e) {
                e.printStackTrace();
            }
        }
    }
}
```

#### Statement 删除 SQL 数据操作

```java
public class Demo4 {
    public static void main(String[] args) {
        Connection connection = null;
        Statement statement = null;

        try {
            // 加载驱动
            Class.forName("com.mysql.jdbc.Driver");

            // 声明连接数据库所需要的参数，包括但不限于IP地址、端口号、连接到哪个数据库、用户名、密码
            String url = "jdbc:mysql://localhost:3306/FC2020?useSSL=true&characterEncoding=utf8";
            String user = "root";
            String password = "root";

            // 通过参数获取数据库连接
            connection = DriverManager.getConnection(url, user, password);

            // 获取Statement对象
            statement = connection.createStatement();

            // 准备SQL语句
            String sql = "delete from student where id = 1;";

            // 执行SQL语句获取受影响的行数
            int affectedRows = statement.executeUpdate(sql);

            System.out.println("受影响的行数：" + affectedRows);
        } catch (ClassNotFoundException | SQLException e) {
            e.printStackTrace();
        } finally {
            // 关闭资源
            try {
                if (statement != null) {
                    statement.close();
                }

                if (connection != null) {
                    connection.close();
                }
            } catch (SQLException e) {
                e.printStackTrace();
            }
        }
    }
}
```

#### 查询操作步骤【重点】

```
1、加载驱动
2、准备连接数据库所需要的参数
3、获取数据库连接
4、获取Statement搬运工对象
5、准备SQL语句
6、执行SQL语句获取结果集对象
7、判断结果集对象中是否有数据
8、如果结果集对象中存在数据，获取每个数据库字段对应类型的数据
```

#### Statement 查询 SQL 数据操作

准备实体类

```java
package bean;

public class User {
    private int uid;
    private String uname;
    private String upassword;

    public User() {
    }

    public User(int uid, String uname, String upassword) {
        this.uid = uid;
        this.uname = uname;
        this.upassword = upassword;
    }

    public int getUid() {
        return uid;
    }

    public void setUid(int uid) {
        this.uid = uid;
    }

    public String getUname() {
        return uname;
    }

    public void setUname(String uname) {
        this.uname = uname;
    }

    public String getUpassword() {
        return upassword;
    }

    public void setUpassword(String upassword) {
        this.upassword = upassword;
    }

    @Override
    public String toString() {
        return "User{" +
                "uid=" + uid +
                ", uname='" + uname + '\'' +
                ", upassword='" + upassword + '\'' +
                '}';
    }
}
```

> 【注意】根据阿里巴巴开发手册，实体类成员变量要用包装类！！！

##### 查询单行

```java
package JDBC;

import bean.User;

import java.sql.*;

public class Demo5 {
    public static void main(String[] args) {

        // 声明资源
        Connection connection = null;
        Statement statement = null;
        ResultSet resultSet = null;

        try {
            // 加载驱动
            Class.forName("com.mysql.jdbc.Driver");

            // 准备参数
            String url = "jdbc:mysql://localhost:3306/islu?useSSL=true&characterEncoding=UTF8";
            String user = "root";
            String password = "root";

            // 获取连接
            connection = DriverManager.getConnection(url, user, password);

            // 获取搬运工对象
            statement = connection.createStatement();

            // 准备SQL语句
            String sql = "select * from user where uid = 1;";

            // 执行SQL语句并获取结果集
            resultSet = statement.executeQuery(sql);

            User userinfo = null;

            // 判断结果集中是否还有下一行数据
            while (resultSet.next()) {
                // 从结果集中获取对应类型的数据
                int uid = resultSet.getInt(1);
                String uname = resultSet.getString(2);
                String upassword = resultSet.getString(3);

                // 通过获取到的数据创建实体类对象
                userinfo = new User(uid, uname, upassword);
            }

            // 展示
            System.out.println(userinfo);

        } catch (SQLException | ClassNotFoundException e) {
            e.printStackTrace();
        } finally {
            // 关闭资源
            try {
                if (resultSet != null) {
                    resultSet.close();
                }

                if (statement != null) {
                    statement.close();
                }

                if (connection != null) {
                    connection.close();
                }
            } catch (SQLException e) {
                e.printStackTrace();
            }
        }
    }
}
```

##### 查询多行

```java
package JDBC;

import bean.User;

import java.sql.*;
import java.util.ArrayList;

public class Demo6 {
    public static void main(String[] args) {

        // 声明资源
        Connection connection = null;
        Statement statement = null;
        ResultSet resultSet = null;

        try {
            // 加载驱动
            Class.forName("com.mysql.jdbc.Driver");

            // 准备参数
            String url = "jdbc:mysql://localhost:3306/islu?useSSL=true&characterEncoding=UTF8";
            String user = "root";
            String password = "luhuijun";

            // 获取连接
            connection = DriverManager.getConnection(url, user, password);

            // 获取搬运工对象
            statement = connection.createStatement();

            // 准备SQL语句
            String sql = "select * from user;";

            // 执行SQL语句并获取结果集
            resultSet = statement.executeQuery(sql);

            User userinfo = null;
            ArrayList<User> list=new ArrayList<>();
            // 判断结果集中是否还有下一行数据
            while (resultSet.next()) {
                // 从结果集中获取对应类型的数据
                int uid = resultSet.getInt(1);
                String uname = resultSet.getString(2);
                String upassword = resultSet.getString(3);

                // 通过获取到的数据创建实体类对象
                userinfo = new User(uid, uname, upassword);
                //添加到list集合中
                list.add(userinfo);
            }

            // 展示
            System.out.println(list);

        } catch (SQLException | ClassNotFoundException e) {
            e.printStackTrace();
        } finally {
            // 关闭资源
            try {
                if (resultSet != null) {
                    resultSet.close();
                }

                if (statement != null) {
                    statement.close();
                }

                if (connection != null) {
                    connection.close();
                }
            } catch (SQLException e) {
                e.printStackTrace();
            }
        }
    }
}
```

### 常见数据库连接

```shell
-------------------------------oracle------------------
驱动：oracle.jdbc.driver.OracleDriver
URL：jdbc:oracle:thin:@machine_name:port:dbname
注：machine_name：数据库所在的机器的名称；
      port：端口号，默认是1521

-------------------------------mysql-------------------
驱动：com.mysql.jdbc.Driver
URL：jdbc:mysql://machine_name:port/dbname
注：machine_name：数据库所在的机器的名称；
      port：端口号，默认3306

------------------------------SQL Server---------------
驱动：com.microsoft.jdbc.sqlserver.SQLServerDriver
URL：jdbc:microsoft:sqlserver://<:port>;DatabaseName=
注：machine_name：数据库所在的机器的名称；
      port：端口号，默认是1433

------------------------------DB2----------------------
驱动：com.ibm.db2.jdbc.app.DB2Driver
URL：jdbc:db2://<:port>/dbname
注：machine_name：数据库所在的机器的名称；
      port：端口号，默认是5000
-------------------------------------------------------
```
