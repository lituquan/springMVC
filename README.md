# springMVC
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
   
   -->提交表单上传文件请求
      （form表单设置enctype,input使用file类型）
   -->服务器DispatcherServlet路由匹配
      （需要在web.xml配置DispatcherServlet）
   -->进入控制器,文件接收并绑定到参数
      （需要在springmvc-servlet.xml配置CommonsMultipartResolver）
   -->处理请求,返回视图   
    
   form 表单设置：
    <textarea rows=20 cols=60>
    <form action="upload" enctype="multipart/form-data" method="post"><!--设置编码类型-->
        <table>
            <tr>
                <td>文件描述:</td>
                <td><input type="text" name="description"></td>
            </tr>
            <tr>
                <td>请选择文件:</td>
                <td><input type="file" name="file"></td><!--设置input类型,name 用来对应控制器接收参数-->
            </tr>
            <tr>
                <td><input type="submit" value="上传"></td>
            </tr>
        </table>
    </form>
    </textarea>
   springMVC配置接收文件：    
    <pre>
    <bean id="multipartResolver"  
        class="org.springframework.web.multipart.commons.CommonsMultipartResolver">  
        <!-- 上传文件大小上限，单位为字节（10MB） -->
        <property name="maxUploadSize">  
            <value>10485760</value>  
        </property>  
        <!-- 请求的编码格式，必须和jSP的pageEncoding属性一致，以便正确读取表单的内容，默认为ISO-8859-1 -->
        <property name="defaultEncoding">
            <value>UTF-8</value>
        </property>
    </bean>
    
   springMVC控制器：	  
    //上传文件会自动绑定到MultipartFile中
    @RequestMapping(value="/upload")
    public String upload(HttpServletRequest request,
           @RequestParam("description") String description,
           @RequestParam("file") MultipartFile file) throws Exception {
       //如果文件不为空，写入上传路径
       if(!file.isEmpty()) {
           //上传文件路径
           String path = request.getServletContext().getRealPath("/images/");
           //上传文件名
           String filename = file.getOriginalFilename();
           File filepath = new File(path,filename);
           //判断路径是否存在，如果不存在就创建一个
           if (!filepath.getParentFile().exists()) { 
               filepath.getParentFile().mkdirs();
           }
           //将上传文件保存到一个目标文件当中
           file.transferTo(new File(path + File.separator + filename));
           return "success";
       } else {
           return "error";
       }
    }   
   </pre>
 3. 参数和视图  
    控制器的方法，参数签名绑定，控制器返回值是视图。

