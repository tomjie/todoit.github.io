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
> 编写过滤器类
```{java}
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


```

> 将过滤器加入到web.xml中

修改tomcat下面的servie.xml文件
`URIEncoding="UTF-8" `



