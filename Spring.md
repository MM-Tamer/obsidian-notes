![[Pasted image 20250318160659.png]]
[[Hibernate]]

---
## Spring Core

Spring is built around the the core concept of dependency injection (design pattern) which is an implementation of IoC (inversion of control).

Spring does this by using a _configuration container_ called `ApplicationContext`.
### What is a Configuration Container?

A **Java configuration container** is part of an IoC framework that:

- **Creates** objects (beans).
    
- **Wires** dependencies (injects them).
    
- **Manages** lifecycle (init, destroy, scope, etc.).
    
- Uses **configuration** (either XML, annotations, or Java code) to understand what to build and how to inject dependencies.
### There are 3 different types of containers
1. XML-Based Configuration 
2. Annotation-Based Configuration
3. Java-Based Configuration (JavaConfig)

---
#### **XML-based configuration** (old-school):
There are multiple ways to handle DI using XML either through `<property name="" ref="" />` tag or the `<constructor-arg ref=""></constructor-arg>`

```xml title:beans.xml
<?xml version="1.0" encoding="UTF-8"?>

<beans xmlns="http://www.springframework.org/schema/beans"

    xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"

    xmlns:context="http://www.springframework.org/schema/context"

    xsi:schemaLocation="http://www.springframework.org/schema/beans

    http://www.springframework.org/schema/beans/spring-beans.xsd

    http://www.springframework.org/schema/context

    http://www.springframework.org/schema/context/spring-context.xsd">
<!-- beans.xml --> 
<beans>     
	<bean id="userService" class="com.example.UserService">
	   <property name="repo" ref="userRepository" />
	</bean>
	<bean id="userRepository" class="com.example.UserRepository" />
	
	<bean id="controller" class="spring.core.start.Controller">
        <constructor-arg ref="admin"></constructor-arg>
    </bean>
    <bean id="admin" class="spring.core.start.AdminService">
    </bean>
	 
	 
</beans>
```

```java title:main.java
ApplicationContext context = new ClassPathXmlApplicationContext("beans.xml"); 
UserService service =  context.getBean("userService", UserService.class);
```
##### Including a Properties File in XML

```xml title:context.xml
<context:property-placeholder location="classpath:data.properties"/> 
<!--data.properties is the file where the data is stored -->
<bean id="admin" class="spring.core.start.AdminService">
	<property name="username" ref="${app.user.name}"/>
</bean>
```
---
The scope of beans is by default a `singleton`. while `prototype` creates a new bean for every request.

> [!WARNING] Prototype Beans Management
> Destroy-method doesn't work on prototype beans and they're garbage collected once the beans go out of scope. Since retaining a potentially large number of beans during the lifetime of the container can pose a significant risk of memory leakage.

---
#### **Annotation configuration** (modern):
There are two ways to use annotation configuration either by creating a configuration class or using an XML file.
###### 1.Using XML File
```xml title:context.xml
<?xml version="1.0" encoding="UTF-8"?>

<beans xmlns="http://www.springframework.org/schema/beans"

    xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"

    xmlns:context="http://www.springframework.org/schema/context"

    xsi:schemaLocation="http://www.springframework.org/schema/beans

    http://www.springframework.org/schema/beans/spring-beans.xsd

    http://www.springframework.org/schema/context

    http://www.springframework.org/schema/context/spring-context.xsd">

  <context:component-scan base-package="com"></context:component-scan>

</beans>
```
```java title:main.java
ApplicationContext context = new ClassPathXmlApplicationContext("beans.xml"); 
UserService service =  context.getBean("userService", UserService.class);
```
```java title:UserService.java
@Component
public class UserService{}
```

###### 2.Using Config Class
```java title:
@Configuration
@ComponentScan("com.example")
public class AppConfig {}

ApplicationContext context = new AnnotationConfigApplicationContext(AppConfig.class);
UserService service = context.getBean(UserService.class);
```

##### Different Types Of Annotations
- `@Component("bean_id")` designates a class as a bean. _default bean name is camelCase class name_
- `@Autowired` designates a dependency injection.
- `@Qualifier("bean")` designates which bean to inject in the case of multiple matching beans.
 ```java title:example.java
@Component
public class NotificationManager {

    private final MessageService messageService;

    @Autowired
    public NotificationManager(@Qualifier("smsService") MessageService messageService) {
        this.messageService = messageService;
    }

    public void notify(String msg) {
        messageService.send(msg);
    }
}

```
- `@PostConstruct` declares an init-method.
- `@PreDestroy` declares a destroy-method.
- `@Scope("prototype")` determines the scope of the bean.
- `@Value("${app.user.name}")` retrieves a value from a properties or yaml file.
- `@Configuration`to designate the container class. 
	- conventionally the name of the config class is _SpringConfig_
- `@ComponentScan("com.spring.start")` to designate the base package to be scanned for components.
- `@PropertySource("classpath:data.properties")` to designate the properties or yaml file from which to retrieve data.
- `@Bean("bean_id")` to manually create a bean within the configuration class by creating a function with the return type of the desired bean class and using the `@Bean` annotation, the default id of the bean will be the function name. This is used when creating beans from READ-ONLY classes or in similar situations.




## Spring Boot
Spring Boot is built on top of the spring framework and it simplifies and abstracts many of the complexities and configurations of spring.
### Maven
`pom.xml` is a configuration file used by **Apache Maven**, which is a build automation and project management tool primarily for **Java** projects.

#### What does `pom.xml` stand for?

- **POM** = _Project Object Model_
    
- It's an XML file that contains information about the project and configuration details used by Maven to build the project.
    

---

#### Key things `pom.xml` does:

1. **Defines the project structure and metadata**
    
    - Project name, version, description, etc.
        
2. **Manages dependencies**
    
    - You can specify external libraries (like Spring Boot, Hibernate, etc.), and Maven will automatically download and manage them for you.
        
3. **Build configuration**
    
    - Tells Maven how to compile, package, test, and deploy the project.
        
4. **Plugins**
    
    - You can add Maven plugins for tasks like compiling code, running tests, generating reports, etc.

>[!tip] Use https://start.spring.io/ to jumpstart your project.

#### Parent 

### File Structure In Spring Boot
src/main/java for java files

src/main/resources - /static for css, bootstrap and other static files
				 |__> application.properties  for configuration parameters such as: database url, driver-class-name, username & password.
				 Spring boot automatically detects application.properties

### `@SpringBootApplication`
```java 
import org.springframework.boot.SpringApplication;
import org.springframework.boot.autoconfigure.SpringBootApplication;

@SpringBootApplication
public class MyApplication {
    public static void main(String[] args) {
        SpringApplication.run(MyApplication.class, args);
    }
}
```

`@SpringBootApplication` is an annotation in the Spring Boot framework that is used to mark the main class of a Spring Boot application. It enables several essential Spring features and simplifies the configuration by combining three annotations into one:

1. `@SpringBootConfiguration`: Equivalent to `@Configuration`, it tells Spring that this class contains configuration settings and beans for the application context.
    
2. `@EnableAutoConfiguration`: This instructs Spring Boot to automatically configure your application based on the dependencies present in your classpath. It saves developers from having to manually configure things like database connections, web servers, or messaging systems.
    
3. `@ComponentScan`: This tells Spring to scan the current package and its sub-packages for Spring components like controllers, services, and repositories, and automatically register them in the application context.

### `@RestController` & `@Controller`

`@Controller` assumes that you're building a monolithic (MVC) app while `@RestController` means that you're building an API.


### `@Repository`
```java title:

@Repository
public interface ApplicationRepo extends JpaRepository<Application, Long> {

}
```
Using JpaRepository offers a range of predefined functions such as findAll()


### RestController -> Service -> Repository
```java title:ApplicationController
import org.springframework.web.bind.annotation.RestController;
import java.util.List;

@RestController
public class ApplicationController {

    @Autowired
    private ApplicationService applicationService;

    @GetMapping("/applications")
    public List<Application> getApplications() {
        return applicationService.getApplications();
    }
}

```
```java title:ApplicationServiceImpl
@Service
public class ApplicationServiceImpl implements ApplicationService {

    @Autowired
    private ApplicationRepo applicationRepo;

    @Override
    public List<Application> getApplications() {
        return applicationRepo.findAll();
    }
}

```
```java title:ApplicationRepo

@Repository
public interface ApplicationRepo extends JpaRepository<Application, Long> {

}
```



### RestController
#### Annotations
- `@GetMapping("/url")`
- `@PostMapping("/url")`
- `@DeleteMapping("/url")` , return type has to be void.
- `@RequestBody` to mark that the incoming data is contained within the request body. Usable only for objects not primitives.
- `@RequestParam` to accept primitives as request parameters.
```java title:RequestParam
	@PostMapping("/age") // url: /age?age=21
	public ResponseEntity<String> setAge(@RequestParam int age) {
    return ResponseEntity.ok("Age set to " + age);
}
```
 - `@PathVariable`
```java title:PathVariable
@GetMapping("/user/{id}") // url: /user/10
public ResponseEntity<String> getUserById(@PathVariable int id) {
    return ResponseEntity.ok("User ID: " + id);
}
```