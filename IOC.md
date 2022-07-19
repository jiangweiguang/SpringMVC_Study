# 1.容器及相关概念

## 1.1 组件、框架、容器

### 组件

实现特定功能、符合某种规范的类集合。

### 框架

框架一般包含具备结构关系的多个组件，这些组件类相互协作构成特定的功能。

### 容器

JAVA开发的框架，包含一个IOC类型的Bean管理容器，另外还提供切面编程（AOP）、数据访问事务管理等组件。

## 1.2  JavaBean、POJO和EJB简介

### JavaBean对象

1. 定义
   - 公共作用域类：为了提供给其他类使用
   - 有默认的无参构造函数：让框架和容器可以使用反射机制进行实例化
   - 需要被序列化且实现Serializable接口：通过序列化或反序列化进行对象的传输或保存到文件中
   - 可能有一系列读写属性、通过getter或setter方法存取属性值：不暴露属性，或容器可以通过反射机制来进行属性值的读写。

### POJO（简单Java对象）

1. 定义：
   - 没有继承任何类，也没有实现任何接口，不需要遵从框架的定义，更没有被其他框架侵入的Java对象

### EJB（企业JavaBean对象）

1. 三种类型：
   - Session Bean
   - Entity Bean
   - MessageDriven Bean

## 1.3 IOC与DI简介

1. IOC本质上是将耦合从代码中转移到配置文件中。容器在启动时依据依赖配置生成依赖对象并注入。
2. DI依赖注入，依赖对象通过注入进行创建，由容器负责组件的创建和注入。
3. IOC是是一种软件设计思想，DI是这种思想的一种实现。



# 2. Spring容器初始化

## 2.1 BeanFactory和 ApplicationContext

使用ApplicationContext优先，如果是Web项目，则使用WebApplicationContext，后者增加了对于Web开发的支持。

### BeanFactory

1. IOC容器的核心接口
2. 职责：实例化、定位、配置应用程序中的对象及建立这些对象的依赖；

### ApplicationContext

1. BeanFactory的实现，称为应用上下文。
2. 具有新功能：
   1. MessageSource：用于信息的国际化显示
   2. ResourceLoader：用于资源加载
   3. ApplicaitonEventPublisher：用于应用事件处理

## 2.2 ApplicaitonContext初始化方法

1. Spring中使用“classpath：”表示类的根路径，加上*，则除了自身的类路径之外，还会查找依赖库（.jar)下的目录。

2. 容器初始化方式：

   1. 配置文件位于项目的类的根目录下：

      ```java
        ApplicationContext context = new ClassPathXmlApplicationContext("applicationContext.xml")
        // or
        ApplicationContext context = new FileSystemXmlApplicationContext("classpath:applicationContext.xml")
      ```

## 哪些类需要配置成Bean？

