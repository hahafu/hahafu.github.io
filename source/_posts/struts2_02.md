---
title: struts2_02 
---
# struts2学习_02
##  struts2执行过程

 1. **浏览器向服务器发送请求。**  
 		  比如：localhost:8080/struts2_test1/userAction.action，Tomcat接收到请求，Tomcatserver来选择处理这个请求的Web应用，然后由struts2_test1这个web项目处理请求。
 2. **Tomcat服务器读取struts2_test1项目下的web.xml文件。** 
          在web.xml下找到配置的struts2过滤器，请求会经过过滤器，`<url-pattern>/*</url-pattern>`表示过滤所有请求。过滤器会在服务器启动时创建。
   
 3. **struts过滤器实现的功能**、
       第一步：获取请求路劲，得到路径中的userAction值
       第二步：到src目录下找到struts.xml文件，使用dom4j解析得到xml文件中的内容，把拿到userAction值到struts.xml，找到action标签，匹配name是否相同
       第三步：匹配name相同，找到所在action标签的class属性值，得到action全路径，使用反射实现功能。
       反射实现过程：
       （1）.得到class。`class clazz = class.forName("action全路径")`
       （2）.得到名称是execute的方法。`Method method = clazz.getMethod("execute")`
       （3）.方法执行。`Object obj = method.Invoke()`
       第四步：得到action的返回值，回到struts.xml中找到action标签下的result标签，配置result标签的name属性值，值一样跳转至相应的页面
