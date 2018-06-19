# 1、spring的简介
---  方炯翊

--- 2018/5/27
## 1.1什么是spring？

	 Spring是一个开源框架，Spring是于2003 年兴起的一个轻量级的Java 开发框架，由Rod 
     Johnson 在其著作Expert One-On-One J2EE Development and Design中阐述的部分理念
     和原型衍生而来。它是为了解决企业应用开发的复杂性而创建的。框架的主要优势之一就是其分层
     架构，分层架构允许使用者选择使用哪一个组件，同时为 J2EE 应用程序开发提供集成的框架。
     Spring使用基本的JavaBean来完成以前只可能由EJB完成的事情。然而，Spring的用途不仅限于
     服务器端的开发。从简单性、可测试性和松耦合的角度而言，任何Java应用都可以从Spring中受
     益。Spring的核心是控制反转（IoC）和面向切面（AOP）。简单来说，Spring是一个分层的
    JavaSE/EE full-stack(一站式) 轻量级开源框架。


##  1.2功能模块 

	   Spring由多个模块组成，它们可以分为核心容器（Core Container）、数据访问/集成（Data 
      Access/Integration）、Web、面向切面编程（AOP, Aspect Oriented Programming）、设
      备（Instrumentation）、消息发送（Messaging）和测试（Test）。


##   1.3 spring的核心

     Spring的核心是控制反转（IoC）和面向切面（AOP）


##  1.4spring的优点


    方便解耦，简化开发  （高内聚低耦合）
		•Spring就是一个大工厂（容器），可以将所有对象创建和依赖关系维护，交给Spring管理
		•spring工厂是用于生成bean
	AOP编程的支持
		•Spring提供面向切面编程，可以方便的实现对程序进行权限拦截、运行监控等功能
		声明式事务的支持
		•只需要通过配置就可以完成对事务的管理，而无需手动编程
	方便程序的测试
		•Spring对Junit4支持，可以通过注解方便的测试Spring程序
	方便集成各种优秀框架
		•Spring不排斥各种优秀的开源框架，其内部提供了对各种优秀框架（如：Struts、Hibernate、MyBatis、Quartz等）的直接支持
	降低JavaEE API的使用难度
		•Spring 对JavaEE开发中非常难用的一些API（JDBC、JavaMail、远程调用等），都提供了封装，使这些API应用难度大大降低



##  下载源代码
		http://repo.spring.io/release/org/springframework/spring/ 


#   2、IOC
##什么是IOC？


    控制反转是一个重要的面向对象编程的法则来削减计算机程序的耦合问题，也是轻量级的spring框
    架的核心。控制反转一般分为两种类型，依赖注入（DI）和依赖查找。依赖注入应用比较广泛，它是
    spring框架的核心。
	
     Ioc不是什么技术，而是一种设计思想。在java开发中，ioc意味着将你设计好的对象交给容器控
     制，而不是传统的在你的对象内部直接控制。理解好ioc的关键需要明确“谁控制谁，控制什么，为
     何是反转，那些方面反转了”
	 谁控制谁，控制什么：在传统的JavaSE程序设计中，我们直接通过对象内部通过new进行创建对象，是程序主动去创建依赖对象；而ioc是有专门的容器来创建这些对象，由ioc容器来控制对象
     的创建。Ioc容器控制了对象，主要控制了外部资源的获取（不只是对象，包括文件等）
     为何是反转，那些方面反转了：传统的应用程序是由我们自己在对象中主动控制去直接获取依赖对
     象，也就是正转；反转则是由容器来帮忙创建及注入依赖对象；由于是容器帮我们查找及注入依赖
     对象，对象只是被动的接受依赖对象，所以是反转；那个方面反转了？依赖对象的获取被反转了。


##  2.2 Ioc能干做什么

    它能指导我们如何轻松的设计出松耦合，更优良的程序。传统应用程序都是由我们在类的内部主动创
    建依赖对象，从而导致类与类之间高耦合，难于测试；IOC把创建和查找依赖对象的控制权交给了容
    器，由容器进行注入组合对象，所以对象与对象之间是松散耦合，这样就方便测试，利于功能复
    用，使得程序的整个体系变得非常灵活。
    Ioc对编程带来的最大改变不是从代码上，而是从思想上，发生了“主从换位”的变化。应用程序原本
    是老大，要获取什么什么资源都是主动出击，在ioc思想中，应用程序变的被动了，被动的等待ioc
    容器来创建并注入它所需要的资源；“别找我们，我们找你”即由ioc容器帮对象找相应的依赖对象
    并注入，而不是由对象主动去找。

####Ioc的优点：
     ioc的最大好处就是把对象生成放在xml里面定义，所以当我们需要换一个实现子类将变得很简单
     （一般这样的对象都是实现与某种接口的），只需要修改xml就可以了，这样我们甚至可以实现对
    象的热插拔。
####Ioc的缺点：
     （1）生成一个对象的步骤变复杂了。（2）对象生成使用反射编程，在效率上有损耗。相对于ioc提
     高的维护性和灵活性来说，这点损耗是微不足道的，除非某对象的生成对效率的要求特变的高。
     （3）缺少ide重构操作的支持，修改类名，需要去xml文件中手动修改。








# 2.3 入门案例

### 2.3.1 添加依赖


		<!--spring依赖包-->
		    <dependency>
		      <groupId>org.springframework</groupId>
		      <artifactId>spring-context</artifactId>
		      <version>4.3.14.RELEASE</version>
		</dependency>



### 2.3.2 编写创建配置文件

		<?xml version="1.0" encoding="UTF-8"?>
		<beans xmlns="http://www.springframework.org/schema/beans"
		       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
		       xsi:schemaLocation="http://www.springframework.org/schema/beans
		                           http://www.springframework.org/schema/beans/spring-beans.xsd">
		
		    <bean id="person" class="net.togogo.Person">
		        <property name="name" value="张三"/>
		    </bean>



    
      <!--<bean id="dog1" class="net.togogo.bean.Dog">-->
        <!--<constructor-arg name="name" value="张三"></constructor-arg>-->
             <!--<constructor-arg name="age" value="3"></constructor-arg>-->

          <!---->
      <!--</bean>-->

		</beans>





###  2.3.4 编写测试类
           //使用ioc容器管理对象
	    @Test
	   public void testSys2(){
	    //读取配置文件
	       ApplicationContext  applicationsContext =new ClassPathXmlApplicationContext("ApplicationContext.xml");
	       Dog dog= (Dog) applicationContext.getBean("dog1");
	
	       dog.sys();
	
	   }




#---------------------------------------------------------------

##  二.当用一个对象是另外一个对象的属性时候的使用


      <!--当一个对象调用另外一个对象的时候，只需要调用对象在容器中注册的名字就可以了-id即为名字 -->
      <bean id="dog1" class="net.togogo.bean.Dog">
        <constructor-arg name="name" value="张三"></constructor-arg>
             <constructor-arg name="age" value="3"></constructor-arg>
          <property name="car" ref="car1"></property>


      </bean>


    <bean id="car1" class="net.togogo.bean.Car">

        <constructor-arg name="name" value="奔驰"></constructor-arg>
        <constructor-arg name="color" value="green"></constructor-arg>
    </bean>


##  三.生命周期

    //等会通过这两个方法来观察对象的生命周期
    public void createBean(){

        System.out.println("对象被创建");

    }

    public void destroyBean(){

        System.out.println("对象对象被销毁");
    }



   <!--当一个对象调用另外一个对象的时候，只需要调用对象在容器中注册的名字就可以了-id即为名字 -->
      <bean id="dog1" class="net.togogo.bean.Dog" init-method="createBean" destroy-method="destroyBean">
        <constructor-arg name="name" value="张三"></constructor-arg>
             <constructor-arg name="age" value="3"></constructor-arg>
          <property name="car" ref="car1"></property>


      </bean>






#  添加日志文件


###  1.添加依赖

    <!--日志依赖-->
    <dependency>
      <groupId>log4j</groupId>
      <artifactId>log4j</artifactId>
      <version>1.2.17</version>
    </dependency>

    <!--日志格式化包-->
    <dependency>
      <groupId>commons-logging</groupId>
      <artifactId>commons-logging</artifactId>
      <version>1.2</version>
    </dependency>

###  2.添加日志配置文件      log4j.properties
  

	###direct log messages to stdout ###
	log4j.appender.stdout=org.apache.log4j.ConsoleAppender
	log4j.appender.stdout.Target=System.err
	log4j.appender.stdout.layout=org.apache.log4j.PatternLayout
	log4j.appender.stdout.layout.ConversionPattern=%-d{yyyy-MM-dd HH:mm:ss} [ %t:%r ] - [ %p ] %m%n
	### direct messages to file mylog.log###
	log4j.appender.file=ogr.apache.log4j.FileAppender
	log4j.appender.file.File=D:/my_log.log
	log4j.appender.file.layout=org.apache.log4j.PatternLayout
	log4j.appender.file.layout.ConversionPattern=%-d{yyyy-MM-dd HH:mm:ss} [ %t:%r ] - [ %p ] %m%n
	###set log levels - for more verbose logging change 'info' to 'debug'###
	log4j.rootLogger=off,stdout


###  3.启用日志功能
     
    Logger logger=Logger.getLogger(DogTest.class);










