---
title: Java反射在数据访问中的应用
date: 2018-05-21 17:21:56
tags: [Java SE]
---

## Java 反射在数据访问中的应用

### 问题：

  在做一个系统的过程中，难免会遇到一个系统要有不只一套数据库管理系统的情况。

然而对于这种情况，我们总不可能去做两套系统，所有，Java反射给我们带来了很大的便利。

 ### 代码：

  比如这有一个例子： 

​    一套系统，要支持两套数据库：mysql、oracle

~~~
//db.properties

#dbName = MySql
dbName = Oracle
~~~

我们把数据库写到配置文件db.properties配置文件中，防止修改数据库代码重新编译



~~~
// User

package com.test.model;

public class User {
    
    private int id;

    public User(int id) {
        this.id = id;
    }

    public User() {
    }

    public int getId() {
        return id;
    }

    public void setId(int id) {
        this.id = id;
    }
}


// Department

package com.test.model;

public class Department {
    
    private int id;
    
    public Department() {
        
    }

    public Department(int id) {
        this.id = id;
    }

    public int getId() {
        return id;
    }

    public void setId(int id) {
        this.id = id;
    }
}

~~~

两个model层实体类，分别对应数据库中两张表



~~~
// IUser
package com.test.methods;

import com.test.model.User;

public interface IUser {
    
    void insert(User user);
    
    User getUser(int id);
}

// MySqlUser
package com.test.methods;

import com.test.model.User;

public class MySqlUser implements IUser {

    @Override
    public void insert(User user) {
        System.out.println("在mysql中给user增加一条记录");
    }

    @Override
    public User getUser(int id) {
        System.out.println("在mysql中根据id得到user中的一条记录");
        return null;
    }
}

// OracleUser
package com.test.methods;

import com.test.model.User;

public class OracleUser implements IUser {

    @Override
    public void insert(User user) {
        System.out.println("在Oracle中给user插入一条记录");
    }

    @Override
    public User getUser(int id) {
        System.out.println("从oracle中根据id得到user一条记录");
        return null;
    }
}

~~~

关于User代码。当然Department类似，有IDepartment接口、MySqlDepartment、OracleDepartment



~~~
// DataAccess
package com.test;

import com.test.methods.IDepartment;
import com.test.methods.IUser;

import java.io.IOException;
import java.io.InputStream;
import java.util.Properties;

public class DataAccess {

    private static String packageName = "com.test.methods.";  // 要反射的类的包名
    private static String dbName;
    
    // 类初始化时执行且仅执行一次
    static {
        InputStream in = DataAccess.class.getClassLoader().getResourceAsStream("db.properties"); // 读取配置文件
        Properties properties = new Properties();
        try {
            properties.load(in);
            dbName = properties.getProperty("dbName");
        } catch (IOException e) {
            e.printStackTrace();
        }
    }

    // 根据反射得到的类创建不同的实例
    public static IUser createUser() throws ClassNotFoundException, IllegalAccessException, InstantiationException {
        Class clazz = Class.forName(packageName + dbName+"User"); //拼接要反射的Class的完整类名
        return (IUser) clazz.newInstance();  // 返回创建的实例
    }
    
    
    public static IDepartment createDepartment() throws ClassNotFoundException, IllegalAccessException, InstantiationException {
        Class clazz = Class.forName(packageName + dbName+"Department");
        return (IDepartment) clazz.newInstance();
    }
}

~~~

工具类DataAccess ,首先读取配置文件，然后根据配置文件内容利用反射动态创建不同实例对象



~~~
// Main
package com.test;

import com.test.methods.IDepartment;
import com.test.model.Department;
import com.test.model.User;
import com.test.methods.IUser;

public class Main {

    public static void main(String[] args) {
        User user = new User();
        user.setId(1);
        Department department = new Department();
        department.setId(1);
        try {
            IUser iu = DataAccess.createUser();
            iu.insert(user);
            iu.getUser(1);

            IDepartment id = DataAccess.createDepartment();
            id.insert(department);
            id.getDepartment(1);
        } catch (ClassNotFoundException e) {
            e.printStackTrace();
        } catch (IllegalAccessException e) {
            e.printStackTrace();
        } catch (InstantiationException e) {
            e.printStackTrace();
        }
    }
}

~~~

最后Main方法

最终运行结果是这样子的

~~~
在Oracle中给user插入一条记录
从oracle中根据id得到user一条记录
在Oracle中给department插入一条记录
从oracle中根据id得到department一条记录

Process finished with exit code 0
------------------------------------------
在mysql中给user增加一条记录
在mysql中根据id得到user中的一条记录
在mysql中给department增加一条记录
在mysql中根据id得到department中的一条记录

Process finished with exit code 0

~~~









