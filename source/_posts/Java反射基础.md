---
title: Java反射基础
date: 2018-05-13 16:10:46
tags: [Java SE]
---

## Java反射基础

Java,一门完全面向对象语言，在Java的世界中处处皆是对象，

当然，一个class、一个method、一个field这些也都例外。

而反射(reflect)，不仅能动态加载类，还能让其获取自身的信息：

### Class类的使用：

~~~
public class ClassDemo
{
 
	public static void main(String[] args)
	{
		Test t1 = new Test();
		Class c1 = Test.class;
		Class c2 = t1.getClass();
		System.out.println(c1 == c2); // 证明类类型也是引用
 
		Class c3 = null;
		try
		{
			c3 = Class.forName("com.reflect.Test");  // 动态加载Test类
		} catch (ClassNotFoundException e)
		{
			// TODO Auto-generated catch block
			e.printStackTrace();
		}
		System.out.println(c2 == c3);
	}
 
}
 
class Test{}
~~~

打印结果为：true  true





### 获取方法信息：

~~~
public class ClassUtil
{
 
	public static void printClassMeeeage(Object obj)
	{
		// 获取类的信息  首先获得类的类类型
		Class c = obj.getClass();
		// 获取类的名称
		System.out.println("类的名称：" + c.getName());
		/*
		 * Method类，方法对象
		 * 一个成员方法就是一个Method对象
		 * getMethod()方法获取的是所有的public函数，包括父类继承而来
		 *
		 */
		Method[] ms = c.getMethods(); // c.getDeclaredMethod()
		for (int i = 0; i < ms.length; i++)
		{
			// 得到方法返回值类型的类类型
			Class returnType = ms[i].getReturnType();
			System.out.print(returnType.getName() + " ");
			// 得到方法名称
			System.out.print(ms[i].getName() + "(");
			// 获取参数类型  参数列表的类型的类类型
			Class[] paramTypes = ms[i].getParameterTypes();
			for (Class class1 : paramTypes)
			{
				System.out.print(class1.getName() + ", ");
			}
			System.out.println(")");
		}
	}
}
~~~





### 获取成员变量信息：

***成员变量也是对象**   

***java.lang.reflect.Field**   

***Field封装了关于成员变量的操作**   

***getDeclaredField获取的是该类声明的所有的数据成员的信息** 

~~~
public static void printFieldMessage(Object obj)
	{
		Class c = obj.getClass();
		Field[] fs = c.getDeclaredFields();
		for (Field field : fs)
		{
			// 获取成员变量类型的类类型
			Class fieldType = field.getType();
			String typeName = fieldType.getName();
			// 获取成员变量的名称
			String fieldName = field.getName();
			System.out.println(fieldName + " " + typeName);
		}
	}
~~~





### 获取构造方法信息

*** 构造方法也是对象**      

 *** java.lang.reflect.Constructor**      

 *** Constructor封装了关于构造方法的操作**      

 *** getConstructor获得该类声明额构造方法** 

~~~
public static void printConMessage(Object obj)
	{
		Class c = obj.getClass();
		Constructor[] cs = c.getDeclaredConstructors();
		for (Constructor constructor : cs)
		{
			System.out.print(constructor.getName() + "(");
			// 获取构造函数的参数列表
			Class paramTypes[] = constructor.getParameterTypes();
			for (Class class1 : paramTypes)
			{
				System.out.print(class1.getName() + ",");
			}
			System.out.println(")");
		}
	}
~~~



