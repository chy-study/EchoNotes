---
title: 周末培训
date: 2020-08-09 22:03:31
categories:
- 生活
tags: 
- study
---

2020年8月9号周日，公司组织第一次培训
<!-- more -->

## 第一次培训

### 异常处理

```
try{
	需要监控的可能会抛出异常的代码块
}
catch(Exception e){
	出现异常后的处理代码
}
finally{
	回收资源的动作
}
```

1. finally{} 里放内存回收相关的代码
2. 在子类方法里不该抛出比父类范围更广的异常
3. try{} 里面包含可能抛出异常的代码,尽量减少用try监控的代码块
4. catch(){} 用专业的异常来处理，最后再用Exception异常来兜底

	```
	try{
		IO代码
		数据库连接代码
	}
	catch(IOException ioe){处理IO异常的代码}
	catch(SQLException ioe){处理数据库操作异常的代码}、
	catch(Exception ioe){最后再用Exception这个异常基类}
	```

5. 在catch从句里，别简单地抛出异常了事，应当尽可能地处理异常。

### 看慢SQL

1. Linux命令，MySql命令，看long SQL
2. 监控CAT，Zabbix

### 数据库调优
1. 索引
2. 缓存，redis
3. MySql集群，主从，读写分离，LVS，负载均衡
4. MyCAT分库分表

### JDBC连接数据库

```
public class JDBCRead {
    public static void main(String[] args) {
        try {
            // 加载数据库驱动
            Class.forName("com.mysql.jdbc.Driver");
        } catch (ClassNotFoundException e) {
            System.out.println("加载数据库驱动失败");
            e.printStackTrace();
        }
        Connection connection = null;
        Statement stmt = null;
        try {
            // 创建连接
            connection = DriverManager.getConnection("jdbc:mysql://localhost:3306/test","root","123456");
            if (connection != null) {
                // 通过Statement对象执行select语句
                stmt = connection.createStatement();
                String query = "select id, username, password from t_user";
                // 通过ResultSet对象得到查询的结果
                ResultSet rs = stmt.executeQuery(query);
                // 通过rs.next()方法遍历查询结果
                while (rs.next()) {
                    System.out.println("id = " + rs.getInt("id"));
                    System.out.println("username = " + rs.getString("username"));
                    System.out.println("password = " + rs.getString("password"));
                }
            } else {
                System.out.println("连接数据库失败");
            }
        } catch (SQLException e) {
            System.out.println("数据库连接抛出异常");
            e.printStackTrace();
        } finally {
            System.out.println("数据库连接关闭");
            try {
                connection.close();
                stmt.close();
            } catch (SQLException e) {
                e.printStackTrace();
            }
        }
    }
}
```

### 读取 .properties文件

	
```
public class PropertiesRead {
    public static void main(String[] args) {
        String fileName;
        if (args != null || args.length == 1) {
            fileName = args[0] + ".properties";
        } else {
            fileName = "sql.properties";
        }

        String driver = null;
        String url = null;
        String username = null;
        String password = null;
        Properties prop = new Properties();
        InputStream in = null;
        try {
            // 读取配置文件
            URL url1 = PropertiesRead.class.getClassLoader().getResource(fileName);
            String path = url1.getFile();
            in = new BufferedInputStream(new FileInputStream(path));
            prop.load(in);
            // 读JDBC连接参数
            driver = prop.getProperty("mysql.Driver");
            url = prop.getProperty("mysql.url");
            username = prop.getProperty("mysql.username");
            password = prop.getProperty("mysql.pwd");
        } catch (IOException e) {
            e.printStackTrace();
        } finally {
            if (in != null) {
                try {
                    in.close();
                } catch (IOException e) {
                    e.printStackTrace();
                }
            }
            prop.clear();
        }
        System.out.println("driver : "+driver);
        System.out.println("url : "+url);
        System.out.println("username : "+username);
        System.out.println("password : "+password);
    }
}
```

### 虚拟机体系结构和Java跨平台特性

