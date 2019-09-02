

写在前面：本次采用的springboot的版本是2.X

# 第一步 添加actuator依赖
1.**pom.xml** 如下：
```xml
<?xml version="1.0" encoding="UTF-8"?>
<project xmlns="http://maven.apache.org/POM/4.0.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">
    <modelVersion>4.0.0</modelVersion>
    <parent>
        <groupId>org.springframework.boot</groupId>
        <artifactId>spring-boot-starter-parent</artifactId>
        <version>2.0.3.RELEASE</version>
        <relativePath/> <!-- lookup parent from repository -->
    </parent>
    <groupId>com.example</groupId>
    <artifactId>configuration</artifactId>
    <version>0.0.1-SNAPSHOT</version>
    <name>configuration</name>
    <description>Demo project for Spring Boot</description>

    <properties>
        <java.version>1.8</java.version>
    </properties>

    <dependencies>


        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-actuator</artifactId>
        </dependency>

        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-web</artifactId>
        </dependency>

        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-test</artifactId>
            <scope>test</scope>
        </dependency>
    </dependencies>

    <build>
        <plugins>
            <plugin>
                <groupId>org.springframework.boot</groupId>
                <artifactId>spring-boot-maven-plugin</artifactId>
            </plugin>
        </plugins>
    </build>

</project>

```

# 第二步 加入配置
1.**application.properties** 如下:
```xml
#web服务端端口
server.port=6000

#监控地址端口
management.server.port=8000

#springboot2.0之后，在Http环境下将默认的endpoint只设置为info和health，要想开启其他的监控功能，需要手动配置
management.endpoints.web.exposure.include=*

#请求连接前缀 默认是/actuator
management.endpoints.web.base-path=/actuator
```

# 第三步 启动验证
### 1.启动项目
启动日志信息中包含如下信息：
![在这里插入图片描述](https://img-blog.csdnimg.cn/20190329082451295.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2JlbG9uZ2h1YW5nMTU3NDA1,size_16,color_FFFFFF,t_70)

从上图可以看出我们将要测试的映射连接地址
### 2.使用浏览器或者Postman

1.**/actuator/env** 查看环境配置
![在这里插入图片描述](https://img-blog.csdnimg.cn/20190329082500358.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2JlbG9uZ2h1YW5nMTU3NDA1,size_16,color_FFFFFF,t_70)

2.**/actuator/beans** 查看所有的bean
![在这里插入图片描述](https://img-blog.csdnimg.cn/20190329082512371.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2JlbG9uZ2h1YW5nMTU3NDA1,size_16,color_FFFFFF,t_70)
*注：上诉内容根据用户自身环境显示*
将不一一进行演示，下表列出常用命令，读者进行测试：

<table><thead><tr><th>HTTP方法</th>
			<th>路径</th>
			<th>描述</th>
			<th>鉴权</th>
		<tr><td>GET</td>
			<td>/actuator//configprops</td>
			<td>查看配置属性，包括默认配置</td>
			<td>true</td>
		</tr><tr><td>GET</td>
			<td>/actuator//beans</td>
			<td>查看bean及其关系列表</td>
			<td>true</td>
		</tr><tr><td>GET</td>
			<td>/actuator//threaddump</td>
			<td>打印线程栈</td>
			<td>true</td>
		</tr><tr><td>GET</td>
			<td>/actuator//env</td>
			<td>查看所有环境变量</td>
			<td>true</td>
		</tr><tr><td>GET</td>
			<td>/actuator//env/{toMatch}</td>
			<td>查看具体变量值</td>
			<td>true</td>
		</tr><tr><td>GET</td>
			<td>/actuator//health</td>
			<td>查看应用健康指标</td>
			<td>false</td>
		</tr><tr><td>GET</td>
			<td>/actuator//info</td>
			<td>查看应用信息（需要自己在application.properties里头添加信息，比如info.contact.email=easonjim@163.com）</td>
			<td>false</td>
		</tr><tr><td>GET</td>
			<td>/actuator//mappings</td>
			<td>查看所有url映射</td>
			<td>true</td>
		</tr><tr><td>GET</td>
			<td>/actuator//metrics</td>
			<td>查看应用基本指标</td>
			<td>true</td>
		</tr><tr><td>GET</td>
			<td>/actuator//metrics/{name}</td>
			<td>查看具体指标</td>
			<td>true</td>
	  <tr><td>GET</td>
			<td>/actuator//httptrace</td>
			<td>查看基本追踪信息</td>
			<td>true</td>
		</tr></tbody></table>
