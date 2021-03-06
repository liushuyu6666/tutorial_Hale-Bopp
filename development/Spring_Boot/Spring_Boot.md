---

---

# Spring Boot

## start

### creat project

Go to [click here](https://start.spring.io/) unzip the file, now this file is the project root, use IntelliJ to open it, then a new file called .gradle will be created

Make sure your project is under java 1.8 by check "File - Project Structure" in IntelliJ.

![project structure](img/project_structure.png)



### add dependencies

Add dependencies in build.gradle from [here](https://mvnrepository.com/artifact/org.springframework.boot), dependencies are here:

- `spring-boot-web-starter`: develop base on RESTful services;
- `spring-boot-starter-security`: access-control features;
- `io.jsonwebtoken`: for token;
- `spring-boot-starter-data-jpa`: for relational database access, if we use `mongodb`, don't include this one;
- `spring-boot-starter-data-mongodb`: for mongo database access;
- `aws-java-sdk`: AWS related development.

Every time when you add new dependency, you will have a `gradle` icon:

<img src="img/load_dependencies.png" alt="load icon" style="zoom:50%;" />

click on the icon to load the new dependency.



## annotation



### `@Bean`

To declare a bean, simply annotate a method with the `@Bean` annotation. When JavaConfig encounters such a method, it will execute that method and register the return value as a bean within a `BeanFactory`. By default, the bean name will be the same as the method name. 

[reference here](https://docs.spring.io/spring-javaconfig/docs/1.0.0.M4/reference/html/ch02s02.html)

### `@Component`

`@Component` is the most generic Spring annotation. A Java class decorated with `@Component` is found during classpath scanning and registered in the context as a Spring bean. `@Service`, `@Repository`, and `@Controller` are specializations of `@Component`, which are used for more specific cases.

`@ComponentScan` ensures that the classes decorated with `@Component` are found and registered as Spring beans. `@ComponentScan` is automatically included with `@SpringBootApplication`. 

[reference here](https://zetcode.com/springboot/component/)

## spring boot security

### Libraries

#### `HttpSecurity`

- `cors()`: add `CorsFilter`
- `csrf()`

#### `io.jsonwebtoken`

- [JwtParser](http://javadox.com/io.jsonwebtoken/jjwt/0.4/io/jsonwebtoken/JwtParser.html)
  - [`setSigningKey`](http://javadox.com/io.jsonwebtoken/jjwt/0.4/io/jsonwebtoken/JwtParser.html#setSigningKey-byte:A-)
  - [`parseClaimsJws`](



### Filter

#### Filter function

- `JWTAuthencicationFilter`

  Two important components, `attemptAuthentication`  try to verify the `jwt`  and `successfulAuthentication` generate to `jwt`. 

  - `attemptAuthentication` : 

    1. get `username` and `password` from `req` .

    2. load `usernamePasswordAuthenticationToken (class: UsernamePasswordAuthenticationToken)` by `username` and `password`. 

       <img src="img/security_usernamePasswordAuthenticationToken.png" style="zoom:67%;" />

    3. authenticate `UsernamePasswordAuthenticationToken` and return `authentication (class: Authentication)` if match, or throw `Exception`.

       <img src="E:img/security_authentication.png" alt="j" style="zoom:50%;" />

  - `successfulAuthentication` :

    1. generate `jwt` via `JwtUtils`, which is a `class` create by yourself.

  - 

#### Filter Ordering

[reference](https://docs.spring.io/spring-security/site/docs/3.0.x/reference/security-filter-chain.html)



## Question need to be finished

- what is bean
- what is IoC container

## Bean

### Intuition

When the program start, beans (annotated as `@Entity`, `@Service`, `Component`, etc ) will be initialized in the memory, when we use `Autowired`, it refers its instance but will not create a new one.

### Java Bean and Spring Boot Bean

[click here](https://stackoverflow.com/questions/21866571/difference-between-javabean-and-spring-bean)