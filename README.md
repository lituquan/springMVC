# springMVC
    <pre>
1.前端控制器

 springmvc 核心类是org.springframework.web.servlet.DispatcherServlet,它实际上继承了HttpServlet,一般配置在web.xml里面.
    <servlet>
      <servlet-name>springmvc</servlet-name>
      <servlet-class>org.springframework.web.servlet.DispatcherServlet</servlet-class>
      <init-param>
        <param-name>contextConfigLocation</param-name>
        <param-value>WEB-INF/springmvc-servlet.xml</param-value>
      </init-param>
    </servlet>

    <servlet-mapping>
      <servlet-name>springmvc</servlet-name>
      <url-pattern>/</url-pattern><!--路由拦截规则-->
    </servlet-mapping>
    
2.文件上传功能   
   -->提交表单上传文件请求（form表单设置enctype,input使用file类型）
   
   -->服务器DispatcherServlet路由匹配（需要在web.xml配置DispatcherServlet）
   
   -->进入控制器,文件接收并绑定到参数（需要在springmvc-servlet.xml配置CommonsMultipartResolver）
   
   -->处理请求,返回视图  
   
 3. 参数和视图  
    控制器的方法，参数签名绑定，控制器返回值是视图。
    </pre>
