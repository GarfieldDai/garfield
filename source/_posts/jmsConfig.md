---
title: Spring配置ActiveMQ和Tibco EMS
date: 2017-09-06 11:14:00
categories: Spring
tags: JMS
thumbnail: "/images/Spring/jms.png"
---
![]("/images/Spring/jms.png")

## 目的
如何使用Spring配置ActiveMQ和Tibco EMS(TIBCO Enterprise For JMS)。

<!--more-->

## 简介
示例项目本身建立在Spring的基础之上，这里只讨论如何引用消息中间件的必要依赖。
+ Maven
+ Spring Framework

## ActiveMQ
1. 添加spring-jms和ActiveMQ的依赖。
```xml
<dependency>
	<groupId>org.springframework</groupId>
	<artifactId>spring-jms</artifactId>
	<version>4.3.1.RELEASE</version>
</dependency>
<dependency>
	<groupId>org.apache.activemq</groupId>
	<artifactId>activemq-core</artifactId>
	<version>5.7.0</version>
</dependency>
```

2. `applicationContext.xml`配置，监听地址为`brokerURL`，监听的队列(Queue)`queueDestination`为garfield，监听类为`com.garfieldwiki.jms.QueueConsumer`。
```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans
	xmlns="http://www.springframework.org/schema/beans"
	xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
	xsi:schemaLocation="http://www.springframework.org/schema/beans
          http://www.springframework.org/schema/beans/spring-beans.xsd">

	<bean id="targetConnectionFactory" class="org.apache.activemq.ActiveMQConnectionFactory">
        <property name="brokerURL" value="tcp://localhost:61616"/>
    </bean>

    <bean id="connectionFactory" class="org.springframework.jms.connection.SingleConnectionFactory">
        <property name="targetConnectionFactory" ref="targetConnectionFactory"/>
    </bean>

    <bean id="jmsTemplate" class="org.springframework.jms.core.JmsTemplate">
        <property name="connectionFactory" ref="connectionFactory"/>
    </bean>

    <bean id="queueDestination" class="org.apache.activemq.command.ActiveMQQueue">
        <constructor-arg>
            <value>garfield</value>
        </constructor-arg>
    </bean>

    <bean id="queueConsumer" class="com.garfieldwiki.jms.QueueConsumer"/>

    <bean id="jmsContainer"
        class="org.springframework.jms.listener.DefaultMessageListenerContainer">
        <property name="connectionFactory" ref="connectionFactory" />
        <property name="destination" ref="queueDestination" />
        <property name="messageListener" ref="queueConsumer" />
    </bean>

</beans>
```

3. `com.garfieldwiki.jms.QueueConsumer`，该类继承了MessageListener，监听队列的消息。
```java
package com.garfieldwiki.jms;

import java.util.logging.Logger;

import javax.jms.JMSException;
import javax.jms.Message;
import javax.jms.MessageListener;
import javax.jms.TextMessage;

public class QueueConsumer implements MessageListener {

	private static final Logger LOGGER = Logger.getLogger(QueueConsumer.class.getName());

	public void onMessage(Message message) {
		try {
			TextMessage textMsg = (TextMessage) message;
			LOGGER.info("Receive a message from garfield queue: " + textMsg.getText());
		} catch (JMSException e) {
			LOGGER.warning(e.getMessage());
		}
	}

}
```

4. `com.garfieldwiki.jms.QueueProducer`，该类可以发送消息到队列。
```java
package com.garfieldwiki.jms;

import java.util.logging.Logger;

import javax.jms.JMSException;
import javax.jms.Message;
import javax.jms.Queue;
import javax.jms.Session;

import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.beans.factory.annotation.Qualifier;
import org.springframework.jms.core.JmsTemplate;
import org.springframework.jms.core.MessageCreator;
import org.springframework.stereotype.Component;

@Component
public class QueueProducer {

	private static final Logger LOGGER = Logger.getLogger(QueueProducer.class.getName());

	@Autowired
	private JmsTemplate jmsTemplate;

	@Autowired
	@Qualifier("queueDestination")
	private Queue queue;

	public void sendMessage() {
		this.jmsTemplate.send(this.queue, new MessageCreator() {
			public Message createMessage(Session session) throws JMSException {
				String msg = "Hello, I am Garfield.";
				LOGGER.info("Send message to garfield queue: " + msg);
				return session.createTextMessage(msg);
			}
		});
	}

}
```

## Tibco EMS
1. 引入必要的jar包，可在Tibco的安装目录寻找`C:\tibco\ems\8.3\lib`。
+ jms-2.0.jar
+ tibjms.jar

2. 项目只需要引入spring-jms即可。
```xml
<dependency>
	<groupId>org.springframework</groupId>
	<artifactId>spring-jms</artifactId>
	<version>4.3.1.RELEASE</version>
</dependency>
```

3. `applicationContext.xml`配置跟ActiveMQ有不同，主要是相关实现类的命名方式不一样。
```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans
	xmlns="http://www.springframework.org/schema/beans"
	xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
	xmlns:context="http://www.springframework.org/schema/context"
	xsi:schemaLocation="http://www.springframework.org/schema/context
          http://www.springframework.org/schema/context/spring-context.xsd
          http://www.springframework.org/schema/beans
          http://www.springframework.org/schema/beans/spring-beans.xsd">

	<bean id="targetConnectionFactory" class="com.tibco.tibjms.TibjmsConnectionFactory">
        <property name="serverUrl" value="tcp://localhost:7222"/>
        <property name="userName" value=""/>
        <property name="userPassword" value=""/>
    </bean>

    <bean id="connectionFactory" class="org.springframework.jms.connection.SingleConnectionFactory">
        <property name="targetConnectionFactory" ref="targetConnectionFactory"/>
    </bean>

    <bean id="jmsTemplate" class="org.springframework.jms.core.JmsTemplate">
        <property name="connectionFactory" ref="connectionFactory"/>
    </bean>

    <bean id="queueDestination" class="com.tibco.tibjms.TibjmsQueue">
        <constructor-arg>
            <value>garfield</value>
        </constructor-arg>
    </bean>

    <bean id="jmsContainer"
        class="org.springframework.jms.listener.DefaultMessageListenerContainer">
        <property name="connectionFactory" ref="connectionFactory" />
        <property name="destination" ref="queueDestination" />
        <property name="messageListener" ref="blChangeConsumer" />
    </bean>

</beans>
```

4. Tibco EMS消息的生产和消费跟ActiveMQ一样。

参考资料
[Maven ActiveMQ](https://mvnrepository.com/artifact/org.apache.activemq/activemq-core)
