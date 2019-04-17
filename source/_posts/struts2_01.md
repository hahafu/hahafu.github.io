---
title: struts2_01 
---
# struts2学习_01
## 一、struts2概述
1、Struts2是一个基于MVC设计模式的Web应用框架，它本质上相当于一个servlet，在MVC设计模式中，Struts2作为控制器(Controller)来建立模型与视图的数据交互。2、Struts 2是Struts的下一代产品，是在 struts 1和WebWork的技术基础上进行了合并的全新的Struts 2框架。其全新的Struts 2的体系结构与Struts 1的体系结构差别巨大。Struts 2以WebWork为核心，采用拦截器的机制来处理用户的请求，这样的设计也使得业务逻辑控制器能够与ServletAPI完全脱离开，所以Struts 2可以理解为WebWork的更新产品。虽然从Struts 1到Struts 2有着太大的变化，但是相对于WebWork，Struts 2的变化很小。
## 二、struts2框架入门

 - struts2版本为struts-2.3.24
 - 第一步：导入struts2框架jar包
 		（1）从struts2官网下载完整包解压，在lib目录中有jar包，不能把这些jar包都导入项目中，其中很多jar包用不上
 		（2）到apps目录中，找到示例程序解压，然后找到示例程序下的lib目录，复制里面的jar包到自己新建的web项目中	
 - 第二部：在web.xml中配置struts过滤器
 

```
<filter>
    <filter-name>struts</filter-name>
    <filter-class>org.apache.struts2.dispatcher.ng.filter.StrutsPrepareAndExecuteFilter</filter-class>
  </filter>
  
  <filter-mapping>
    <filter-name>struts</filter-name>
    <url-pattern>/*</url-pattern>
  </filter-mapping>
```

 - 第三步：创建action
 	（1）新建一个普通类，然后在类中写execute方法
```
public class HelloAction extends {

    /**
     *(1)每次访问servlet时，都会执行service方法
     *(2)每次访问action,默认执行execute方法
     */
    private static final long serialVersionUID = 1L;

    public String execute() {
        return "ok";
    }
}
```
 - 第四步：配置action的访问路径
 	（1）创建struts2核心配置文件， 核心配置文件名称和位置是固定的， 位置必须在src下面，名称 struts.xml
 	（2）引入dtd约束

```
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE struts PUBLIC
    "-//Apache Software Foundation//DTD Struts Configuration 2.3//EN"
    "http://struts.apache.org/dtds/struts-2.3.dtd">
```
 	（3）struts.xml配置action访问路径
 	
```
<struts>
	<!-- package标签的name属性值为包名，extends="struts-default"就是继承struts-default.xml，它里面定义了许多跳转类型、拦截器等一些常用的东西，namespace：命名空间，默认为'/'表示webapp根目录 -->
    <package name="hello" extends="struts-default" namespace="/">
    	<!-- action标签的name属性值为访问名称-->
        <action name="userAction" class="cn.com.action.HelloAction">
            <result name="ok">/hello.jsp</result>
        </action>
    </package>
</struts>
```
然后把项目部署到Tomcat中，在浏览器中访问，访问路劲为localhost:8080/struts2_test1/userAction.action，
localhost:8080表示本机8080端口，也就是Tomcat 服务器端口，后面接上项目名和action名，用“/”隔开
