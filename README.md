# Projeto web services com Spring Boot e JPA / Hibernate 

### Objetivos 

- Criar projeto Spring Boot Java 
- Implementar modelo de domínio 
- Estruturar camadas lógicas: resource, service, repository 
- Configurar banco de dados de teste (H2) 
- Povoar o banco de dados 
- CRUD - Create, Retrieve, Update, Delete 
- Tratamento de exceções 

![Projeto-web-services-Spring-Boot-JPA-1](https://user-images.githubusercontent.com/81713250/133672827-e8420715-3a8e-49ac-803b-9f0071302e9e.png)

### Domain Model

![Projeto-web-services-Spring-Boot-JPA-2](https://user-images.githubusercontent.com/81713250/133673436-1631378a-fa34-410e-95d6-a3c4d0266312.png)

### Domain Instance

![Projeto-web-services-Spring-Boot-JPA-3](https://user-images.githubusercontent.com/81713250/133673574-e0aedf51-d146-4cbd-b2ec-6707b21a012f.png)

### Logical Layers 

![Projeto-web-services-Spring-Boot-JPA-4](https://user-images.githubusercontent.com/81713250/133673671-ae542a97-3c98-4efe-a80b-1fc233760431.png)

### Project created

**Checklist:** 

- File -> New -> Spring Starter Project 
  - Maven 
  - Java 11 
  - Packing JAR 
  - Dependencies: Spring Web Starter



### User entity and resource

**Basic entity checklist:** 

- Basic attributes 
- Associations (instantiate collections) 
- Constructors 
- Getters & Setters (collections: only get) 
- hashCode & equals 
- Serializable 



### H2 database, test profile, JPA 

**Checklist:** 

- JPA & H2 dependencies 
- application.properties 
- application-test.properties 
- Entity: JPA mapping 

**Dependencies:**  

&lt;dependency&gt;<br>
&emsp;&lt;groupId&gt;org.springframework.boot&lt;/groupId&gt;<br>
&emsp;&lt;artifactId&gt;spring-boot-starter-data-jpa&lt;/artifactId&gt;<br>
&lt;/dependency&gt;<br>

&lt;dependency&gt;<br>
&emsp;&lt;groupId&gt;com.h2database&lt;/groupId&gt;<br>
&emsp;&lt;artifactId>h2&lt;/artifactId&gt;<br>
&emsp;&lt;scope>runtime&lt;/scope&gt;<br>
&lt;/dependency&gt;<br>

**application.properties:**  <br>

spring.profiles.active=test<br>

spring.jpa.open-in-view=true<br>

**application-test.properties:** <br>

 spring.datasource.url=jdbc:h2:mem:testdb <br>
spring.datasource.username=sa <br>
spring.datasource.password= <br>

spring.h2.console.enabled=true <br>
spring.h2.console.path=/h2-console <br>

spring.jpa.show-sql=true <br>
spring.jpa.properties.hibernate.format_sql=true<br>



### JPA repository, dependency injection, database seeding 

**Checklist:** 

- UserRepository extends JPARepository<User, Long> 
-  Configuration class for "test" profile 
-  @Autowired UserRepository 
-  Instantiate objects in memory 
-  Persist objects 

**Objects:** <br>
User u1 = new User(null, "Maria Brown", "maria@gmail.com", "988888888", "123456"); <br>
User u2 = new User(null, "Alex Green", "alex@gmail.com", "977777777", "123456"); <br>



### Service layer, component registration 



### Order, Instant, ISO 8601 

**Basic new entity checklist:** 

- Entity 
  - "To many" association, lazy loading, JsonIgnore 
- Repository 
-  Seed 
-  Service 
-  Resource 

**Objects:** <br>
Order o1 = new Order(null, Instant.parse("2019-06-20T19:53:07Z"), u1); <br>
Order o2 = new Order(null, Instant.parse("2019-07-21T03:42:10Z"), u2); <br>
Order o3 = new Order(null, Instant.parse("2019-07-22T15:21:22Z"), u1); <br>



### OrderStatus enum 



### Category 

**Objects:** <br>
Category cat1 = new Category(null, "Electronics"); <br>
Category cat2 = new Category(null, "Books"); <br>
Category cat3 = new Category(null, "Computers"); <br>



### Product 

**Objects:**<br>Product p1 = new Product(null, "The Lord of the Rings", "Lorem ipsum dolor sit amet, consectetur.", 90.5, ""); <br>
Product p2 = new Product(null, "Smart TV", "Nulla eu imperdiet purus. Maecenas ante.", 2190.0, ""); <br>
Product p3 = new Product(null, "Macbook Pro", "Nam eleifend maximus tortor, at mollis.", 1250.0, ""); <br>
Product p4 = new Product(null, "PC Gamer", "Donec aliquet odio ac rhoncus cursus.", 1200.0, ""); <br>
Product p5 = new Product(null, "Rails for Dummies", "Cras fringilla convallis sem vel faucibus.", 100.99, ""); <br>

### Many-to-many association with JoinTable 



### OrderItem, many-to-many association with extra attributes 

**Checklist:** <br>

- OrderItemPK 
-  OrderItem 
-  Order one-to-many association 
-  Seed 

**Objects:** <br>
OrderItem oi1 = new OrderItem(o1, p1, 2, p1.getPrice()); <br>
OrderItem oi2 = new OrderItem(o1, p3, 1, p3.getPrice()); <br>
OrderItem oi3 = new OrderItem(o2, p3, 2, p3.getPrice()); <br>
OrderItem oi4 = new OrderItem(o3, p5, 2, p5.getPrice()); <br>

 

### Product-OrderItem one-to-many association 

 

### Payment, one-to-one association 

 

### Subtotal & Total methods 



### User insert 

**Checklist:** 

- UserService 
-  UserResource 

**Test:** <br>
{ <br>
    &emsp;"name": "Bob Brown", <br>
    &emsp;"email": "bob@gmail.com", <br>
    &emsp;"phone": "977557755", <br>
   &emsp; "password": "123456" <br>
} <br>



### User delete 

**Checklist:** 

- UserService 
-  UserResource 



### User update 

 **Checklist:** 

- UserService 
-  UserResource 

**Test:** <br>
{ <br>
    &emsp;"name": "Bob Brown", <br>
    &emsp;"email": "bob@gmail.com", <br>
    &emsp;"phone": "977557755" <br>
}<br>



### Exception handling - findById 

**Checklist:** 

- NEW CLASS: services.exceptions.ResourceNotFoundException 
-  NEW CLASS: resources.exceptions.StandardError 
-  NEW CLASS: resources.exceptions.ResourceExceptionHandler 
-  UserService 





### Exception handling - delete 

 **Checklist:** 

- NEW CLASS: services.exceptions.DatabaseException 
-  ResourceExceptionHandler 
-  UserService 
  - EmptyResultDataAccessException 
  -  DataIntegrityViolationException 

 

### Exception handling - update 

**Checklist:** 

- UserService 
  - EntityNotFoundException 



### Create Heroku app & provision PostgreSQL 

 **Checklist:** 

- Heroku Sign Up 
-  Create app 
-  Provision PostgreSQL 
  - App dashboard -> Resources 
  -  Search "postgres" -> select "Heroku Postgres" 

 

### Install local PostgreSQL 

 **Checklist:** 

- Download and install: https://www.postgresql.org/download/ 
  - Super user: postgres 
  -  Password: 1234567 
  -  Port: 5432 
- Start/stop service: Task manager -> Services 
-  Check instalation 
  - Start pgAdmin 
  -  Databases -> Create -> Database 
    - Encoding: UTF8 



### Dev profile 

**Checklist:** 

- PgAdmin: create local database: create database springboot_course 

- Add PostgreSQL Maven dependency 

&lt;dependency&gt;<br>
 &emsp;&lt;groupId&gt;org.postgresql&lt;/groupId&gt; <br>
 &emsp;&lt;artifactId&gt;postgresql&lt;/artifactId&gt;<br>
 &emsp;&lt;scope&gt;runtime&lt;/scope&gt; <br>
&lt;/dependency&gt;<br>

- Create file: application-dev.properties  

spring.datasource.url=jdbc:postgresql://localhost:5432/springboot_course <br>
spring.datasource.username=postgres <br>
spring.datasource.password=1234567 <br>

spring.jpa.properties.hibernate.jdbc.lob.non_contextual_creation=true <br>
spring.jpa.hibernate.ddl-auto=update <br>
spring.jpa.show-sql=true <br>
spring.jpa.properties.hibernate.format_sql=true <br>

jwt.secret=MYJWTSECRET <br>
jwt.expiration=3600000 <br>

 

- Update application.properties: spring.profiles.active=dev 

 

- Run application 



### Get SQL script from local PostgreSQL 

- PgAdmin: get SQL script: 
  - Select database 
  -  Tools -> Backup 
    - Format: Plain 
    -  Encoding: UTF8 
    -  Dump options: 
      - Only schema: YES 
      -  Blobs: NO 
      -  Do not save: (ALL) 
      -  Verbose messages: NO 

 

- Delete instructions before CREATE statements 



### Run SQL Script  

**Checklist:** 

- App dashboard -> Settings - > Config Vars 

**EXAMPLE:**<br>
postgres://wavglvupbdad:358f443aafe452eca4c58fbc15d02e50b08130c7aaea3aff6c4f59c
13f9abb@ec2-23-21-106-266.compute-1.amazonaws.com:5432/d7u9ub86cdsu 

**user:** wavglvupbdad 

**password:** 358f443aafe452eca4c58fbc15d02e50b08130c7aaea3aff6c4f59c13f9abb 

**server:** ec2-23-21-106-266.compute-1.amazonaws.com 

**port:** 5432 

**database:** d7u9ub86cdsu 

- PgAdmin: Servers -> Create -> Server 
  - Advanced -> DB rescriction: (database) 

- Database -> Query Tool 
  - Load and run SQL Script 



### Deploy app to Heroku 

- Heroku app dashboard -> Deploy <br>
  heroku git:remote -a myapp<br>
  git remote -v <br>

- Setup Heroku app Config Vars 
  - DATABASE_URL 
  -  JWT_EXPIRATION 
  -  JWT_SECRET 

- Create: application-prod.properties 

spring.datasource.url=${DATABASE_URL} <br>

spring.jpa.hibernate.ddl-auto=none <br>
spring.jpa.show-sql=false <br>
spring.jpa.properties.hibernate.format_sql=false <br>

jwt.secret=${JWT_SECRET} <br>
jwt.expiration=${JWT_EXPIRATION} <br>



- Update application.properties: spring.profiles.active=prod 

- Create files: system.properties  

java.runtime.version=11 

# Desenvolvido por:
 * Brígido Sigá.

 

- Send to Heroku: <br>
  git add . <br>
  git commit -m "Deploy app to Heroku" <br>
  git push heroku master <br>
