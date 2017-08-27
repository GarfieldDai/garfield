---
title: Hibernate Validator进行数据校验
date: 2017-08-26 16:24:52
categories: Hibernate
thumbnail: "/images/Hibernate/hibernate.jpeg"
---
![](/images/Hibernate/hibernate.jpeg)

## 目的
使用 Hibernate Validator 进行数据校验。

<!--more-->

## 简介
在应用程序的所有分层中，从表现层（Presentation Layer）到持久层（Persistent Layer）进行数据的校验都是一个非常必要的工作。如果每层都进行相同代码的数据校验，不仅费时而且也不能保证校验过程不会出错。
![](/images/Hibernate/hibernateValidator1.png)
为了避免这些重复校验的工作，开发者通常将所有的校验逻辑直接绑定在领域模型（Domain Model）里面。JSR 380 - Bean Validation 2.0里面定义了实体类（Entity）和方法的校验接口。Hibernate Validator进行了 JSR 380 接口的实现，Hibernate Validator 6 和 Bean Validation 2.0 需要 Java 8 以上。
![](/images/Hibernate/hibernateValidator2.png)

## 内容
接下来会介绍怎么在你的应用程序里面进行 Hibernate Validator 6 的应用。
+ 需要 Java 8 及以上的环境。
+ 项目使用 Apache Maven 进行依赖管理。

1. 首先需要创建 Maven 项目，加入相关的依赖。
```XML
<dependency>
    <groupId>org.hibernate.validator</groupId>
    <artifactId>hibernate-validator</artifactId>
    <version>6.0.2.Final</version>
</dependency>
<dependency>
    <groupId>org.glassfish</groupId>
    <artifactId>javax.el</artifactId>
    <version>3.0.1-b08</version>
</dependency>
```

2. 创建实体类，使用注解进行校验。

  + `@NotNull`：表示该字段不能为空。
  + `@Size(min = 2, max = 14)`：表示该字段长度在2到14之间。  
  + `@Min(2)`：表示该字段的值必须大于或等于2 。   
```Java
package com.garfieldwiki.hibernate;

import javax.validation.constraints.Min;
import javax.validation.constraints.NotNull;
import javax.validation.constraints.Size;

public class Car {

  @NotNull
  private String manufacturer;

  @NotNull
  @Size(min = 2, max = 14)
  private String licensePlate;

  @Min(2)
  private int seatCount;

  public Car(String manufacturer, String licensePlate, int seatCount) {
    super();
    this.manufacturer = manufacturer;
    this.licensePlate = licensePlate;
    this.seatCount = seatCount;
  }

  public String getManufacturer() {
    return manufacturer;
  }

  public void setManufacturer(String manufacturer) {
    this.manufacturer = manufacturer;
  }

  public String getLicensePlate() {
    return licensePlate;
  }

  public void setLicensePlate(String licensePlate) {
    this.licensePlate = licensePlate;
  }

  public int getSeatCount() {
    return seatCount;
  }

  public void setSeatCount(int seatCount) {
    this.seatCount = seatCount;
  }

}
```

3. 使用单元测试进行数据校验测试。这里使用`Validator`这个对象，该对象从`ValidatorFactory`这个工厂类获得，`Validator`是线程安全的，可以在多线程的环境下使用。`validate()`这个方法返回一个`ConstraintViolation`的Set对象，该对象存储的是所有校验后的结果，如果校验结果都通过，那么该集合的长度为0，表示成功通过校验。
```Java
package com.garfieldwiki.hibernate;

import java.util.Set;

import javax.validation.ConstraintViolation;
import javax.validation.Validation;
import javax.validation.Validator;
import javax.validation.ValidatorFactory;

import org.junit.Assert;
import org.junit.BeforeClass;
import org.junit.Test;

public class TestCar {

  private static Validator validator;

  @BeforeClass
  public static void setUp() {
    ValidatorFactory factory = Validation.buildDefaultValidatorFactory();
    validator = factory.getValidator();
  }

  @Test
  public void manufacturerIsNull() {
    Car car = new Car(null, "DD-AB-123", 4);
    Set<ConstraintViolation<Car>> constraintViolations = validator.validate(car);
    Assert.assertEquals(1, constraintViolations.size());
    Assert.assertEquals("must not be null", constraintViolations.iterator().next().getMessage());
  }

  @Test
  public void licensePlateTooShort() {
    Car car = new Car("Mirrors", "D", 4);
    Set<ConstraintViolation<Car>> constraintViolations = validator.validate(car);
    Assert.assertEquals(1, constraintViolations.size());
    Assert.assertEquals("size must be between 2 and 14", constraintViolations.iterator().next().getMessage());
  }

  public void seatCountTooLow() {
    Car car = new Car("Mirrors", "DD-AB-123", 1);
    Set<ConstraintViolation<Car>> constraintViolations = validator.validate(car);
    Assert.assertEquals(1, constraintViolations.size());
    Assert.assertEquals("must be greater than or equal to 2", constraintViolations.iterator().next().getMessage());
  }

  @Test
  public void carIsValid() {
    Car car = new Car("Morris", "DD-AB-123", 2);
    Set<ConstraintViolation<Car>> constraintViolations = validator.validate(car);
    Assert.assertEquals(0, constraintViolations.size());
  }

}
```


参考资料
[Hibernate Validation Reference Guide](http://docs.jboss.org/hibernate/stable/validator/reference/en-US/html_single/#validator-gettingstarted-createmodel)
