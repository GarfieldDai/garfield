---
title: Spring Boot快速构建项目
date: 2017-08-25 21:56:45
categories: Spring
tags: Spring Boot
thumbnail: "/images/Spring/spring.png"
---
![](/images/Spring/spring.png)

## 目的
如何使用Sprint Boot快速构建项目。

<!--more-->

## 简介
Spring Boot可以简单快速的构建基于Spring的应用系统。
+ 构建独立运行的应用系统，不用额外配置应用服务器，开箱即用。
+ 内置Tomcat，Jetty和Undertow应用服务器，并且不需要部署war文件，默认使用服务器`Tomcat`。
+ Spring自动化配置，提供一站式服务，彻底摆脱XML配置。
+ 项目将会被打包为jar文件，使用`java -jar`即可运行。

## 搭建项目
1. 使用Maven进行项目管理，创建普通Java应用项目，不是Java web项目。本教程基于`Spring Boot 1.5.6 Release`开发。
Spring Boot依赖`groupId`为`org.springframework.boot`相关的项目，项目默认都会依赖`spring-boot-starter-parent`这个项目，该项目提供了构建Spring应用的基本配置和包引用。
```XML
<?xml version="1.0" encoding="UTF-8"?>
<project xmlns="http://maven.apache.org/POM/4.0.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
    xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">
    <modelVersion>4.0.0</modelVersion>

    <groupId>com.example</groupId>
    <artifactId>myproject</artifactId>
    <version>0.0.1-SNAPSHOT</version>

    <parent>
        <groupId>org.springframework.boot</groupId>
        <artifactId>spring-boot-starter-parent</artifactId>
        <version>1.5.6.RELEASE</version>
    </parent>

    <!-- Additional lines to be added here... -->

</project>
```

2. Spring Boot提供了一站式的配置`Starter`,Starters里面引用了构建项目必要的依赖和配置，示例代码使用SpringMVC搭建web应用，只需要在`pom.xml`里面加入`spring-boot-starter-web`的这个`Starter`依赖即可。
```XML
<dependencies>
    <dependency>
        <groupId>org.springframework.boot</groupId>
        <artifactId>spring-boot-starter-web</artifactId>
    </dependency>
</dependencies>
```

3. 在Maven项目创建目录`src/main/java`,在该目录下创建Java类`Example.java`。
```java
import org.springframework.boot.*;
import org.springframework.boot.autoconfigure.*;
import org.springframework.stereotype.*;
import org.springframework.web.bind.annotation.*;

@RestController
@EnableAutoConfiguration
public class Example {

    @RequestMapping("/")
    String home() {
        return "Hello World!";
    }

    public static void main(String[] args) throws Exception {
        SpringApplication.run(Example.class, args);
    }

}
```

4. 可以在IDE里面运行`Main.java`,然后在浏览器访问`http://localhost:8080`，你就会看到应用程序返回`Hello World!`。

5. 创建可执行jar文件，Spring Boot提供了`spring-boot-maven-plugin`该插件。
```xml
<build>
    <plugins>
        <plugin>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-maven-plugin</artifactId>
        </plugin>
    </plugins>
</build>
```

6. 保存`pom.xml`文件，执行命令`mvn package`进行项目打包，你可以在`targe`目录下找到`myproject-0.0.1-SNAPSHOT.jar`文件，以下是完整的`pom.xml`配置。
```xml
<?xml version="1.0" encoding="UTF-8"?>
<project xmlns="http://maven.apache.org/POM/4.0.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
    xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">
    <modelVersion>4.0.0</modelVersion>

    <groupId>com.example</groupId>
    <artifactId>myproject</artifactId>
    <version>0.0.1-SNAPSHOT</version>

    <!-- Inherit defaults from Spring Boot -->
    <parent>
        <groupId>org.springframework.boot</groupId>
        <artifactId>spring-boot-starter-parent</artifactId>
        <version>1.5.6.RELEASE</version>
    </parent>

    <!-- Add typical dependencies for a web application -->
    <dependencies>
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-web</artifactId>
        </dependency>
    </dependencies>

    <!-- Package as an executable jar -->
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

7. 使用命令即可运行打包好的项目`java -jar target/myproject-0.0.1-SNAPSHOT.jar`，无需繁琐的XML配置即可构建基于SpringMVC的Web应用程序。
```
$ java -jar target/myproject-0.0.1-SNAPSHOT.jar

  .   ____          _            __ _ _
 /\\ / ___'_ __ _ _(_)_ __  __ _ \ \ \ \
( ( )\___ | '_ | '_| | '_ \/ _` | \ \ \ \
 \\/  ___)| |_)| | | | | || (_| |  ) ) ) )
  '  |____| .__|_| |_|_| |_\__, | / / / /
 =========|_|==============|___/=/_/_/_/
 :: Spring Boot ::  (v1.5.6.RELEASE)
....... . . .
....... . . . (log output here)
....... . . .
........ Started Example in 2.536 seconds (JVM running for 2.864)
```


参考资料
[Spring Boot Demo](https://github.com/GarfieldDai/springboot)
[Spring Boot Reference Guide](https://docs.spring.io/spring-boot/docs/1.5.6.RELEASE/reference/htmlsingle/)
[Spring Starter](https://docs.spring.io/spring-boot/docs/1.5.6.RELEASE/reference/htmlsingle/#using-boot-starter)
