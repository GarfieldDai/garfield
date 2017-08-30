---
title: Spring Framework 概述
date: 2017-08-30 10:06:37
categories: Spring
tags: Spring Framework
thumbnail: "/images/Spring/spring.png"
---
![](/images/Spring/spring.png)

## 目的
介绍什么是Spring Framework，基于Spring Framework 4.3.10 Release进行讲解。

<!--more-->

## 简介
Spring Framework是一个实现了依赖注入DI的控制反转IOC容器。该框架提供了一个轻量级的，非侵入式的，一站式的企业级应用解决方案。该方案提供了诸多的模块可供使用，该框架有以下的特征：
+ 依赖注入 Dependency Injection
+ 面向切面的编程 Aspect-Oriented Programming
+ 声明式事务管理 Declarative Transaction Management
+ Spring MVC web应用和基于RESTful的web service框架
+ 支持JDBC，JPA，JMS的集成
+ Much more...

## 内容
![Overview of the Spring Framework](/images/Spring/spring-overview.png)

Spring Framework由20个模块组成，归为以下几部分：
+ Core Container
+ AOP and Instrumentation
+ Messaging
+ Data Access/Integration
+ Web
+ Test

1. Core Container
这部分由`spring-core`,`spring-beans`,`spring-context`,`spring-context-support`和`spring-expression`(Spring Expression Language)五个模块组成。
`spring-core`和`spring-beans`构成了该框架的基础，里面包括了控制反转和依赖注入。

2. AOP and Instrumentation
`spring-aop`提供了面向切面编程的实现，能够减少代码的重复，耦合和侵入。
`spring-aspects`该模块继承了`AspectJ`。
Instrumentation包括了`spring-instrument`和`spring-instrument-tomcat`。

3. Messaging
这部分包含模块`spring-messaging`，为基于消息服务架构的应用程序提供消息服务。

4. Data Access/Integration
这部分由JDBC，ORM，OXM，JMS，和Transaction组成。
`spring-jdbc`模块提供了JDBC抽象层，免去了配置JDBC的麻烦。
`spring-tx`模块支持声明式事务管理。
`spring-orm`模块为对象-关系型映射(Object-relational mapping)API提供了集成层，包括JPA，JDO和Hibernate。
`spring-oxm`模块为对象-XML型映射(Object/XML mapping)提供了抽象层，包括JAXB，Castor， XMLBeans，JiBX和XStream。
`spring-jms`模块包含了消息的生产和消费，为Java消息服务(Java Messaging Service)提供了集成。从Spring Framework 4.1后，和模块`spring-messaging`一起提供集成服务。

5. Web
这部分包含模块`spring-web`，`spring-webmvc`，`spring-websocket`和`spring-webmvc-portlet `。构建web应用需要引入这些模块，这就是俗称的SpringMVC。

6. Test
`spring-test`该模块支持使用JUnit或者TestNG进行单元测试和集成测试。

## Spring Framework Artifacts
以下就是Spring Framework总的20个模块：

GroupId | ArtifactId | Description
--------|------------|---------------
org.springframework|spring-aop|Proxy-based AOP support
org.springframework|spring-aspects|AspectJ based aspects
org.springframework|spring-beans|Beans support, including Groovy
org.springframework|spring-context|Application context runtime, including scheduling and remoting abstractions
org.springframework|spring-context-support|Support classes for integrating common third-party libraries into a Spring application context
org.springframework|spring-core|Core utilities, used by many other Spring modules
org.springframework|spring-expression|Spring Expression Language (SpEL)
org.springframework|spring-instrument|Instrumentation agent for JVM bootstrapping
org.springframework|spring-instrument-tomcat|Instrumentation agent for Tomcat
org.springframework|spring-jdbc|JDBC support package, including DataSource setup and JDBC access support
org.springframework|spring-jms|JMS support package, including helper classes to send/receive JMS messages
org.springframework|spring-messaging|Support for messaging architectures and protocols
org.springframework|spring-orm|Object/Relational Mapping, including JPA and Hibernate support
org.springframework|spring-oxm|Object/XML Mapping
org.springframework|spring-test|Support for unit testing and integration testing Spring components
org.springframework|spring-tx|Transaction infrastructure, including DAO support and JCA integration
org.springframework|spring-web|Foundational web support, including web client and web-based remoting
org.springframework|spring-webmvc|HTTP-based Model-View-Controller and REST endpoints for Servlet stacks
org.springframework|spring-webmvc-portlet|MVC implementation to be used in a Portlet environment
org.springframework|spring-websocket|WebSocket and SockJS infrastructure, including STOMP messaging support

## Quick Start
示例代码使用Spring Framework 4.3.10，需要Java 6以上环境，这个例子简单的演示了如何使用Spring进行依赖注入，`MessagePrinter`与`MessageService`如何通过接口实现解耦。

1. 创建Maven项目，添加`spring-context`依赖。
```xml
<dependencies>
    <dependency>
        <groupId>org.springframework</groupId>
        <artifactId>spring-context</artifactId>
        <version>4.3.10.RELEASE</version>
    </dependency>
</dependencies>
```

2. `hello/MessageService.java`

```java
package hello;

public interface MessageService {
    String getMessage();
}
```

3. `hello/MessagePrinter.java`
```java
package hello;

import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.stereotype.Component;

@Component
public class MessagePrinter {

    final private MessageService service;

    @Autowired
    public MessagePrinter(MessageService service) {
        this.service = service;
    }

    public void printMessage() {
        System.out.println(this.service.getMessage());
    }
}
```

4. `hello/Application.java`
```java
package hello;

import org.springframework.context.ApplicationContext;
import org.springframework.context.annotation.*;

@Configuration
@ComponentScan
public class Application {

    @Bean
    MessageService mockMessageService() {
        return new MessageService() {
            public String getMessage() {
              return "Hello World!";
            }
        };
    }

  public static void main(String[] args) {
      ApplicationContext context =
          new AnnotationConfigApplicationContext(Application.class);
      MessagePrinter printer = context.getBean(MessagePrinter.class);
      printer.printMessage();
  }
}
```

5. 最后程序输出`Hello World!`。

参考资料
[Spring Framework](http://projects.spring.io/spring-framework/)
[Spring Framework Reference Document](docs.spring.io/spring/docs/current/spring-framework-reference/htmlsingle/)
