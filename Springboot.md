### Intial set-up

- Select java with web,sts,Eclipse
- Goto spring boot initializr
- Select package name
- Edit other fields
- Select java
- And accordingly

## Extension

- Spring Boot Extension Pack
- Java extension Pack

Wait to complete the setup
Make folder like sub package

Folder structure
Com.example.app
Com.example.app.controllers
Com.example.app.entities
Com examole.app.services

The file that are made with .java
Make default constructor
Make other constructor
Make getter and setter
Make tostrings methods

Annotations used
@GetMapping
@services
@controller

For web page

1. Make a file in main>views>home.jsp
2. Add code in application.properties

``` spring.mvc.view.prefix=/views/
spring.mvc.view.suffix=.jsp
```

add dependency

Jaspher is used as servlet to execute `HTML`, `Javascript`, etc

```
<!-- https://mvnrepository.com/artifact/org.apache.tomcat.embed/tomcat-embed-jasper -->
<dependency>
    <groupId>org.apache.tomcat.embed</groupId>
    <artifactId>tomcat-embed-jasper</artifactId>
    <version>10.1.0-M11</version>
</dependency>

```

add dependency for auto rebuild after editinng

```
<!-- https://mvnrepository.com/artifact/org.springframework.boot/spring-boot-devtools -->
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-devtools</artifactId>
    <version>2.6.4</version>
</dependency>
```

In Mycontroller
Add a function for `@RequestMapping`

```
@RequestMapping("/")
public String home()
{
    System.out.println("This is home page");
    return "homr";

}
```

JPA *java persistence*

- its orm tool , orm is third party tool
- java is object oriented follower
- It help in sql querying

|  id |  Name |  City | City |
---|---|---|---
|||||
|||||
|||||

## Method to connect sql database through spring boot

- install the dependency of jpa
- Press `ctr+shift+T` in eclipse on any java file in editor then search `mysql` and select 55 dilect

```
 * Hibernate, Relational Persistence for Idiomatic Java
 *
 * License: GNU Lesser General Public License (LGPL), version 2.1 or later.
 * See the lgpl.txt file in the root directory or <http://www.gnu.org/licenses/lgpl-2.1.html>.
 */
package org.hibernate.dialect;

/**
 * An SQL dialect for MySQL 5.5.x specific features.
 *
 * @author Vlad Mihalcea
 */
public class MySQL55Dialect extends MySQL5Dialect {

 @Override
 protected MySQLStorageEngine getDefaultMySQLStorageEngine() {
  return InnoDBStorageEngine.INSTANCE;
 }
}
```

- some java class as above will be created

- then copy the class `org.hibernate.dialect` and class name `MySQL55Dialect` and place it in `spring.jpa.properties.hibernate.dilect`
as `org.hibernate.dialect.MySQL55Dialect` in application.properties`
configuration of file `application.properties` with following syntax

```
    spring.datasource.name=new_schema
    spring.datasource.url=jdbc:mysql://localhost:3306/new_schema?serverTimezone=UTC
    spring.datasource.username=root
    spring.datasource.password=password
    spring.flyway.driver-class-name=com.cj.jdbc.Driver
    spring.jpa.properties.hibernate.dilect=org.hibernate.dialect.MySQL55Dialect
    spring.jpa.hibernate.ddl-auto=update

```

`spring.jpa.hibernate.ddl-auto=update` this is for auto table creation in sql schemma database no need to do manually.
now in main java class
write the test code like this

```
  ApplicationContext context =SpringApplication.run(DemoApplication.class, args);
  
  UserRepository userRepository = context.getBean(UserRepository.class);
  
  Course course = new Course();
  course.setTitle("Aditya");
  course.setDescription("First");
  Course course1 = userRepository.save(course);
  System.out.println(course1);
```

output should be
`Course [id=1, title=Aditya, description=First]`

Spring boot dev tool *To better auto run without rebuild*

> info

`@Controller`send the view if gets post request and need to assign `@ResponseBody`
`@RestController` send the String body and no need to define `@ResponseBody`

`@ResquestMapping(value = "/books", method = RequestMethod.GET)` vs
`@GetMapping("/books")` second one is betther no need to define method.

Folder Structure
<!-- ```
.
+-- _config.yml
+-- _drafts
|   +-- begin-with-the-crazy-ideas.textile
|   +-- on-simplicity-in-technology.markdown
+-- _includes
|   +-- footer.html
|   +-- header.html
+-- _layouts
|   +-- default.html
|   +-- post.html
+-- _posts
|   +-- 2007-10-29-why-every-programmer-should-play-nethack.textile
|   +-- 2009-04-26-barcamp-boston-4-roundup.textile
+-- _data
|   +-- members.yml
+-- _site
+-- index.html
``` -->
```
+-- Project Folder
|   +-- src
    |   +-- main
        |   +-- webapp
            |   +-- views
                |   +-- jsppages.jsp

```
Books to refer for spring boot
1. Spring boot in Action
2. Learn Spring Boot 2.0
3. Mastering Spring Boot 2.0
4. Spring Microservices in Action
5. Learn by Doing
6. Prefer docs for learning