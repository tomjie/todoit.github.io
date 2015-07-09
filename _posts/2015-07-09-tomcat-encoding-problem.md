---
layout: post
title: tomcat服务器一种无法解决的乱码方式
categories:
- program
tags:
- java
- tomcat
- 过滤器
---

以前总是用`new string(.getbytes( iso-8859-1 ) utf-8 )`处理中文乱码，但是后来经大牛指点，发现这种方式不仅使用繁琐而且不友好，经常无缘无故出问题。

于是经人指点使用了过滤器。过滤器的使用方法:
- ##编写过滤器类

{% highlight java %} 
package cn.ac.imicams.todoit.util.encoding;
import java.io.IOException;
import javax.servlet.Filter;
import javax.servlet.FilterChain;
import javax.servlet.FilterConfig;
import javax.servlet.ServletException;
import javax.servlet.ServletRequest;
import javax.servlet.ServletResponse;
//字符编码处理
public class CharacterEncodingFilter implements Filter {
    protected FilterConfig filterConfig = null;
    protected String encoding = "";
    public void destroy() {
        filterConfig = null;
        encoding = null;
    }
    public void doFilter(ServletRequest servletRequest, ServletResponse servletResponse,
            FilterChain filterChain) throws IOException, ServletException {
        if(encoding != null && !"".equals(encoding))
            servletRequest.setCharacterEncoding(encoding);
        filterChain.doFilter(servletRequest, servletResponse);
    }
    public void init(FilterConfig filterConfig) throws ServletException {
        this.filterConfig = filterConfig;
        this.encoding = filterConfig.getInitParameter("encoding");
        System.out.print(this.encoding);
    }
}

{% endhighlight %}

- ##将过滤器加入到web.xml中

{% highlight xml %} 
<?xml version="1.0" encoding="UTF-8"?>
<web-app version="2.5" 
	xmlns="http://java.sun.com/xml/ns/javaee" 
	xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" 
	xsi:schemaLocation="http://java.sun.com/xml/ns/javaee 
	http://java.sun.com/xml/ns/javaee/web-app_2_5.xsd">
  <welcome-file-list>
    <welcome-file>index.jsp</welcome-file>
  </welcome-file-list>
  
   <!-- 乱码过滤器 -->
       
        <filter>
	        <filter-name>characterEncodingFilter</filter-name>
	        <filter-class>cn.ac.imicams.todoit.util.encoding.CharacterEncodingFilter</filter-class>
	        <init-param>
	            <param-name>encoding</param-name>
	            <param-value>UTF-8</param-value>
	        </init-param>
    	</filter>
	    <filter-mapping>
	      <filter-name>characterEncodingFilter</filter-name>
	      <url-pattern>*</url-pattern>
	    </filter-mapping>
	    
</web-app>

{% endhighlight %}

完成上述设置后，发现仍然是乱码，折腾了一上午找不到根源，最后搜到了解决方法，原来是tomcat设置的问题，在tomcat根目录的conf文件夹下的server.xml文件中，找到下面这段，将URIEncoding修改为UTF-8，如果没有则加上，乱码问题自然解决。

{% highlight xml %} 

<Connector port="8080" protocol="HTTP/1.1" 
               connectionTimeout="20000" 
               redirectPort="8443"  
               URIEncoding="UTF-8" /> #修改为
               
{% highlight xml %} 




