---
title: 基于角色的权限管理
date: 2017-03-20 14:26:14
categories: Security
tags: RBAC
thumbnail: "/images/Security/RBAC/RBAC05.png"
---
![](/images/Security/RBAC/RBAC05.png)

## 目的
理解什么是基于角色的权限管理（RBAC）？

<!--more-->

## 简介
目前单系统应用中，基于角色的权限管理 *(Role-based Access Control)* 被奉为是最佳实践。

在系统应用中，最核心的是业务的数据和对数据的操作，其次最重要的是系统应该辨别哪些用户可以访问数据和对数据能进行什么操作。后者其实就是所谓的权限管理，权限管理包括认证和授权。
认证就是对用户进行识别，看该用户是不是合法用户，只有合法用户才能够进入系统。授权就是在认证的基础之上，管理用户可以访问哪些数据和对数据的增删查改 *(CRUD)*。

## 内容
基于角色的权限管理实际上是处理主体（Subject），角色（Role），权限（Permission）三者之间的关系。
* Subject：指调用本系统服务的“用户”，可以是具体的某个人也可以是其他系统。
* Role：比如系统管理员，公司普通职员或者经理。
* Permission：比如财务经理可以看到所有员工的薪资，但是普通用户只能看到自己的薪资。

在设计系统架构中，需要考虑三个层面的设计：
* 核心架构
* 角色的继承
* 职责分离

### 核心架构
![RBAC01](/images/Security/RBAC/RBAC01.png)
通常一个机构都会给每个人分配不同的职位，不同职位有不同的工作范围。职位其实就是角色，工作范围也代表了你的操作权限。如图 *RBAC01* 所示，主体，角色和权限其实是多对多的关系。

![RBAC02](/images/Security/RBAC/RBAC02.png)
不同的职位代表了不同的操作权限。

### 角色的继承
![RBAC03](/images/Security/RBAC/RBAC03.png)
通常来说，角色是有继承关系的，比如一个部门经理的权限是包含了该部门普通员工的权限。

![RBAC04](/images/Security/RBAC/RBAC04.png)
举个栗子，在一个软件部门里面，某个人被分配到该部门，他有进入该部门的最低权限，然后他被分配到 TeamOne 做开发，那么他就有该小组的权限和做开发的权限。在该部门里面，Manager有该部门的所有的权限。

### 职责分离
![RBAC05](/images/Security/RBAC/RBAC05.png)
职责分离（Separation of duties）其实就是在用户和角色之间加一层约束。简单的说，就是在同一个球场上，不会有一个人既是球员又是裁判。

## 使用场景
* 在单系统应用中，广泛的被业界所接受，被列为最佳实践。
* 比较适合角色稳定并且角色数量有限的应用。

## 优点
* 批量授权：只要给某个角色赋予对应的权限，就可以批量的授权给对应的用户。
* 能够迅速变更权限：能够快速的变更某个人的角色，比如某员工离职或升职都可以快速的移除或更换对应的角色。

## 缺点
* 需要有人一直去维护主体，角色和权限的关系，直到该系统下线。
* 所有的用户都至少有一个角色。
* 给某个用户授权的时候，都需要有另一个人去审核该用户所对应的角色没有越权。

参考资料
[Wikipedia: Role-based access control](https://en.wikipedia.org/wiki/Role-based_access_control)
[Beyond Roles: A Practical Approach to Enterprise User Provisioning](https://hitachi-id.com/documents/beyond-roles-a-practical-approach-to-enterprise-user-provisioning.php)
[Role Based Access Control (RBAC) and Role Based Security](http://csrc.nist.gov/groups/SNS/rbac/)
