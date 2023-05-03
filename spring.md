[Вопросы для собеседования](README.md)



# Spring Framework

+ [Что такое __Spring Framework__?](#Что-такое-Spring-Framework)
+ [Архитектура __Spring Framework__](#Архитектура-Spring-Framework)
+ [Какие паттерны проектирования используются в __Spring Framework__?](#Какие-паттерны-проектирования-используются-в-Spring-Framework)
+ [Что такое Bean](#Что-такое-Bean)
+ [Какие способы создания Beans или какие способы конфигурирования вы знаете?](#Какие-способы-создания-Beans-или-какие-способы-конфигурирования-вы-знаете)
+ [Application Context и Dependency Injection](#Application-Context-и-Dependency-Injection)
+ [Inversion of Control __IoC__](#Inversion-of-Control-IoC)
+ [Dependency Injection __DI__](#Dependency-Injection-DI)
+ [Scope или области видимости](#Scope-или-области-видимости)
+ [Этапы инициализации контекста](#Этапы-инициализации-контекста)
+ [Жизненный цикл бина Bean Lifecycle](#Жизненный-цикл-бина-Bean-Lifecycle)
+ [Spring MVC](#Spring-MVC)
+ [Стартеры в Spring](#Стартеры-в-Spring)
+ [Аннотации Spring](#Аннотации-Spring)
+ [Conditional бин и необязательная зависимость Autowired required false](#Conditional-бин-и-необязательная-зависимость-Autowired-required-false)
+ [Spring AOP](#Spring-AOP)



















## Что такое __Spring Framework__?

<details> 
  <summary>Правильный ответ</summary>

__Spring Framework__ — один из самых популярных фреймворков для разработки веб-приложений на
языке Java, с открытым исходным кодом, главным преимуществом которого является простота и легковесность.
Фреймворк Spring представляет собой контейнер Inversion of Control (IoC).\

</details>

[в меню _Spring Framework_](#Spring-Framework)





## Архитектура __Spring Framework__

<details> 
  <summary>Правильный ответ</summary>

![Архитектура Spring Framework](images/spring-schema.jpg "Архитектура Spring Framework")

__Data Access__ - набор модулей для доступа к данным в различных форматах, включая базы данных, обмен сообщениями,XML

+ `JDBC` - абстракция над Java JDBC API, когда нам нужен доступ к данным из БД, устраняет всю сложность в виде
  (запросов, Statement, ResultSet, Queries) предоставляет JdbcTemplate для легкого доступа к данным.
  Так же дает способы итерации и сопоставления ResultSet-ов.
  
+ `ORM` - object relation mapping(объектно-реляционное отображение) - обеспечивает поддержку интеграций с различными 
реализациями ORM(Hibernate, JDO(Java Data Objects))
  
+ `JMS` - __Java Messaging Service__ - это абстракция над различными реализациями __JMS__(ActiveMQ, RabbitMQ),определяет спецификацию
  связи в форме сообщений.
  
+ `OXM` - спецификация Java OXM(Object XML Marshalling), определяет способ передачи и доступа к данным в форме XML.
Реализации __OXM__ - JAXB и XStream
  
+ `Transactions` - обеспечивает единый способ управления транзакцими объектов данных, а так же баз данных.\
Поддерживает программное и декларативное управление транзакциями.
  + Программное - управление с помощью программирования
  + Декларативное - отделяем управление транзакциями от бизнес логики, используя аннотации в конфигурации на основе XML


__Core Container__ - основа Spring содержит базовые классы и инструменты.\
Включая DI(dependency injection) внедрение зависимостей и IoC (Inversion of control) инверсию управления.

+ `Beans` - управляет жизненным циклом бинов.
Bean - любой класс зарегистрированный как бин.
В Beans есть BeanFactory которая создает экземпляр бин-компонентов, преобразует бин-компоненты в зависимости бин-компонентов
и автоматически связывает бин-компоненты на основе имени или типа.

+ `Context` - ключевым элементом модуля является интерфейс ApplicationContext. Все бины лежал в Context, через него
осуществляется доступ к бин-компонентам.
При запуске приложения все классы которые помечены аннотациями описаны в xml или config классе становятся бинами,
  попадают в контекст, спринг сам создает эти объекты, реализует зависимости и предоставляет доступ к ним.

+ `SpEL` __Spring Expression Language - мощный полнофункциональный язык выражения.
Используется для преобразования выражений в значения во время выполнения.\
Может запрашивать графы объектов во время выполнения и может использоваться в XML или основанных на аннотациях
_BeanDefinition_ и _BeanConfiguration_.

+ `Web` - используется для создания web - приложений, используя его можем создавать приложения MVC, перехватчики, веб-сервисы, портлеты(элементы веб-страниц)

+ `Web&Servlet` - представляет функции для веб интеграций.
Обеспечивает внедрение модели Spring MVC - предоставляет механизм для создания веб приложений.\
  Model View Controller - концепция просмотра и действий.\
  Представление - пользовательский интерфейс и пользователь\
  Действие - это компонент обслуживающий веб запрос.


+ `Web Sockets` - для создания веб-сеокетов.
Веб-сокеты - это скажем так это тунель между сервисом и потребителем, в HTTP соединении клиент опрашивает сервер на предмет обновлений.\
С помощью веб-сокетов создается двунаправленная связь, происходит клиент-серверное общение напрямую.

+ `Web Portlets` - подключаемые программные компоненты пользовательского интерфейса, которые управляются и отображаются на 
web-портале.Это механизм для отображения пользовательских интерфесов нескольких приложений(портлетов) в одном пользовательском интерфейсе.
  
+ `AOP` - реализация аспектно-ориентированного программирования.\
Аспект - любая вторичная задача, которую объект должен выполнить.\
Каждый объект имеет отдельную ответственность и может иметь вторичные задачи(ведение журнала, обработка исключений).\
__AOP__ - это механизм для снятия вторичных обязаностей с объектов и передачи их прокси объектам.
  
+ `Aspects` - предоставляет единый способ интеграции с другими реализациями __AOP__, такими как AspectJ.

+ `Instrumentation` - используется для мониторинга производительности приложения, он отслеживает различные обьекты,
чтобы диагностировать проблемы приложений и регистрирует их.

+ `Messaging` - обеспечивает единообразный способ взаимодействия с различными службами обмена сообщениями.

+ `Test` - обеспечивает тестирование кода.

</details>

[в меню _Spring Framework_](#Spring-Framework)






## Какие паттерны проектирования используются в __Spring Framework__?

<details> 
  <summary>Правильный ответ</summary>

Spring Framework использует множество шаблонов проектирования, например:

+ Singleton Pattern: Creating beans with default scope.
+ Factory Pattern: Bean Factory classes
+ Prototype Pattern: Bean scopes
+ Adapter Pattern: Spring Web and Spring MVC
+ Proxy Pattern: Spring Aspect Oriented Programming support
+ Template Method Pattern: JdbcTemplate, HibernateTemplate etc
+ Front Controller: Spring MVC DispatcherServlet
+ Data Access Object: Spring DAO support
+ Dependency Injection and Aspect Oriented Programming

</details>

[в меню _Spring Framework_](#Spring-Framework)





## Что такое Bean

<details> 
  <summary>Правильный ответ</summary>

__Bean__ - Java объект созданный Spring.

>Спринг сам создает по описанному классу объект, внедряет в него все зависимости и помещает его в контекст,
> такие объекты созданные спрингом, принято называть бинами. Скажем так, настроенные, готовые объекты.

</details>

[в меню _Spring Framework_](#Spring-Framework)





## Какие способы создания Beans или какие способы конфигурирования вы знаете?

<details> 
  <summary>Правильный ответ</summary>

+ конфигурирование при помощи XML-файла конфигурации (beans.xml config.xml)
+ Конфигурирование с использованием аннотаций (@Component и наследников @Controller @Service @Repository)
+ Конфигурирование в Java классе используя аннотации @Configuration и @Bean

__Конфигурирование при помощи XML-файла__

```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
  xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
  xsi:schemaLocation="http://www.springframework.org/schema/beans
  http://www.springframework.org/schema/beans/spring-beans.xsd">
  <bean id="cameraRoll" class="ru.geekbrains.spring.ColorCameraRoll" />
  <bean id="camera" class="ru.geekbrains.spring.CameraImpl">
    <property name="cameraRoll">//в камеру вставляем пленку
    <ref bean="cameraRoll" />
    </property>
  </bean>
</beans>
```
__Конфигурирование с использованием аннотаций (@Component и наследников @Controller @Service @Repository)__

Spring 2.5 стало возможным убрать часть кода из XML-конфигурации с помощью
специальных аннотаций

```java
@Component("cameraRoll")
public class ColorCameraRoll implements CameraRoll {
public void processing() {
System.out.println("-1 цветной кадр");
}
}
```
Но чтобы спринг нашел классы помеченные этими аннотациями, нужно в xml файле указать в каком пакете искать их:

```xml
<context:component-scan base-package="ru.geekbrains.spring" />
```
Тогда при запуске приложения Spring просканирует этот пакет и все вложенные на наличие классов помеченных 
аннотациями.

__Конфигурирование в Java классе используя аннотации @Configuration и @Bean__

>Создание контекста Spring может происходить вообще без использования XML-конфигурации. Всю
конфигурацию можно вынести в отдельный Java-класс, помеченный аннотацией @Configuration
 
```java
@Configuration
@ComponentScan("ru.geekbrains.spring")//можно указать спрингу где искать через аннотацию
public class AppConfig {
    
  @Bean(name = "cameraRoll")
  public CameraRoll cameraRoll() {
    return new ColorCameraRoll() ;
  }
  
  @Bean(name = "camera")
  public Camera camera(CameraRoll cameraRoll){
    Camera camera = new CameraImpl();
    camera.setCameraRoll(cameraRoll);
    return camera;
  }
}
```

+ __@Configuration__ — аннотация, указывающая на то, что данный Java-класс является классом
конфигурации;
+ __@Bean__ — используется для аннотирования методов, создающих бины в классе, помеченном
аннотацией @Configuration. Аналог тега <bean…../> в XML-конфигурации.

</details>

[в меню _Spring Framework_](#Spring-Framework)










## Application Context и Dependency Injection

<details> 
  <summary>Правильный ответ</summary>

__ApplicationContext__ представляет собой Spring IoC контейнер и необходим для инициализации, настройки и сборки бинов для построения приложения.

```java

/**
 * Конфигурационный класс Spring IoC контейнера
 */
@Configuration
public class LessonsConfiguration {
}
```
Создание контекста в который передаем сконфигурированный класс через аннотацию
```java
public class Starter {

    private static final Logger logger = LogManager.getLogger(Starter.class);

    public static void main(String[] args) {
        logger.info("Starting configuration...");

        ApplicationContext context = new AnnotationConfigApplicationContext(LessonsConfiguration.class);
    }
}
```
Создание контекста в который передаем XML файл в котором описан наш бин
![Application Context](images/spring-xml.jpg "Application Context")

![Application Context](images/spring-applicationcontext.jpg "Application Context")


![Application Context и Dependency Injection](images/spring-applicationcontext-dependencyinjection.jpg "Application Context и Dependency Injection")

Каждая ссылка называется зависимостью, один объект зависит от другого.
Когда объектов очень много и они зависят от большого количества других объектов, поддерживать это трудно, в этом помогает нам спринг.

Spring уменьшает количество кода и берет на себя контроль по настройке объектов и всех этих зависимостей.

>Например:
> + Допустим нам нужен объект в единственном экземпляре, нам пришлось бы реализовать паттерн Singleton,
> спринг делате это за нас, нет лишнего кода.
> + Если нам нужно всем объектам внедрить этот класс Singleton, это тоже куча когда, и можно запутаться, спринг это берет на себя.

![Application Context и Dependency Injection](images/spring-applicationcontext-dependencyinjection2.jpg "Application Context и Dependency Injection")
 
1. Мы описываем объекты которые необходимы для работы нашего приложения
2. Spring сам создает эти объекты и берет на себя управление ими(их жизненым циклом и многое другое)
3. Все готовые объекты с уже внедренными зависимостями храняться в одном месте Application Context, откуда
мы их забираем и используем.

![Application Context и Dependency Injection](images/spring-applicationcontext-dependencyinjection3.jpg "Application Context и Dependency Injection")


</details>

[в меню _Spring Framework_](#Spring-Framework)








## Inversion of Control __IoC__

<details> 
  <summary>Правильный ответ</summary>

__Инверсия управления (Inversion of Control, IoC)__ - паттерн проектирования или архитектурное решение
в котором стремимся к слабой связанности между компонентами программы.
>Одной из реализаций IoC является DI Dependency Injection Внедрение зависимостей
 
### Рассмотрим пример:

![Inversion of Control](images/spring-IoC1.jpg "Inversion of Control")

### Чтобы реализовать слабую зависимость мы можем использовать интерфейс(но появилась вторая проблема):
![Inversion of Control](images/spring-IoC3.jpg "Inversion of Control")

### Представим что мы решили проблему, и Spring сам нам создает бины.(хоть и написано new ClassicalMusic)
>появляется 3-я проблема\
> Даже представив что объекты музыки создал спринг, то плеер обращался бы к Application Context 
> и извлекал созданый бин в методе playMusic()
 
![Inversion of Control](images/spring-IoC4.jpg "Inversion of Control")

### Что мы можем сделать
![Inversion of Control](images/spring-IoC5.jpg "Inversion of Control")

>__Инверсия управления__ - это архитектурный подход, когда компонент не сам создает зависимости,
>а зависимости поставляются ему из вне.

### Теперь применим принцип Инверсии управления (Inversion of Control, IoC)

![Inversion of Control](images/spring-IoC6.jpg "Inversion of Control")

### И остается у нас последняя проблема, объект который нам поставляется извне должен где-то и кем-то создаваться

![Inversion of Control](images/spring-IoC7.jpg "Inversion of Control")

### Эта проблема решается уже при помощи __DI Dependency Injection__ (Внедрение зависимости) - в следующем вопросе.

> Итог:
> + поле класса сделали интерфейсом, теперь можем передавать любые его реализации(добились слабой связанности)
> + объекты не создаем вручную, а конфигурируем через(XML, аннотации или Java класс конфигурации)
> + применили IoC инверсию управления, мьюзик плеер теперь не сам создает/достает свои зависимости, а получает их из вне в конструктор

</details>

[в меню _Spring Framework_](#Spring-Framework)








## Dependency Injection DI

<details> 
  <summary>Правильный ответ</summary>

__Dependency Injection (внедрение зависимостей)__ - процесс предоставления внешней зависимости программному компоненту.
>Это одна из реализаций принципа Inversion of Control (помимо этого есть еще Factory Method, Service Locator).

>Внедрение зависимостей в Spring —  особенность фреймворка где контейнер Spring «внедряет» объекты в другие объекты или «зависимости».\
>Проще говоря, это позволяет слабо связывать компоненты и переносит ответственность за управление компонентами на контейнер.

### Основные виды Dependency Injection:

+ внедрение через конструктор;
+ внедрение через сеттер;
+ внедрение на уровне поля.

>Еще можно внедрять:
> + через множество конфигураций(scope, factory method)
> + через XML, аннотации или Java код

### Внедрение через конструктор

```java
public class Seller {
    
    private Shop shop;

    public Seller(Shop shop) {
        this.shop = shop;
    }
}
```

### Внедрение через сеттер

```java
public class Seller {

    private Shop shop;

    public void setShop(Shop shop) {
        this.shop = shop;
    }
}
```

### Внедрение через поле 

```java
@Component
public class Shop {
}
```

```java
@Component
public class Seller {

    @Autowired
    private Shop shop;
}
```

### Продолжим решать проблему из вопроса IoC

![Dependency Injection](images/spring-DI.jpg "Dependency Injection")

### Внедрим зависимость при помощи XML конфигурации

![Dependency Injection](images/spring-DI1.jpg "Dependency Injection")

>Теперь мы не создаем нужные объекты в ручную, чтобы положить их в конструктор в качестве зависимости,
> а достаем их из контекста уже настроенные с внедренными зависимостями

![Dependency Injection](images/spring-DI2.jpg "Dependency Injection")

### Внедрение зависимостей через конструктор и сеттер

![Dependency Injection](images/spring-DI-constructor-setter.jpg "Dependency Injection")

### Внедрение простых зависимостей(примитивных типов и строк)

![Dependency Injection](images/spring-DI-value.jpg "Dependency Injection")

>Можно использовать аннотацию @Value

```java
@Component
public class Camera {
  @Value("X1")
  private String model;
  
  public Camera() {
  }
  public Camera(String model) {
  this.model = model;
  }
  public String getModel() {
  return model;
  }
  public void setModel(String model) {
  this.model = model;
}
```

### Внедрение значений из внешнего файла .properties
> + не хотим каждый раз лезть в applicationContext.xml
> + хотим все простые значения указать в одно файле

1. Создаем файл `application.properties` указываем переменные и их значения
  + musicPlayer.name=Some name
  + musicPlayer.volume=60

2. Импортируем файл в наш XML 

```xml
<context:property-placeholder location="classpath:application.properties"/>
```
3. Теперь мы можем в XML файле использовать значения из файла `application.properties`

```xml
<property name="name" value="${musicPlayer.name}"/>
<property name="volume" value="${musicPlayer.volume}"/>
```

![Dependency Injection](images/spring-DI3.jpg "Dependency Injection")

<Чтобы не использовать XML можно над классом использовать `@PropertySource(classpath:application.properties)`

</details>

[в меню _Spring Framework_](#Spring-Framework)








## Scope или области видимости

<details> 
  <summary>Правильный ответ</summary>

`Scope` - определяет область видимости бинов, по умолчанию для каждого бина scope=singleton.

__Виды scope:__

+ `singleton` - создается один единственный бин, при каждом запросе будет возвращаться один и тот же.
  >Используется в основном когда у нашего бина нет изменяемых состояний(stateless), потому что
  > если будем изменять состояние у singleton бина -> столкнемся с проблемой
  > Пример: достали бин музыкальный плеер, и изменили значение поля громкость, то в других местах где используется
  > плеер, громкость будет тоже изменена(работает как в Java __все ссылки ссылаются на один и тот же объект в памяти__)
+ `prototype` - при каждом запросе создается новый экземпляр бина, позволяет иметь любое кол-во экземпляров бина.
  > используется когда у бина есть изменяемые состояния(stateful)\
  > Когда для каждой ссылке есть свой собственный бин в Application Context
+ `request` - создается один экземпляр бина на каждый HTTP- запрос(касается исключительно Application Context)
+ `session` - создается один экземпляр бина на каждую HTTP сессию(касается исключительно Application Context)
+ `globalSession` - создается один экземпляр бина на каждую глобальную HTTP-сессию(касается Application Context)

</details>

[в меню _Spring Framework_](#Spring-Framework)






 ## Этапы инициализации контекста

<details> 
  <summary>Правильный ответ</summary>

`1 ЭТАП` - __Чтение данных из конфиг файла__

Когда приложение поднимается, спринг получает все данные из конфиг файла или сканируя пакет и подпакеты,
в котором лежит основной класс запуска приложения с аннотацией `@SpringBootApplication` на наличие служебных и 
пользовательских классов помеченных аннотациями(@Configuration, @Bean, @Component и его наследников @Service @Repository итд)

>На основании полученных данных создаются специальные объекты BeanDefinition которые попадают в BeanFactory.\
> BeanDefinition содержит:
> + Class - полный путь к классу объектом которого станет будущий бин
> + Scope - область видимости
> + Abstract - является ли класс абстрактным и т.д.
> 
> Все BeanDefinition попадают в контейнер BeanFactory.
> Итог: создаст определенное количество BeanDefinition содержащих информацию какие объекты с какими нужно создать.

`2 ЭТАП` - __Настройка созданных Bean Definition__

> Происходит настройка созданных BeanDefinition, обрабатываются только те BeanDefinition, классы которых помечены
> определенными аннотациями.\ Например `@Value(“${property.password}”` в поле класса присваивается значения из файла `application.properties`\
> Если мы хотим изменить бин до его создания, можно создать класс настройщик:
> 1. Класс-настройщик должен быть компонентом Spring (т.е. иметь аннотацию @Component, а
> путь к данному классу должен содержаться в конфигурационном файле или в классе нашего
> приложения);
> 2.  Реализовывать интерфейс BeanFactoryPostProcessor и его единственный метод
> postProcessBeanFactory, который и принимает в качестве параметра BeanFactory.
 
```java
@Component
public class TestBeanFactoryPostProc implements BeanFactoryPostProcessor {
  public void postProcessBeanFactory(ConfigurableListableBeanFactory beanFactory) throws BeansException {
    // Получение имен BeanDefinition всех бинов, объявленных пользователем
    String[] beanDefinitionNames = beanFactory.getBeanDefinitionNames();
    // Перебор массива для получения доступа к каждому имени
    for(String name: beanDefinitionNames) {
      // Получение BeanDefinition по имени
      BeanDefinition beanDefinition = beanFactory.getBeanDefinition(name);
      // Вывод информации о BeanDefinition
      System.out.println(beanDefinition.toString());
    }
  }
}
``` 

`3 ЭТАП` - __Внутренний этап, Spring создает бины__

>На этом этапе BeanFactory, используя BeanDefinition, создает бины. Данный процесс является
>внутренним процессом Spring, и нет смысла влиять на него. Важно отметить, что на этой стадии бины
>лишь создаются, но их зависимости еще не удовлетворены.

`4 ЭТАП` - __Внутренний этап, Spring создает бины__

>На четвертом этапе мы имеем созданные бины, но зависимости еще не внедрены, в том числе и
простые значения, внедряемые аннотацией @Value. Значит, бины еще не готовы к использованию.

>Чтобы внедрить зависимости, Spring использует классы-настройщики, которые и обрабатывают
>аннотации @Value, @Autowired и другие. 
> По завершении этапа бины полностью готовы к использованию.

>Мы без проблем можем реализовать собственный
>класс-настройщик, но для этого он должен выполнять два условия:
> + Класс-настройщик должен являться компонентом Spring (иметь аннотацию @Component, а
>путь к данному классу должен содержаться в конфигурационном файле или классе нашего
>приложения);
> + Реализовывать интерфейс BeanPostProcessor и его методы:

```java
public interface BeanPostProcessor {
  Object postProcessBeforeInitialization(Object bean, String beanName) throws BeansException;
  Object postProcessAfterInitialization(Object bean, String beanName) throws BeansException;
}
```
>В отличие от класса, реализующего интерфейс BeanFactoryPostProcessor, реализация этого
интерфейса позволит получать доступ к каждому бину поочередно. В каждый из методов передается
сам бин и его имя.
> 
> + __postProcessBeforeInitialization__ – метод, вызываемый до инициализации бина (термин
>«инициализация» в данном контексте довольно относителен: для Spring это означает вызов
>пользовательского init-метода, о котором будет рассказано далее). На данном этапе бин
>создан, и в него уже внедрены зависимости, которые помечены аннотациями Spring
>(@Autowired, @Value и т.п.). Классы-настройщики Spring всегда будут вызываться раньше,
>чем реализованные пользователем;
> + __postProcessAfterInitialization__ – метод, который выполняется после инициализации (после
>  вызова init-метода). После него настроенные бины попадают непосредственно в контейнер
>   бинов.

Предположим, что помощник перед покупкой фотоаппарата решил проверить его работоспособность.
Для этого ему необходимо самому попробовать сделать фотографию. Для осуществления этой затеи
реализуем собственный BeanPostProcessor: 

```java
@Component
public class PhotocameraTestBeanPostProcessor implements BeanPostProcessor {
  public Object postProcessBeforeInitialization(Object bean, String beanName) throws BeansException {
    // В данном методе просто возвращаем бин
    return bean;
  }
  public Object postProcessAfterInitialization(Object bean, String beanName) throws BeansException {
    // Находим бин класса фотокамеры
    if (bean instanceof Camera) {
      System.out.println("Делаю пробное фото!");
      // Делаем пробное фото
      ((Camera) bean).doPhotograph();
      System.out.println("Отлично! Работает!");
    }
    return bean;
  }
}
```

</details>

[в меню _Spring Framework_](#Spring-Framework)







## Жизненный цикл бина Bean Lifecycle

<details> 
  <summary>Правильный ответ</summary>

Все, что было рассмотрено ранее, относится к этапам инициализации контекста. Но сам бин об этих
этапах ничего не знает. Бины Spring обладают жизненным циклом. Фактически, это дает возможность
вызывать собственные методы бина на его жизненных этапах. Чтобы подобное стало возможным,
необходимо как-то пометить метод и время его вызова. На практике используется несколько
подходов.

![Bean Lifecycle](images/spring-bean-lifecycle.jpg "Bean Lifecycle")

__Первый подход использует аннотации:__

+ @PostConstruct – метод инициализации, вызываемый после создания объекта и внедрения
зависимостей (т.е. между методами postProcessBeforeInitialization и
postProcessAfterInitialization интерфейса BeanPostProcessor);
+ @PreDestroy – метод, вызываемый перед уничтожением бина.

__Второй подход использует XML-атрибуты тега <bean>:__

+ init-method;
+ destroy-method.

>Если используются оба подхода для одного и того же бина, первым выполнятся методы помеченные аннотацией.

`init-method` - метод запускается в ходе инициализации бина(инициализация ресурсов, обращение к внешним файлам, запуск БД)

`destroy-method` - метод запускается в ходе уничтожения бина(при завершении приложения)(очищение ресурсов, закрытие потока ввода-вывода, закрытие соединения с БД)

>+ Модификатор доступа может быть любой
>+ Тип возвращаемого значения может быть любой но чаще всего `void` - нет возможности получить возвращаемое значение
>+ Название метода может быть любым
>+ Не должны принимать какие либо аргументы
Чтобы использовать аннотации нужно подключать доп зависимости

> __!!!__ Spring не вызывает destroy-method для бинов со scope=prototype(об этом должны думать мы)
> 
```xml
<dependency>
  <groupId>javax.annotation</groupId>
  <artifactId>jsr250-api</artifactId>
  <version>1.0</version>
</dependency>

//в JAVA 11 они полностью удалены 
<dependency> 
    <groupId>javax.annotation</groupId>     
    <artifactId>javax.annotation-api</artifactId>  
    <version>1.3.2</version> 
</dependency> 
```

### Factory method (Фабричный метод)

![Factory method](images/spring-factory-method.jpg "Factory method")
![Factory method](images/spring-factory-method2.jpg "Factory method")

> Чтобы реализовать фабричный метод нужно в класс добавить приватный конструктор и статический метод
> который будет возвращать объект.
> 
![Factory method](images/spring-factory-method3.jpg "Factory method")

>а в XML конфиг файле указать фабричный метод который будет вызывать спринг при создании бина.

![Factory method](images/spring-factory-method4.jpg "Factory method")

> ВАЖНО. 
> Пока стоит scope=singleton, не зависимо от того, что в классе каждый раз создается объект `new ClassicalMusic()`
> он будет создан один раз. Все остальные разы спринг будет возвращать ссылку на этот объект.

</details>

[в меню _Spring Framework_](#Spring-Framework)








## Spring MVC

<details> 
  <summary>Правильный ответ</summary>

`Spring MVC` -  это один из компонентов Spring Framework, который помогает разрабатывать web приложения;\
Spring MVC - предлагает разработку веб приложений с использованием архитектуры `Model - View - Controller`;\
Разрабатывая по этой модели мы можем использовать другие компоненты спринга, Spring Core - IoC,DI,Beans итд;

![Spring MVC](images/spring-mvc-schema.jpg "Spring MVC")

>Что может представлять из себя Spring MVC приложение:
> + набор Java классов (контроллеры, модели или сущности, классы сервисного слоя и слоя репозитория)
> + представления - набор HTML страниц с использования JavaScript и CSS 
> + Spring конфигурация

![Spring MVC](images/spring-mvc-ds.jpg "Spring MVC")

__Рассмотрим каждый из этапов:__

+ Шаг 0. Пользователь делает запрос, который содержит URL-адрес запроса и, возможно,
какие-то данные.
+ Шаг 1. Все запросы поступают на DispatсherServlet, который обязан перенаправить их
конкретному контроллеру. Контроллеров может быть много, поэтому DispatcherServlet
обращается к HandlerMapping, который на основании URL-строки запроса возвращает
информацию о классе контроллера и его методе, который необходимо вызвать.
+ Шаг 2. DispatcherServlet вызывает метод контроллера, передавая в него класс объекта
Model. Метод, как правило, возвращает имя представления и может добавлять в объект
класса Model данные, которые необходимо в дальнейшем передать пользователю.
+ Шаг 3. На данном этапе у DispatcherServlet могут быть данные, которые являются
результатом работы метода контроллера, и имя отображения. Дальнейшие действия —
добавить эти данные в представление, но для начала нужно получить ссылку на
представление. Для формирования ссылки DispatcherServlet обращается к ViewResolver,
который на основании выбранного разработчиком правила формирует полную ссылку на
представление (например, JSP или HTML) и возвращает ее DispatcherServlet.
+ Шаг 4. DispatcherServlet получает конкретное представление по сформированной ранее
ссылке (пути), добавляет в представление данные, отрисовывает его в HTML-страницу (но не
обязательно).
+ Шаг 5. DispatcherServlet возвращает ответ пользователю, и он отображается в браузере.

</details>

[в меню _Spring Framework_](#Spring-Framework)





## Стартеры в Spring

<details> 
  <summary>Правильный ответ</summary>

__Стартеры__ — это наборы удобных дескрипторов(абстракция от слова "описывающий") зависимостей,
которые можно включить в приложение.

Например, чтобы использовать Spring и JPA для доступа к базе данных, нужно просто
добавить зависимость `spring-boot-starter-data-jpa` в проект. 

Стартеры содержат множество зависимостей, необходимых для быстрого запуска проекта с помощью согласованного и
поддерживаемого набора управляемых транзитивных зависимостей. Все официальные стартеры
следуют единой схеме именования: `spring-boot-starter-*`, где `*` — конкретный тип приложения.

__Вот несколько популярных стартеров Spring Boot:__
+ `spring-boot-starter-web` — используется для создания веб-служб RESTful с использованием
Spring MVC и Tomcat в качестве встроенного контейнера приложений;
+ `spring-boot-starter-thymeleaf` — подключение шаблонизатора Thymeleaf;
+ `spring-boot-starter-data-jpa` — подключает модуль Spring Data JPA;

+ `spring-boot-starter-security` — подключает модуль Spring Security для обеспечения
безопасности веб-приложения;
+ `spring-boot-starter-jersey` — альтернатива Spring-boot-starter-web, в которой используется
встроенный сервер приложений Jersey, а не Tomcat;
+ `spring-boot-starter-jdbc` — реализует пул соединений JDBC, основан на реализации пула
JDBC Tomcat.

`spring-boot-starter-parent` — это специальный стартер, предоставляющий настройки Maven по
умолчанию и раздел управления зависимостями, чтобы вы могли опустить теги версии для
Spring-зависимостей.

>По-умолчанию, в spring-boot-starter-parent указана совместимость с Java 6. Для того, чтобы
изменить версию на более новую, достаточно в pom.xml в элементе <properties> прописать элемент
<java.properties> с соответствующей версией.

```xml
<properties>
    <java.version>1.8</java.version>
</properties>
```
</details>

[в меню _Spring Framework_](#Spring-Framework)








## Аннотации Spring

<details> 
  <summary>Правильный ответ</summary>

`@SpringBootApplication` - наследуется от аннотаций @Configuration, @ComponentScan,
@EnableAutoConfiguration, вешается на класс начальной загрузки и конфигурации Spring

---

`@Configuration` — объявляет класс классом Java-based конфигурации;

---

`@ComponentScan` — позволяет выполнять компонентное сканирование(без аргументов будет сканировать текущий пакет и все подпакеты);

---

`@EnableAutoConfiguration` — включает автоконфигурирование

---

`EnableWebMVC` - включает поддержку аннотаций MVC- компонентов(например @Controller) импортирует конфигурации MVC

---

`@ModelAttribute` - чтобы не указывать пачку RequestParam можно указать `@ModelAttribute Student newStudent` спринг
сам соберет объект из параметров например формы.

---

`@PersistenceContext` - Аннотация @PersistenceContext внедряет прокси, который выполняет открытие и закрытие
EntityManager автоматически. В отличие когда мы создаем entityManager при помощи __EntityManagerFactory__ нужно следить 
за открытием и закрытием entityManager.

```java
@PersistenceContext
private EntityManager entityManager;
```
---
`@Bean` - аннотация уровня метода, используется вместе с @Configuration, для создания/настройки бина.
Аннотируется фабричный метод создания бина.
---
`@Autowired` - для внедрения зависимости/компонента.

---

`@Qualifier` - используется вместе с @Autowired для уточнение какой именно бин хотим внедрить(заинжектить) например в поле интерфейса.

```java
@Autowired//конструктор
Biker(@Qualifier("bike") Vehicle vehicle) {
    this.vehicle = vehicle;
}

@Autowired//сеттер
void setVehicle(@Qualifier("bike") Vehicle vehicle) {
    this.vehicle = vehicle;
}

@Autowired//сеттер альтернативный способ
@Qualifier("bike")
void setVehicle(Vehicle vehicle) {
    this.vehicle = vehicle;
}

@Autowired//над полем
@Qualifier("bike")
Vehicle vehicle;
```
---

`@Primary`- задает бин, который будет внедрен по умолчанию при отсутствии других.

```java
@Component
@Primary
class Car implements Vehicle {}

@Component
class Bike implements Vehicle {}

@Component
class Driver {
    @Autowired
    Vehicle vehicle;//тут внедрится Car
}

@Component
class Biker {
    @Autowired
    @Qualifier("bike")
    Vehicle vehicle;//а сюда внедрится уже Bike
}
```
---

`@Lookup` - для того чтобы метод заглушка возвращал бин со scope=prototype(каждый раз новый)

>Обычно бины в приложении Spring являтся синглтонами, и для внедрения зависимостей мы используем конструктор или сеттер.
Но бывает и другая ситуация: имеется бин Car — синглтон (singleton bean), и ему требуется каждый раз новый экземпляр бина Passenger.\
> То есть Car – синглтон, а Passenger – так называемый прототипный бин (prototype bean).\
> Жизненные циклы бинов разные. Бин Car создается контейнером только раз, а бин Passenger создается каждый раз новый – допустим,
> это происходит каждый раз при вызове какого-то метода бина Car. 
> Вот здесь то и пригодится внедрение бина с помощью Lookup метода. 
> Оно происходит не при инициализации контейнера, а позднее: каждый раз, когда вызывается метод.\
> __Что такое Lookup method injection?__\
> Суть в том, что вы создаете метод-заглушку в бине Car и помечаете его специальным образом – аннотацией
> @Lookup. Этот метод должен возвращать бин Passenger, каждый раз новый. 
> Контейнер Spring под капотом создаст подкласс и переопределит этот метод и будет вам выдавать новый
> экземпляр бина Passenger при каждом вызове аннотированного метода.
> Даже если в вашей заглушке он возвращает null (а так и надо делать, все равно этот метод будет переопределен).

Допустим, в бине есть метод drive(), и при каждом вызове метода drive() бину Car требуется новый экземпляр бина Passenger – сегодня пассажир Петя, завтра — Вася. То есть бин Passenger прототипный. Для получения этого бина надо написать метод-заглушку createPassenger() аннотировать его с помощью @Lookup
```java
@Component
public class Car {
    @Lookup
    public Passenger createPassenger() {
        return null;
    };
    public String drive(String name) {
        Passenger passenger = createPassenger();
        passenger.setName(name);
        return "car with " + passenger.getName();
    }
}
```

Контейнер Spring переопределит этот метод-заглушку и будет выдавать при его вызове каждый раз новый экземпляр Passenger.

Осталось только определить бин Passenger как прототипный:

```java
@Component
@Scope("prototype")
public class Passenger {
    private String name;
    public String getName() {
        return name;
    }
    public void setName(String name) {
        this.name = name;
    }
}
```
И все, теперь при вызове метода drive() мы можем везти каждый раз нового пассажира. Имя его передается в аргументе метода drive(), и затем задается сеттером во вновь созданном экземпляре пассажира

---

`@DependsOn` - говорим Spring инициализировать другие bean-компоненты перед аннотированным.
>Обычно это поведение является автоматическим, основанным на явных зависимостях между bean-компонентами.\
>Эта аннотация нужна нам только тогда, когда зависимости неявные , например, загрузка драйвера JDBC или инициализация статической переменной.\
Мы можем использовать @DependsOn для зависимого класса, указав имена bean-компонентов зависимостей. Аргумент значения аннотации нуждается в массиве, содержащем имена bean-компонентов зависимостей:

```java
@DependsOn("engine")
class Car implements Vehicle {}
```
В качестве альтернативы, если мы определяем bean-компонент с аннотацией @Bean , фабричный метод должен быть аннотирован с помощью @DependsOn :

```java
@Bean
@DependsOn("fuel")
Engine engine() {
    return new Engine();
}
```
---

`@Lazy` - для ленивой инициализации компонента.
>По умолчанию Spring создает все одноэлементные компоненты при запуске/загрузке контекста приложения.\
Однако бывают случаи, когда __нам нужно создать bean-компонент, когда мы его запрашиваем, а не при запуске приложения__.

Эта аннотация ведет себя по-разному в зависимости от того, где именно мы ее размещаем. Можем поставить:

+ аннотированный фабричный метод компонентов @Bean для задержки вызова метода (отсюда и создание компонента)
+ класс @ Configuration и все содержащиеся в нем методы @Bean будут затронуты
+ класс @Component, который не является классом @Configuration, этот bean-компонент будет инициализирован лениво
+ конструктор, сеттер или поле @Autowired для ленивой загрузки самой зависимости (через прокси)

---

`@Component` - аннотация уровня класса, класс является компонентом.
Наследники(@Controller, @Service,@Repository)

---

`@Controller` - объявляет, что этот класс является контроллером

---

`@Service` - объявляющая, что этот класс представляет собой сервис – компонент сервис-слоя.

---

`@Repository` - объявляет, что класс служит для работы с данными в основном с Базой Данных.

---

`ResponseBody` - означает что будет возвращен объект.

---

`RestController` - аналог двух аннотаций (@Controller + @ResponseBody)

---

`@RequestMapping` - используется в сочетании @RestController для прописывания маппинга контроллера

```java
@RequestMapping("/api/v1/products")
```

---

`@RequestParam` -  указывается в агрументах метода
```java
 @PostMapping("/add")//добавить продукт в корзину
    public void addToCart(@RequestParam UUID cartId, @RequestParam(name = "product_id") Long productId) {
       cartService.addToCart(cartId,productId);
    }
```
---

`@PathVariable` - переменная часть(кусочек) пути
```java
@GetMapping("/{uuid}")//запросить корзину
public CartDto getCurrentCart(@PathVariable(name = "uuid") UUID cartId){}
```
---

`@CookieValue`- используется в аргументах метода, чтобы получить значение куки.

---

`@Value` - для внедрения значений свойств в bean-компоненты.
```java
Engine(@Value("8") int cylinderCount) {//через конструктор
   this.cylinderCount = cylinderCount;
}
```

```java
@Autowired
void setCylinderCount(@Value("8") int cylinderCount) {//через сеттер
    this.cylinderCount = cylinderCount;
}
```

```java
@Value("8")
void setCylinderCount(int cylinderCount) {//альтернатива так же через сетер
    this.cylinderCount = cylinderCount;
}
```

```java
@Value("8")//над полем
int cylinderCount;
```

```java
@Value("${jwt.secret}")//из файла application.properties
private String secret;//ключ для генерации токенов
```

---

`@CrossOrigin` - используется для указания списка доверенных адресов, кому разрешено обращаться к нашему приложению.

---

`@CrossOrigin(origins = "http://example.com")`

---

`@ExceptionHandler` - уровень метода, для обработки исключений на уровне контроллера, стоит на методе в контроллере(старый способ)

---

`@ControllerAdvice и RestControllerAdvice ` - аннотируемый класс становится глобальным перехватчиком исключений всего слоя контроллеров.

---

`@Scope` - задает область действия/видимости.

```java
@Component
@Scope("prototype")
class Engine {}
```
---

`@Profile` -Если мы хотим, чтобы Spring использовал класс @Component или метод @Bean только тогда, когда активен определенный профиль 

```java
@Component
@Profile("sportDay")
class Bike implements Vehicle {}
```

---

`@Import` - С помощью этой аннотации мы можем использовать определенные классы @Configuration без сканирования компонентов . Мы можем предоставить этим классам аргумент значения @Import :

```java
@Import(VehiclePartSupplier.class)
class VehicleFactoryConfig {}
```

---


`@ImportResource` - можем импортировать конфигурации XML .

```java
@Configuration
@ImportResource("classpath:/annotations.xml")
class VehicleFactoryConfig {}
```

---

`@PropertySource` - С помощью этой аннотации мы можем определить файлы свойств для настроек приложения

```java
@Configuration
@PropertySource("classpath:/annotations.properties")
class VehicleFactoryConfig {}
```

>@PropertySource использует функцию повторяющихся аннотаций Java 8, что означает, что мы можем пометить ею класс несколько раз:

```java
@Configuration
@PropertySource("classpath:/annotations.properties")
@PropertySource("classpath:/vehicle-factory.properties")
class VehicleFactoryConfig {}
```

`@PropertySources` - для указания нескольких конфигураций @PropertySource

```java
@Configuration
@PropertySources({ 
    @PropertySource("classpath:/annotations.properties"),
    @PropertySource("classpath:/vehicle-factory.properties")
})
class VehicleFactoryConfig {}
```
---

`@Embeddable` - "встраиваемый" чтобы объявить, что класс будет внедрен другими объектами.

```java
@Embeddable
public class ContactPerson {

    private String firstName;

    private String lastName;

    private String phone;

    // standard getters, setters
}
```

`@Embedded` - "встроенный" ставится над полем встраиваемого объекта(на классе которого стоит @Embeddable)

```java
@Entity
public class Company {

    @Id
    @GeneratedValue
    private Integer id;

    private String name;

    private String address;

    private String phone;

    @Embedded
    private ContactPerson contactPerson;

    // standard getters, setters
}
```

---

### Аннотации SPRING AOP 

---

`@Order` - определяет порядок сортировки аннотированного компонента или компонента.

__Ordered.LOWEST_PRECEDENCE__ - компонент имеет самый низкий приоритет\
__Ordered.HIGHEST_PRECEDENCE__ -  компонент имеет самый высокий приоритет

До Spring 4.0 аннотация @Order  использовалась только для порядка выполнения AspectJ.

>Начиная с Spring 4.0, он поддерживает упорядочение внедренных компонентов в коллекцию. В результате Spring будет внедрять автосвязанные bean-компоненты одного и того же типа в зависимости от их порядкового значения.

```java
public interface Rating {
    int getRating();
}
```

```java
@Component
@Order(1)//чем ниже значение - тем лучше приоритет
public class Excellent implements Rating {

    @Override
    public int getRating() {
        return 1;
    }
}

@Component
@Order(2)
public class Good implements Rating {

    @Override
    public int getRating() {
        return 2;
    }
}

@Component
@Order(Ordered.LOWEST_PRECEDENCE)
public class Average implements Rating {

    @Override
    public int getRating() {
        return 3;
    }
}
```
---


</details>

[в меню _Spring Framework_](#Spring-Framework)








## Conditional бин и необязательная зависимость Autowired required false

<details> 
  <summary>Правильный ответ</summary>

>В общем случае рекомендуется внедрять зависимости через конструктор. Но необязательные зависимости рекомендуется внедрять через сеттер.

### @Conditional бин

Допустим, в проекте есть необязательный бин, который создается (либо нет) в зависимости от условия: окружения, версии jre, свойства в application.properties.

Например, логгер в production-среде может быть один, а в develepment-среде — другой. Но мы сделаем еще проще — создадим бин Logger, который либо создается, либо нет в зависимости от настройки в application.properties

```xml
logger=true
```

Для этого аннотируем бин Logger с помощью @ConditionalOnExpression

```java
@Component//мы задали, что бин Logger создается только в том случае, если свойство logger=true. Иначе он не создается.
@ConditionalOnExpression("${logger:true}")
public class Logger {
    public void log(String message){
        System.out.println("log");
    }
}
```

Вариантов поставить условия очень много, мы рассматриваем  только @ConditionalOnExpression (внутри задается SPEL-выражение), но тут подошел бы и @ConditionalOnProperty:

>Нежелательно внедрять бин Logger в другой бин AnimalRepository через конструктор AnimalRepository. Потому что внедрение через конструктор подразумевает, что все внедряемые бины уже созданы к моменту вызова конструктора. То есть сначала Logger, потом AnimalRepository. В случае же logger=false бин Logger отсутствует.

Поэтому необязательный бин внедрим через сеттер.

### @Autowired(required=false) и внедрение через сеттер

То, что зависимость не обязательная, указывается с помощью аннотации: `@Autowired(required=false)`

Итак, класс AnimalRepository с необязательной зависимостью выглядит так:

```java
@Repository
public class AnimalRepository {
    private Logger logger;
    @Autowired(required = false)
    public void setLogger(Logger logger) {
        this.logger = logger;
    }
    public void save() {
        if (logger != null)
            logger.log("logged");
        System.out.println("save method");
    }
}
```
AnimalRepository создается вне зависимости от настройки logger.

А с необязательной зависимостью обходятся так, как показано выше — проверяют ее на null. (Хотя есть еще вариант просто присвоить некий логгер по умолчанию, но опустим этот вариант).

### Проверка

Можно написать тест и убедиться, что контекст успешно создается при любом значении свойства logger. А логирование происходит только при logger=true.

```java
@SpringBootTest
class MainTests {
    @Autowired
    private AnimalRepository animalRepository;
    @Test
    void whenLogger_thenLog() {
        animalRepository.save();
    }
}
```
</details>

[в меню _Spring Framework_](#Spring-Framework)








## Spring AOP

<details> 
  <summary>Правильный ответ</summary>

__АОП (аспектно-ориентированное программирование)__ — это шаблон программирования, 
повышающий модульность за счет разделения сквозных задач.
Эти сквозные проблемы отличаются от основной бизнес-логики. 
Мы можем добавить дополнительное поведение к существующему коду без модификации самого кода.

Spring AOP - помогает реализовать сквозные задачи такие как аудит, логирование итд.

При помощи AOP мы можем выполнить следующее:

- сквозную задачу/проблему разбить на модули 
- вынести из основного кода, в отдельное место, в классы аспекты.  
- определяем как/где/когда будет применяться функциональность не изменяя основной класс

Есть два преимущества аспектов:

+ Во-первых, логика для каждой проблемы теперь находится в одном месте, а не разбросана по кодовой базе.
+ Во-вторых, бизнес-модули содержат код только для своей основной задачи. Второстепенная проблема была перемещена в аспект .

Включить AOP в Spring

1-й способ
+ Добавить зависимость `spring-boot-starter-aop` + библиотеку `aspectjweaver.jar`
+ Включить поддержку @AspectJ с Java @Configuration, добавьте @EnableAspectJAutoProxy аннотацию:

```java
@Configuration 
@EnableAspectJAutoProxy
 public class AppConfig {

}
```
2-й способ
+ подключить зависимость `spring-boot-starter-web` и можно пользоваться(без аннотаций и конфиг класса из пункта 2)
 
__Терминология АОП__

`Join point` — это точки среза/наблюдения, присоединения к коду, где планируется введение функциональности
(когда AOP вмешивается и выполняет наш Advice)

![Join point](images/spring-aop-joinpoint.jpg "Join point")

`Pointcut` - это предикат(условие/выражение), которое выбирает одну или несколько точек соединения, 
в которых выполняется рекомендация. Точек может быть несколько.

![Pointcut](images/spring-aop-pointcut.jpg "Pointcut")

`Advice` — набор инструкций выполняемых на точках среза (Pointcut).

![Advice](images/spring-aop-advice.jpg "Advice")

Инструкции можно выполнять по событию разных типов:

+ `@Before` — перед вызовом метода
+ `@After` — после вызова метода(выполняется независимо от того, нормально ли завершился метод или было выброшено исключение)
+ `@AfterReturing` — после возврата значения из функции(выполняется при нориальном завершении метода)
+ `@AfterThrowing` — в случае exception(выполняется, если  было выброшено исключение)
+ `@AfterFinally` — в случае выполнения блока finally
+ `@Around` — можно сделать пред., пост., обработку перед вызовом метода, а также вообще обойти вызов метода.

`Aspect` — модуль в котором собраны описания Pointcut и Advice.

![Aspect](images/spring-aop-aspect.jpg "Aspect")

`introduction` -(Внедрение) — изменение структуры класса и/или изменение иерархии наследования для добавления функциональности аспекта в инородный код

`target` - объект к которому будут применяться Advice(советы)

`weaving` - это процесс связывания аспектов с другими объектами для создания рекомендуемых прокси-объектов. Это можно сделать во время компиляции, загрузки или во время выполнения.

__Шаблон для сборки Pointcut выражение:__

```java
"execution(modifier-pattern? return-type-pattern declaring-type-pattern? method-name-pattern(args-pattern)throws-pattern?)"

execution([модификатор_метода(public, *)?] [тип_возврата] [класс?] [имя_метода]([аргументы]) [исключения?]
```
Выражение настраивается по разному  в зависимости от того что нам нужно.
+ () - без аргументов
+ (*) - один аргумент
+ (..) -  несколько аргументов

Это обычное строковое выражение, можно вынести в константу и использовать в Advice.

```java
private static final String POINTCUT_EXPRESSION = "execution(public void com.geekbrains.aop.UserDAO.addUser())";
          
```

```java
@Before("execution(public void com.geekbrains.aop.UserDAO.addUser())"// 1 способ
        
@Before(POINTCUT_EXPRESSION)"// 2 способ

@Pointcut("execution(public * com.geekbrains.aop.UserDAO.get*(..))") // 3 способ
public void userDAOGetTrackerPointcut() {//это имя poincut
}

@Before(userDAOGetTrackerPointcut())"// 3 способ


```

### Примеры:


```java
@Aspect
@Component
public class AppLoggingAspect {
    
  @Before("execution(public void com.geekbrains.aop.UserDAO.*())") // pointcut expression
  public void beforeAnyMethodWithoutArgsInUserDAOClass() {
      System.out.println("AOP: любой void метод без аргументов класса UserDAO");
  }

  @Before("execution(public void com.geekbrains.aop.*.*(..))") // pointcut expression
  public void beforeAnyMethodInUserDAOClass() {
      System.out.println("AOP: любой метод без аргументов любого класса");
  }

  @AfterReturning(
          pointcut = "execution(public * com.geekbrains.aop.UserDAO.getAllUsers(..))",
          returning = "result")
  public void afterGetBobInfo(JoinPoint joinPoint, List<String> result) {
    result.set(0, "Donald Duck");
  }

  @AfterThrowing(
          pointcut = "execution(public * com.geekbrains.aop.UserDAO.*(..))",
          throwing = "exc")
  public void afterThrowing(JoinPoint joinPoint, Throwable exc) {
      System.out.println(exc); // logging
  }

  @Around("execution(public * com.geekbrains.aop.UserDAO.*(..))")
  public Object methodProfiling(ProceedingJoinPoint proceedingJoinPoint) throws Throwable {
    System.out.println("start profiling");
    long begin = System.currentTimeMillis();
    Object out = proceedingJoinPoint.proceed();
    long end = System.currentTimeMillis();
    long duration = end - begin;
    System.out.println((MethodSignature) proceedingJoinPoint.getSignature() + " duration: " + duration);
    System.out.println("end profiling");
    return out;
  }
}

```
`JoinPoint joinPoint` - отсюда можно получить информацию о методе, его сигнатуру итд, точка подключения к методу.

```java
@Before("articleListPointcut()")
public void beforeAdvice(JoinPoint joinPoint) {
    log.info(
      "Method {} executed with {} arguments",
      joinPoint.getStaticPart().getSignature(),
      joinPoint.getArgs()
    );
}
```
ProceedingJoinPoint — это расширение JoinPoint, предоставляющее дополнительный метод continue ().
Главное отличие мы можем управлять процессом запуска.

Например, если выпало исключение мы можем еще раз вызывать метод, пример ниже:

```java
@Around("articleListPointcut()")
public Object aroundAdvice(ProceedingJoinPoint pjp) {
    try {
        return pjp.proceed(pjp.getArgs());
    } catch (Throwable) {
        log.error(e.getMessage(), e);
        log.info("Retrying operation");
        return pjp.proceed(pjp.getArgs());
    }
}
```

>Spring AOP по умолчанию использует стандартные динамические прокси JDK для прокси AOP. Это позволяет проксировать любой интерфейс (или набор интерфейсов)

>Spring AOP также может использовать прокси CGLIB(библиотека автогенерации кода). Это необходимо для проксирования классов, а не интерфейсов. CGLIB используется по умолчанию, если бизнес-объект не реализует интерфейс.
</details>

[в меню _Spring Framework_](#Spring-Framework)












<details> 
  <summary>Правильный ответ</summary>


</details>

[в меню _Spring Framework_](#Spring-Framework)

![Все о ThreadLocal](images/ "Все о ThreadLocal")