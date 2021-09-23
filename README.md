------

# Maven

## 1.主要内容

![1](/Volumes/D/code/Java/MavenLearning/img/1.png)

## 2.Maven的简介

### 2.1.简介

maven这个词可以翻译为“专家，内行”。作为Apache组织中的一个颇为成功的开源项目，Maven主要服务于基于java平台的项目构建，依赖管理和项目信息管理

### 2.2.项目构建

构建是每个程序员每天都在做的工作

我们发现，除了编写源代码，我们每天有相当一部分时间花在了编译，运行单元测试，生成文档，打包和部署等繁琐且不起眼的工作上，这就是构建。

于是有人用软件的方法让这一系列工作完全自动化，使得软件的构建可以像全自动流水线一样，只需要一条简单的命令，所有繁琐的步骤都能够自动完成，很快就能得到最终结果。

### 2.3.项目构建工具

> Ant 构建

最早的构建工具，但是其XML脚本编写格式让XML文件特别大。对工程构建过程中的过程控制特别好

>  Maven

项目对象模型，通过其描述信息来管理项目的构建，报告和文档的软件项目管理工具

Maven支持从网络上下载的功能，仍然采用XML作为配置文件格式。Maven专注的是依赖管理，使用Java编写

>  Gradle

结合以上两个的优点，它继承了Ant的灵活和Maven的生命管理周期，是google用于Android的管理工具。它最大的区别是不用XML作为配置文件格式，采用DSL格式，使得脚本更加简洁



### 2.4.Maven的四大特性

####  **2.4.1. 依赖管理系统**

Maven 为java世界引入了一个新的依赖管理系统，jar包管理，jar包升级时修改配置文件即可，在java世界中，可以用groupId，artifactId，version组成的Coordination（坐标）唯一标识一个依赖。

任何基于Maven构建的项目自身也必须定义这三项属性，生成的可以是jar包，也可以是war包或者jar包

一个典型的依赖引入如下所示：

```xml
<dependency>
	<groupId>javax.servlet</groupId>
  <artifactId>javax.servlet-api</artifactId>
	<version>3.1.0</version>
</dependency>
```

> **groupId**

​	定义当前Maven项目隶属的实际项目-公司名称（jar包所在仓库的路径）由于Maven中模块的概念，因此一个项目往往分成许多模块。比如spring是一个实际项目，其对应的Maven模块会有很多，例如spring-core、spring-webmvc等

> **attifactId**

该元素定义实际项目中一个Maven模块-项目名，推荐的做法是使用实际项目名作为artfactId的前缀。比如spring-bean，spring-webmvc等

> **version**

该元素定义Maven项目的当前所处版本


####  **2.4.2. 多模块构建**

项目复查时dao service controller 层分离将一个项目分解为多个模块已经是一种通用的方式。

在Maven中需要定义一个parent POM作为一组module的聚合POM。在该POM中可以使用<modules>标签来定义一组子模块。parent POM不会有什么实际构建产出。而parent POM中的build配置以及依赖配置都会自动继承给子module。



####  **2.4.3**. **一致的项目结构**

Conversion over configuration （约定大于配置）

其定制了一套项目目录结构作为标准的java项目结构，解决不同ide带来的文件目录结构不同的问题。



####  **2.4.4**. **一致的构建模型和插件机制**

## 3.Maven的安装配置和目录结构

### 3.1.Maven的安装配置

#### 参考博客

#### https://blog.csdn.net/zeal9s/article/details/97231887



### 3.2. 认识Maven目录结构

Maven的项目目录结构

![3.2](/Volumes/D/code/Java/MavenLearning/img/3.2.png)

#### 3.2.1.创建一个文件夹作为项目的根目录

在根目录中创建一个pom.xml文件，参考 [maven-pom.xml](maven-pom.xml) 

![3.2.1](/Volumes/D/code/Java/MavenLearning/img/3.2.1.png)

#### 3.2.2. 编写主函数

```java
package com.xxx.demo;
public class Hello{
  public static void main(String[] args){
    System.out.println("hello maven");
  }
}
```

#### 3.2.3.终端下的编译和运行

> 1.使用maven构建web 项目，首先进入项目的根目录。

> 2.使用命令：mvn archetype:generate -DgroupId=组织名 -DartifactId=项目名_模块名 -Dversion=版本号 -Dpackage=代码所存在的包名

   例如：mvn archetype:generate -DgroupId={project-packaging} -DartifactId={project-name} -DarchetypeArtifactId=maven-archetype-webapp -Dpackage=com.xxx.java

  初次建立项目会需要去中央仓库去下载一些相关的依赖包。会花比较长的时间。下载到本地仓库之后就不需要再次下载了。

> maven默认的中央仓库是英国，所以因为国内访问外网不方便的原因可能导致下载失败或者及其的慢，所以我们可以把中央仓库改为国内的。

 在/maven_3.3.9/conf/settings.xml中，有配置镜像地址的示例，

https://www.cnblogs.com/chenyanbin/p/12506889.html



## 4.Maven命令

 作为开发利器Maven，为我们提供了十分丰富的命令，了解maven的命令行操作并熟练运用常见maven命令是十分有必要的，即使在IDEA等工具给我们提供了图形化界面，但其底层还是依靠maven命令来驱动的。

mvn 的命令格式如下：

```
mvn [plugin-name]:[goal-name]	
```

命令代表的含义：执行plugin-name插件的goal-name目标

### 4.1.常用命令

| 命令                   | 描述                                                    |
| ---------------------- | ------------------------------------------------------- |
| mvn -version           | 显示版本信息                                            |
| mvn clean              | 清理项目生产的临时文件，一般是模块下的target目录        |
| mvn compile            | 编译源代码，一般编译模块下的src/main/java目录           |
| mvn package            | 项目打包工具，会在模块下的target目录生成jar或war等文件  |
| mvn test               | 测试命令，或执行src/test/java下junit的测试用例          |
| mvn install            | 将打包的jar/war文件复制到你的本地仓库中，供其他模块使用 |
| mvn desploy            | 将打包的文件发布到远程参考，提供其他人员进行下载依赖    |
| mvn site               | 生成项目相关信息的网页                                  |
| mvn eclipse:eclipse    | 将项目转换成eclipse项目                                 |
| mvn denpendency:tree   | 打印出项目的整个依赖树                                  |
| mvn archetype:generate | 创建Maven的普通java项目                                 |
| mvn tomcat7:run        | 在tomcat容器中运行web项目                               |
| mvn jetty:run          | 调用Jetty插件的Run目标在JettyServlet容器中启动web应用   |

```
注意：运行maven命令时，首先需要定位到maven项目的目录，也就是项目的pom.xml文件所在的目录，否则，必须以通过参数来指定项目的目录
```

### 4.2.命令参数

​	上面列举的只是比较通用的命令，其他很多命令都可以携带参数执行更加精准的任务

#### 4.2.1. -D传入属性参数

```shell
mvn package -D maven.test.skip=true
```

打包的时候跳过单元测试

#### 4.2.2.-P使用指定的Profile配置 

​	比如项目开发需要多个环境，一般为开发、测试、预发、正式4个环境，在pom.xml中的配置：

​	profiles定义了各个环境的变量id，filters中定义了变量配置文件的地址，其中地址中的环境变量就是上面profile中定义的值，resources中是定义哪些目录下的文件会被配置文件中定义的变量替换

​	通过maven可以实现不同环境打包部署，例如：

```shell
mvn package -Pdev -dMaven.test.skip=true	
```

表示打包本地环境，并跳过单元测试

## 5.IDEA编辑器集成Maven环境

### 5.1.设置Maven版本

选择“File”——>"Other setting"——>"Settings for New Projects..."——>搜索“Maven”

https://blog.csdn.net/AmaniZ/article/details/79284853

## 6.Maven项目创建

### 6.1.创建java项目

#### 6.1.1.新建项目

1. 选择“File”-->"New"-->"Project"

2. 选择Maven，设置JDK版本，选择maven项目的模版

![6.1.1](/Volumes/D/code/Java/MavenLearning/img/6.1.1.png)

3. 设置项目的GroupId（公司和个人名）和ArtifactId（项目名）
4. 检查Maven环境，选择Next
5. 再次检查，并结束初始化
6. 打开项目后，根据需求添加resource目录

#### 6.1.2.编译项目

1. 点击右上角“Add Configurations”，打开“Run/DeBug Configurations”窗口
2. 点击左上角的“+”，选择Maven
3. 设置编译项目的命令
4. 应用并执行

### 6.2.创建Web项目

#### 6.2.1. 创建项目

1. 创建Web项目与创建Java项目步骤基本一致，区别在于选择Maven模版（web项目选择webapp），其他步骤与Java项目一致
2. webapp 用于防止jsp，html等

#### 6.2.2. Web项目修改

1. 修改jdk1.7为1.8

2. 设置单元测试版本为4.12

3. 删除pluginManagement标签

4. 添加web部署的插件

   在build标签中添加plugins标签

   1. Jetty插件

   ```xml
   
   <!-- jetty插件, 设定端口与context path -->
         <plugin>
           <groupId>org.mortbay.jetty</groupId>
           <artifactId>maven-jetty-plugin</artifactId>
           <version>6.1.25</version>
           <configuration>
             <!-- 热部署，每10秒扫描一次 -->
             <scanIntervalSeconds>10</scanIntervalSeconds>
             <!-- 此处为项目的上下文路径 -->
             <contextPath>/test</contextPath>
             <connectors>
               <connector implementation="org.mortbay.jetty.nio.SelectChannelConnector">
               <!--此处配置了访问的端口号 -->
                 <port>9090</port>
               </connector>
             </connectors>
           </configuration>
         </plugin>
   ```

   2. Tomcat 插件

      ```xml
       			<plugin>
                 <groupId>org.apache.tomcat.maven</groupId>
                 <artifactId>tomcat7-maven-plugin</artifactId>
                 <version>2.1</version>
                 <configuration>
                     <!-- 此处为项目的上下文路径 -->
                     <path>/test</path>
                     <!--此处配置了访问的端口号 -->
                     <port>8080</port>
                     <!--字符集编码 -->
                     <uriEncoding>UTF-8</uriEncoding>
                     <!--服务器名称 -->
                     <server>tomcat7</server>
                 </configuration>
             </plugin>
      ```

5. 启动项目

   * 点击右上角“Add Configuration”，打开“Run/Debug Configuration”窗口

   * 点击左上角“+”号，选择“Maven”

   * Jetty插件命令配置

     ```shell
     jetty:run
     jetty:run -Djetty.port =9090 #需要将插件配置中的port标签去掉
     ```

   * 点击启动图标，启动服务

## 7.Maven仓库的基本概念

​	当第一次运行Maven命令的时候，你需要Internet链接，因为它需要从网上下载一些文件。那么它需要从网上下载一些文件。那么它从哪里下载呢？它是从Maven默认的远程库下载的。这个远程库有Maven的核心插件和可供下载的jar文件

对于Maven来说，仓库只分为两类：本地仓库和远程仓库

当Maven根据坐标寻找构件时候，它首先会查看本地仓库，如果本地仓库存在，则会直接使用，如果本地仓库没有，Maven回去远程仓库寻找，发现需要的构件之后，就会下载到本地仓库再使用。如果本地仓库和远程仓库都没有，Maven就会报错。

远程仓库分为三种：中央仓库、私服、其他公共服务库

中央仓库是默认配置下，Maven下载jar包的地方

私服是另一种特殊的远程仓库，为节省带宽和时间，应该在局域网内架设一个私有的仓库服务器，用其代理所有外部的远程仓库，内部的项目还能部署到私服上攻其他项目使用

一般来说，在Maven项目目录下，没有诸如lib/这样用来存放依赖文件的目录。当Maven在执行编译或测试时，如果需要使用依赖文件，它总是基于坐标使用远程仓库的依赖文件。

默认情况下，每个用户在自己的用户目录下都有一个路径名为.m2/repository/的仓库目录。有时候，因为某些原因（比如c盘空间不足），需要修改本地仓库目录地址。

对于仓库路径的修改，可以通过Maven配置文件conf目录下settings.xml来指定仓库路径

```xml
<!--设置到指定目录中，路径的斜杠不要写反-->
<settings>
  <localRepository><!--路径--></localRepository>
</settings>
```

### 7.1.中央仓库

由于原始的本地仓库是空的，maven必须知道至少一个可用的远程仓库，才能执行maven命令的时候下载到需要的构件。中央仓库就是这样一个默认的远程仓库。

maven-model-builder-3.39.jar maven自动的jar中包含了一个超级POM，定义了默认中央仓库的位置。中央仓库包含了2000多个开源项目，接收每天1亿次以上的访问

### 7.2. 私服

私服是一种特殊的远程仓库，它是架设在局域网内的仓库服务，私服代理广域网上的远程仓库，供局域网内的maven用户使用。当maven需要下载构件事，它会去私服中找，如果私服没有，则从外部远程仓库下载，并缓存在私服上，再为maven提供。

此外，一些无法从外部仓库下载的构件也能从本地上传到私服提供局域网中的其他人使用

配置方式：项目pom.xml配置

![7.2](/Volumes/D/code/Java/MavenLearning/img/7.2.png)

公司内部应该建立的私服：

* 节省自己的外网贷带宽
* 加速maven构建
* 部署第三方控件
* 提高稳定性
* 降低中央仓库的负荷

### 7.3. 其他公共库

常用的阿里云仓库配置

![截屏2021-09-23 下午10.39.55](/Volumes/D/code/Java/MavenLearning/img/7.3.png)

### 7.4 如何寻找Maven对应的仓库

https://mvnrepository.com/?__cf_chl_captcha_tk__=pmd_lOcupYtyP3lAHEIdvjpCFQOgIlRM7awnIHSztVP_UdU-1632408082-0-gqNtZGzNAuWjcnBszQal

## 8.Maven环境下构建多模块项目

使用maven提供的多模块构建的特性完成maven环境下多个模块的项目的管理与构建。

```
这里以四个模块为例来搭建项目，以达到通俗易懂的初衷

模块maven_parent --基模块，就是常说的parent（pom）

模块 maven_dao --数据库的访问层，例如jdbc操作（jar）

模块 maven_service --项目的业务逻辑层（jar）

模块 maven_controller --用来接收请求，响应数据（war）
```

### 8.1.创建maven_parent项目

1. 选择File-->New-->Project（不选择模版）
2. 设置GroupId和ArtifactId
3. 设置项目名称以及工作空间

### 8.2.创建maven_dao模块

1. 选择maven_parent，右键选择New，选择Module
2. 选择Maven项目的模版（普通Java项目）
3. 设置子模块的ArtifactId
4. 设置Maven的配置
5. 设置子模块的名称以及存放位置

### 8.3.创建 maven_service 模块

创建maven_service模块的步骤与maven_dao模块一致

### 8.4.创建maven_controller模块

创建maven_service模块的步骤与maven_dao模块基本一致，只需要将第一步选择Maven模版设置为web项目即可（模版类型：maven-archetype-webapp）

### 8.5.修改模块配置

* 设置jdk版本
* 单元测试JUnit版本
* 删除多余的配置

### 8.6. 设置模块之间的依赖

#### 8.6.1.maven_dao

1. 新建包
2. 在包中创建UserDao类
   ![image-20210923231919966](/Volumes/D/code/Java/MavenLearning/img/8.6.1.png)
3. 在类中添加方法

#### 8.6.2.maven_service

1.添加maven_dao的依赖

```xml
<!--加入maven_dao模块的依赖-->
<dependency>
	<groupId>com.xxx</groupId>
	<artifactId>maven_dao</artifactId>
  <version>1.0-SNAPSHOT</version>
</dependency>
```

2. 在项目中添加UserService类，并添加方法

   ![image-20210923232420324](/Volumes/D/code/Java/MavenLearning/img/8.6.2.png)

   #### 8.6.3.maven_controller

   1. 添加maven_service模块的依赖

      ```xml
      <!--加入maven_service模块的依赖-->
      <dependency>
      	<groupId>com.xxx</groupId>
      	<artifactId>maven_service</artifactId>
        <version>1.0-SNAPSHOT</version>
      </dependency>
      ```

   2. 添加Servlet的依赖

      ```xml
      <!--Servlet的依赖-->
      <dependency>
      	<groupId>javax.servlet</groupId>
        <artifactId>javax.servlet-api</artifactId>
        <version>3.0.1</version>
        <scope>provided</scope>
      </dependency>
      ```

   3. 新建Java类，继承HttpServlet类，并重写service方法

      ![image-20210923233232568](/Volumes/D/code/Java/MavenLearning/img/8.6.3.png)

   4. 添加Tomcat插件

      

      

   
