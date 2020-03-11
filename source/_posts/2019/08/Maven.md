---
title: Maven
date: 2019-08-07 18:23:13
categories: Java
---

## Maven能解决什么问题

1. 引入工程所需的各种jar包
2. 编译代码
3. 可以进行单元测试
4. 打包项目、部署项目

## 仓库种类

1. 本地仓库
2. 远程仓库【私服】
3. 中央仓库

## Maven常用的命令

1. **mvn complie**：compile 是 maven 工程的编译命令，作用是将 src/main/java 下的文件编译为 class 文件输出到 target 目录下。
2. **mvn test**： maven 工程的测试命令 mvn test，会执行src/test/java下的单元测试类。
3. **mvn clean**： maven 工程的清理命令，执行 clean 会删除 target 目录及内容。
4. **mvn package**：package 是 maven 工程的打包命令，对于 java 工程执行 package 打成 jar 包，对于web 工程打成war包。
5. **mvn install**：install 是 maven 工程的安装命令，执行 install 将 maven 打成 jar 包或 war 包发布到本地仓库。

注：当后面的命令执行时，前面的操作过程也都会自动执行，

## Maven 生命周期

- Clean Lifecycle 在进行真正的构建之前进行一些清理工作。
- **Default Lifecycle 构建的核心部分，编译，测试，打包，部署等等。**
- Site Lifecycle 生成项目报告，站点，发布站点

## 创建web项目问题

- 出现不能没有创建servlet的选项，在pom文件中加入

  ```xml
  <dependency>
        <groupId>javax.servlet</groupId>
        <artifactId>servlet-api</artifactId>
        <version>2.5</version>
      </dependency>
  ```

  