## 开发平台后端框架参考指南

### 作者

苗世鹏、唐红石、罗明强

### 版本

0.0.1-SNAPSHOT

## 1.文档简介

本节主要是开发平台后端框架参考指南的一个概述，你可以把它想象成本文档的一个内容索引。你可以顺序的阅读本文档，也可以跳过本节，如果你对本节没有兴趣的话。

### 1.1 关于本文档

开发平台后端框架参考指南最新版本发布地址：[https://chamc-devplatform.github.io/chamc-boot-starter-reference/](https://chamc-devplatform.github.io/chamc-boot-starter-reference/) ，本文档的副本你可以随便下载或分享给他人。

### 1.2 获取帮助

关于开发平台后端框架的任何问题，我们都乐于提供帮助！
- 查看[How-to](#how-to)章节，你可以找到大部分问题的答案；
- 发送邮件给[我](mailto:luomingqiang@chamc.com.cn)、[苗世鹏](mailto:miaoshipeng@chamc.com.cn) 或 [唐红石](mailto:tanghongshi@chamc.com.cn)；
- 电话给我、苗世鹏或唐红石，电话号码可在公司通讯录里查询，具体路径：华融资产-子公司-华融融通-软件开发部。

### 1.3 开始步骤

如果你刚开始使用开发平台后端框架，那么[这章](#get-start)应该对你很有帮助！

### 1.4 开发平台后端框架组件

如果你对开发平台后端框架已经有了初步的了解，想要进一步的了解与使用，那么[这章](#component)将为你详细介绍开发平台后端框架的各个组件：[web组件](#web)、[swagger组件](#swagger)、[工作流组件](#bpm)。

### 1.5 高级功能

## <span id="get-start">2 入门</span>

如果你刚开始使用开发平台后端框架，那么本节内容会对你有很大帮助！本节主要回答基本的“what”、“how”和“why”问题，以及一个简单的使用说明。然后我们会构建第一个基于开发平台后端框架的应用。

### 2.1 开发平台后端框架介绍

1. 简介    
开发平台后端框架基于Spring实现，只需引入依赖便可使用。
2. 系统要求  
开发平台后端框架使用的Spring Boot的版本为：Spring Boot 1.5.4.RELEASE；JDK版本为：jdk1.8；MAVEN版本为：maven3.5.0。

### 2.2 环境安装

使用开发平台后端框架需要以下环境：  

- [jdk1.8](#jdk)
- [maven3.5.0](#maven)
- [spring tool suite](#sts)  

以上软件都可通过 [公司网盘](http://hq-spsdocument/Documents/Forms/AllItems.aspx?RootFolder=%2FDocuments%2F4-%E8%BD%AF%E4%BB%B6%E5%BC%80%E5%8F%91%E9%83%A8%2F%E5%9F%B9%E8%AE%AD%2F171013-SpringMVC%E5%92%8CJPA%E5%9F%BA%E7%A1%80-%E7%BD%97%E6%98%8E%E5%BC%BA%2F%E8%BD%AF%E4%BB%B6) 获得。

#### <span id="jdk">2.2.1 jdk的安装配置</span>

##### 1. 安装jdk
根据安装提示进行安装。**注意：安装路径不要包含中文、空格、特殊字符** 
##### 2. 配置环境变量  

1) 新增环境变量JAVA_HOME 
<pre>例：C:\Program Files\Java\jdk1.8.0_131</pre> 
  
![](https://i.imgur.com/49uVnkH.png)  

2) 新增环境变量path(最好将其放在第一位)  
<pre>例：C:\Program Files\Java\jdk1.8.0_131\bin;C:\Program Files\Java\jdk1.8.0_131\jre\bin;</pre>
 
![](https://i.imgur.com/d3H1T7E.png)

3） 新增环境变量CLASSPATH  
<pre>例：.;%JAVA_HOME%\lib;%JAVA_HOME%\lib\tools.jar</pre>

![](https://i.imgur.com/xd78npM.png)

##### 3. 在cmd中执行java -version,若出现下图则安装成功  

![](https://i.imgur.com/k5g3ZUa.png)

#### <span id="maven">2.2.2 maven的安装配置</span>

##### 1. 解压apache-maven-3.5.0-bin.zip到某个目录（例如D盘） **注意：解压路径不要包含中文、空格、特殊字符**  
##### 2. 设置环境变量  
1） 新建系统变量  MAVEN_HOME  变量值：D:\apache-maven-3.5.0  

![](https://i.imgur.com/KcBDyNb.png)

2） 编辑系统变量  Path  添加变量值：;%MAVEN_HOME%\bin  

![](https://i.imgur.com/hiaMCLH.png)

##### 3. 打开命令行，输入 mvn --version，若出现以下情况则配置成功。 

![](https://i.imgur.com/yY62UDa.png)

##### 4. 在maven目录下的conf文件夹的settings.xml中加入：  
  
1） 在`<proxies>`标签中加入代理：  

	<proxy>  
		<id>optional</id>  
		<active>true</active>  
		<protocol>http</protocol>  
		<username></username>  
		<password></password>  
		<host>10.80.2.4</host>  
		<port>80</port>  
		<nonProxyHosts>local.net|some.host.com</nonProxyHosts>  
	</proxy>

2） 在`<profiles>`标签中加入：  

	<profile>  
		<id>jdk-1.8</id>  
		<activation>  
			<activeByDefault>true</activeByDefault>  
			<jdk>1.8</jdk>  
		</activation>  
		<properties>  
			<maven.compiler.source>1.8</maven.compiler.source>  
			<maven.compiler.target>1.8</maven.compiler.target>  
			<maven.compiler.compilerVersion>1.8</maven.compiler.compilerVersion>  
		</properties>  
	</profile>  
  
3） 在`<activeProfiles>`标签中添加：  

   `<activeProfile>jdk-1.8</activeProfile>`
		
#### <span id="sts">2.2.3 spring tool suite的安装配置</span>

##### 1. STS的安装

1） 解压 spring-tool-suite-3.8.4.RELEASE-e4.6.3-win32-x86_64.zip （**注意：解压路径不要包含中文、空格、特殊字符**）  
2） 打开 sts-3.8.4.RELEASE 的 STS.exe ，即可使用  
  
##### 2. STS的配置

1） Maven配置  
  
- 打开STS，进入windows —》Preferences —》Maven —》Installations。  
- 点击Add...选择Maven的所在目录。  
 
![1](https://i.imgur.com/ilpB3Wu.png)  

- 勾选这个Maven，并点击Apply。    

![2](https://i.imgur.com/oMYGNrY.png)  

- 选择User Settings，将设置User Settings为自己的settings.xml，OK。  
		
![3](https://i.imgur.com/1quxhE5.png)  

2） JDK配置

- 打开STS，进入windows —》Preferences —》Java —》Installed JREs。  

![4](https://i.imgur.com/MZgsUFu.png)  

- 选中jdk，选择Edit...。将jdk改为指向jdk的目录（**而不是jre**），Finish。 

![5](https://i.imgur.com/W8hkZp6.png)

3） <span id="daili">配置代理（可不配）</span>  

- 打开 windows —》Preferences —》Network Connections，配置如图所示。

![](https://i.imgur.com/UktUnq1.png)

### 2.3 第一个demo

#### 2.3.1 新建项目（两种方法）
##### 1. 在STS中新建项目 （此方法需[配代理](#daili)）
1） 打开STS，File —》New —》Spring Starter Project  

![](https://i.imgur.com/yorOwni.png)

2） 填写信息，Next —》Finish。在STS中可见此项目，如下。**注意：项目group应为 com.chamc**  

![](https://i.imgur.com/IwqTOoy.png) 

![](https://i.imgur.com/KCFKonw.png)

##### 2. 在官网新建项目
1） 打开[https://start.spring.io/](https://start.spring.io/)，填入Group和Artifact，可添加一些依赖（例如：mysql等），点击Generate Project，将自动下载一个压缩包。**注意：项目group应为 com.chamc**  

![](https://i.imgur.com/xogLRCi.png)

2） 解压压缩包，因为父工程的版本为spring boot 1.5.4，此处最好将工程的版本改为1.5.4，打开/demo-1/pom.xml文件，修改如图所示。

![](https://i.imgur.com/Re76Sva.png)

3） 打开STS，File —》import... —》Maven —》Existing Maven Projects —》next>。  

![](https://i.imgur.com/KQ36uFH.png)

4） 选择项目的路径，finish。在STS中可见此项目，如下。  

![](https://i.imgur.com/Mej1yAz.png)

![](https://i.imgur.com/D5xYDkh.png)

##### 3. 添加依赖

1） 打开pom.xml在`<dependencies>`标签中添加开发平台web组件依赖，若没有后端开发平台框架组件请先[获取](#get-web)  

	<dependency>
		<groupId>com.chamc.boot</groupId>
		<artifactId>chamc-boot-starter-web</artifactId>	
		<version>0.0.1-SNAPSHOT</version>		
	</dependency>

2） 在`<plugins>`中添加插件

	<plugin>
		<groupId>com.mysema.maven</groupId>
		<artifactId>apt-maven-plugin</artifactId>
		<version>1.1.3</version>
		<executions>
			<execution>
				<goals>
					<goal>process</goal>
				</goals>
				<configuration>
					<outputDirectory>src/main/querysdl</outputDirectory>
					<processor>com.querydsl.apt.jpa.JPAAnnotationProcessor</processor>
				</configuration>
			</execution>
		</executions>
	</plugin>

3） 右键项目选择Maven —》update project...。此时可能还会报错，这是因为没有安装lombok，请执行下一步操作。  
4） 在maven dependencies中找lombok.jar所在路径，在其路径下找到它并安装。安装成功后，右键项目Maven —》update project...。（安装一次即可）  

![](https://i.imgur.com/f1vvl29.png)

![](https://i.imgur.com/YGYzCw4.png)

##### 4. 开始编码

1） 在application.properties中添加数据库信息（MySQL数据库安装包可通过[公司网盘](http://hq-spsdocument/Documents/Forms/AllItems.aspx?RootFolder=%2FDocuments%2F4-%E8%BD%AF%E4%BB%B6%E5%BC%80%E5%8F%91%E9%83%A8%2F%E5%9F%B9%E8%AE%AD%2F171013-SpringMVC%E5%92%8CJPA%E5%9F%BA%E7%A1%80-%E7%BD%97%E6%98%8E%E5%BC%BA%2F%E8%BD%AF%E4%BB%B6)获得）  

![](https://i.imgur.com/acl5F7C.png)

2） 在mysql中建一个数据库**（注意：如果要使用代码生成功能，建表时，每个表必须有一个主键id，并且auto_increment）**例如：  

![](https://i.imgur.com/KN2eVWi.png)

![](https://i.imgur.com/diMhiYW.png)

![](https://i.imgur.com/blvD7uf.png)

3） 生成代码，新建一个generate包，新建一个Generator类，添加一个main方法，使用CodeGenerator.generate(……)。右键run as java application  

![](https://i.imgur.com/16HnSPI.png)

右键项目refresh一下，可见下图所示。  

![](https://i.imgur.com/eucG6TS.png)

4） 生成的controller不是rest接口，若想改为rest接口，将@Controller改为@RestController，将继承的BaseController改为BaseRestController，如下图所示。

![](https://i.imgur.com/l7fXK7U.png)

##### <span id="get-web">5. 获取组件</span>

1） 【方法一】配置Maven仓库  

- 在pom.xml文件中加入远程仓库配置

		<repositories>
			<repository>
				<id>Nexus</id>
				<name>Nexus</name>
				<url>http://10.1.8.147:8081/nexus/content/groups/public/</url>
			</repository>
		</repositories>

- 修改setting.xml文件

1.在maven的安装目录下找到settings文件，maven目录\conf\settings.xml。  
2.在`<mirrors></mirrors>`里加入：  

	<mirror>
		<id>nexus-200</id>
		<mirrorOf>*</mirrorOf>
		<url>http://10.80.38.200:8081/repository/maven-public/</url>
	</mirror>

3.在`<profiles></profiles>`里加入：  

	<profile>
		<id>nexus-200</id>
		<repositories>
			<repository>
			<id>central</id>
			<url>http://central</url>
			<releases><enabled>true</enabled></releases>
			<snapshots><enabled>true</enabled></snapshots>
			</repository>
		</repositories>
		<pluginRepositories>
			<pluginRepository>
				<id>central</id>
				<url>http://central</url>
				<releases><enabled>true</enabled></releases>
				<snapshots><enabled>true</enabled></snapshots>
			</pluginRepository>
		</pluginRepositories>
	</profile>

4.在`<activeProfiles></activeProfiles>`里加入：（**注意：`<profiles>`里有啥加啥，加的是`<profile>`里的`<id>`**）  

	<activeProfile>jdk-1.8</activeProfile>
	<activeProfile>nexus-200</activeProfile>

5.将配置的代理注释掉。

![](https://i.imgur.com/LF0UmZR.png)

2） 【方法二】下载jar包到本机的maven仓库

### 2.4 关于数据库操作的一些介绍

## <span id="component">3 开发平台后端框架组件</span>

### <span id="web">3.1 web组件</span>

#### 3.1.1 配置多数据源及其使用说明
- 1. 简介
- 2. 配置
- 3. demo

#### 3.1.2 配置主从及其使用说明
- 1. 简介
- 2. 配置
- 3. demo

#### 3.1.3 配置单点登录及其使用说明
- 1. 简介
- 2. 配置
- 3. demo

#### 3.1.4 配置日志打印及其使用说明
- 1. 简介
- 2. 配置
- 3. demo

### <span id="swagger">3.2 swagger组件</span>
- 1. 简介
- 2. 配置
- 3. demo

### <span id="bpm">3.3 工作流组件</span>

## <span id="how-to">4 “How-to”指南</span>

## 6 附录


