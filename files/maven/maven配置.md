## Maven 配置

### 1. settings.xml文件

settings.xml配置文件用来配置**Maven**全局参数配置文件，pom.xml是文件所在项目的局部配置文件

```xml
<?xml version="1.0" encoding="UTF-8"?>

<!--
 | 这是Maven的配置文件。可以在两个级别指定：
 |	
 |  1. 用户级别。此settings.xml文件为单个用户提供配置，
 |     通常以${user.home}/.m2/settings.xml格式提供。
 |
 |  2. 全局级别。此settings.xml文件为所有Maven提供配置，
 |     通常以${maven.conf}/settings.xml格式提供。
 |-->
  <!-- settings标签为配置文件的根标签-->
<settings xmlns="http://maven.apache.org/SETTINGS/1.0.0"
          xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
          xsi:schemaLocation="http://maven.apache.org/SETTINGS/1.0.0 http://maven.apache.org/xsd/settings-1.0.0.xsd">
  <!-- localRepository
   | 指定本地仓库存储路径，可以指定路径
   | 默认路径: ${user.home}/.m2/repository
   <localRepository>/path/to/local/repo</localRepository>
  -->
<localRepository>E:\maven-repository</localRepository>
  <!-- interactiveMode
	 设置maven是否需要和用户交互以获得输入
     默认值: true
     <interactiveMode>true</interactiveMode>
  -->

  <!-- offline
	设置maven是否需要在离线模式下运行
    默认值: false
    <offline>false</offline>
  -->

  <!-- pluginGroups
   这是一个附加组标识符的列表，当通过它们的前缀来解析插件时，这些标识符将被搜索。
   调用类似“mvn prefix:goal”这样的命令行时，Maven将自动添加组标识符
   如果这些还不在列表中，调用"org.apache.maven.plugins" and "org.codehaus.mojo"
   |-->
  <pluginGroups>
    <!-- pluginGroup
     指定用于插件查找的进一步组标识符
     <pluginGroup>com.your.plugins</pluginGroup>
    -->
  </pluginGroups>

  <!-- proxies
	配置不同的代理
   |-->
  <proxies>
    <!-- proxy
     | 配置一个用于连接的代理
     |
    <proxy>
      <id>optional</id>
      <active>true</active>
      <protocol>http</protocol>
      <username>proxyuser</username>
      <password>proxypass</password>
      <host>proxy.host.net</host>
      <port>80</port>
      <nonProxyHosts>local.net|some.host.com</nonProxyHosts>
    </proxy>
    -->
  </proxies>

  <!-- servers
   这是一个身份验证配置文件列表，由系统中使用的服务器id作为键值。
   无论何时maven必须连接到远程服务器，都可以使用|身份验证配置文件。
   -->
  <servers>
    <!-- server
     指定连接到特定服务器时使用的身份验证信息
     系统内唯一的名称(由下面的“id”属性引用)。
     注意:您应该指定 username/password OR privateKey/passphrase, 为这些配对是一起使用。
    <server>
      <id>deploymentRepo</id>
      <username>repouser</username>
      <password>repopwd</password>
    </server>
    -->
    <!-- 通过privateKey/passphrase配置
    <server>
      <id>siteServer</id>
      <privateKey>/path/to/private/key</privateKey>
      <passphrase>optional; leave empty if not used.</passphrase>
    </server>
    -->
  </servers>

  <!-- mirrors
   这是列表用于从远程存储库下载的镜像列表
   -->
  <mirrors>
    <!-- mirror
    <mirror>
      #指定镜像的唯一标识符。id用来区分不同的mirror元素
      <id>mirrorId</id> 
	  #被镜像的服务器的id
      <mirrorOf>repositoryId</mirrorOf> 
      #镜像名称
      <name>Human Readable Name for this Mirror.</name>
      #镜像URL
      <url>http://my.repository.com/repo/path</url>
    </mirror>
     -->
	 
		<mirror>

		<id>nexus-aliyun</id>

		<mirrorOf>*</mirrorOf>

		<name>Nexus aliyun</name>

		<url>http://maven.aliyun.com/nexus/content/groups/public</url>

		</mirror>
  </mirrors>

  <!-- profiles
   根据环境参数来调整构建配置的列表。
   -->
  <profiles>
    <!-- profile
    可以通过<activatedProfiles/>指定使用的构建环境
	或者通过命令行指定构建环境
   
    <profile>
      <id>jdk-1.4</id>  #id
      <activation>
        <jdk>1.4</jdk> #指定激活的profile
      </activation>

      <repositories>
        <repository>
          <id>jdk14</id>
          <name>Repository for JDK 1.4 builds</name>
          <url>http://www.myhost.com/maven/jdk14</url>
          <layout>default</layout>
          <snapshotPolicy>always</snapshotPolicy>
        </repository>
      </repositories>
    </profile>
    -->
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
  </profiles>

  <!-- activeProfiles
   指定激活的profile
  <activeProfiles>
    <activeProfile>alwaysActiveProfile</activeProfile>
    <activeProfile>anotherAlwaysActiveProfile</activeProfile>
  </activeProfiles>
  -->
</settings>

```



### 2. POM.xml文件

完整POM.xml介绍:[pom.xml官方文档]( https://maven.apache.org/ref/3.6.3/maven-model/maven.html )

```xml
<!-- project 根目录-->
<project xmlns="http://maven.apache.org/POM/4.0.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
  xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 https://maven.apache.org/xsd/maven-4.0.0.xsd">
  <!--模型版本。值4.0.0，maven2.0必须是这样写，现在是maven2唯一支持的版本 -->
  <modelVersion>4.0.0</modelVersion>
 
  <!--指定父项目的位置（如果存在）。如果未指定父项目中的值，则它们将是此项目的默认值。
 		指定父项目groupId，artifactId，version
  -->
  <parent>
        <groupId>org.springframework.boot</groupId>
        <artifactId>spring-boot-starter-parent</artifactId>
        <version>2.2.6.RELEASE</version>
        <relativePath/>
  </parent>
  
  <!--组织通用唯一标识符。使用完全限定的包名将其与具有类似名称的其他项目 -->
 <groupId>xxx</groupId>
  <!--在groupId下，项目的唯一标识-->  
  <artifactId>xxx</artifactId>
  <!-- 项目的当前版本 --> 
  <version>0.0.1-SNAPSHOT</version>
  <!-- 项目打包方式 jar|war|pom 默认:jar -->
  <packaging>jar</packaging>
  <!-- 项目全名 -->
  <name>xxx</name>
  <!--项目描述-->
  <description></description>
  <!-- 项目主页访问url -->
  <url/>
 
  	<!-- 多module项目的聚合关系设置 -->
    <modules>
    	<module></module>
        ...
    </modules>
  <!--设置属性值，供其他地方引用-->
  <properties>
    <key>value</key>
  </properties>
 <!-- 对依赖的jar版本进行管理，不会实际引入jar-->
  <dependencyManagement>
    <!--依赖管理 -->
    <dependencies>
      <!-- 具体某个依赖的信息-->
      <dependency>
        <groupId/>
        <artifactId/>
        <version/>
        <!--设置依赖的类型-->
        <type/>
        <!--来帮助定义构件输出的一些附属构件 -->
        <classifier/>
        <!--设置依赖范围，默认:compile
			compile:表示jar包会在编辑和打包的时候都引入
            provided:表示jar包在编译和测试的时候引入，打包时不引入;例如servlet-api.jar
            runtime:运行时依赖，编译时不依赖;例如jdbc驱动包
            system:provided相同,依赖项不从maven仓库获取，从本地文件系统获取。通过systemPath来设置
            test:表示在测试范围有效，编译和打包不引入
            import:只能在<dependencyManagement>节中的使用。从其他POM文件中导入dependency配置。
		-->
        <scope/>
        <!--当score=system 设置引入的本地文件路径 -->
        <systemPath/>
        <!--排除依赖-->
        <exclusions>
          <exclusion>
            <artifactId/>
            <groupId/>
          </exclusion>
        </exclusions>
        <optional/>
      </dependency>
    </dependencies>
  </dependencyManagement>
    
  <!--引入依赖的jar包-->  
  <dependencies>
    <dependency>
      ...<!--同dependencyManagement中的dependencies-->
    </dependency>
  </dependencies>
    
  <!--生成项目所需信息-->
  <build>
    <!--指定项目源码路径(相对路径)。根据指定的目录进行编译。默认：src/main/java -->
    <sourceDirectory/>
    <!--指定项目脚本源码路径(相对路径)。默认：src/main/scripts -->
    <scriptSourceDirectory/>
    <!--指定项目单元测试路径(相对路径)。在项目测试时编译源码。默认：src/test/java -->
    <testSourceDirectory/>
    <!--已编译的类所在的目录。默认值是target/classes-->
    <outputDirectory/>
    <!--已编译的测试类所在的目录。默认值是target/test-classes -->
    <testOutputDirectory/>
    
   <!--描述所有类路径资源，如与项目关联的属性文件。默认值是src/main/resources。 -->
    <resources>
      <resource>
        <targetPath/>
        <filtering/>
        <directory/>
        <includes/>
        <excludes/>
      </resource>
    </resources>
    <!--放置生成的所有文件的目录。默认值为target。-->  
    <directory/>
    <!--生成的项目名。默认值是${artifactId}-${version}。 -->
    <finalName/>
    <!-- 加入使用的插件-->
    <plugins>
      <plugin>...</plugin>
    </plugins>
  </build>
 <!--设置激活指定环境配置 -->
  <profiles>
    <profile>
     </profile>
  </profiles>
</project>
```

### 3. maven 依赖管理

- 依赖传递性

- 依赖优先原则

  - **依赖最短路径优先原则**  当多个依赖同时依赖同一个jar，选择依赖路径最短的jar
  - **pom文件中申明顺序优先** pom文件中使用先申明的
  - **覆写优先**  子pom申明优先于父pom

- 可选依赖

   任何可传递的依赖可以被标记为可选的，通过使用 "optional" 元素。例如：A 依赖 B， B 依赖 C。因此，B 可以标记 C 为可选的， 这样 A 就可以不再使用 C。 

- 排除依赖

   任何可传递的依赖都可以通过 "exclusion" 元素被排除在外。举例说明，A 依赖 B， B 依赖 C，因此 A 可以标记 C 为 "被排除的"。 

- **依赖范围**

  - **compile**:表示jar包会在编辑和打包的时候都引入。默认值
  - provided:表示jar包在编译和测试的时候引入，打包时不引入;例如servlet-api.jar
  - runtime:运行时依赖，编译时不依赖;例如jdbc驱动包
  - system:provided相同,依赖项不从maven仓库获取，从本地文件系统获取。通过systemPath来设置
  - test:表示在测试范围有效，编译和打包不引入
  - import:只能在<dependencyManagement>节中的使用。从其他POM文件中导入dependency配置。



### 4. maven 项目继承与聚合

- 项目继承

  继承是指子工程直接继承父工程 当中的属性、依赖、插件等配置，避免重复配置。通过<parent>标签进行配置。子工程可以进行重写属性，依赖，插件等配置

- 项目聚合

  将多个模块整合在一起，统一构建，避免一个一个的构建。聚合需要个父工程，然后使用 <modules> 进行配置其中对应的是子工程的相对路径 。

  ```xml
  <modules>
  	<module>project-A</module>
      <module>project-B</module>
      <module>project-C</module>
  </modules>
  ```

  

### 5. maven 构建生命周期

maven有三个标准生命周期

- **clean**   项目清理 

- **default/bulid** 项目部署

- **site**  项目站点文档创建的处理 

  

**default生命周期**

开始-> validate（验证） -> **compile（编译）** -> **test（单元测试）** ->**package（打包）** -> verify（检查） -> **install（安装）** -> **deploy（部署）**

### 6. maven常用命令

1.mvn clean  清空项目的class文件、jar文件等( 清空target目录)

2.mvn compile 编译源代码(target目录生成class文件)

3.mvn install  在本地repository中安装jar（包含mvn compile，mvn package，然后上传到本地仓库）

4.mvn deploy  上传到私服(包含mvn install,然后，上传到私服)

5.mvn package   打包（项目打包，在target目录生成一个pom中指定打包格式的文件。包含mvn test）

6.mvn test      运行测试

7.mvn site   产生site

8.mvn test-compile  编译测试代码

9.mvn -Dtest package 只打包不测试

10.mvn jar:jar  只打jar包

11.mvn test -skipping compile -skipping test-compile 只测试而不编译，也不测试编译

12.mvn source.jar  源码打包