# SpringBoot with JPA, HIBERNATE and CUSTOM TOKEN AUTH

### REQUIREMENTS
* Java 8
* Maven 3.5.2 or higher
* GIT

### Installation
```
  > git pull git@github.com:fibanez6/springboot-boilerplate.git
  > cd custom-token-auth
  > mvn clean install
```

### Execution

```
  > java -jar target/custom-token-auth-1.0-SNAPSHOT.jar
```
or
```
  > mvn spring-boot:run
```

### REST API

* Swagger REST API Documentation
```
  > http://localhost:8080/swagger-ui.html#/
```


### Dependencies

* **spring-boot** version 1.5.9.RELEASE
   * **spring-boot-starter-web**
   * **spring-boot-starter-data-jpa**
   * **spring-boot-starter-actuator**
   * **spring-boot-starter-security**
* **Lombok** version 1.16.16. 

  > [Project Lombok](https://projectlombok.org/) is a java library that automatically plugs into your editor and build tools, spicing up your java.
Never write another getter or equals method again.

* **Swagger2** version 2.6.1
  > [Swagger](https://swagger.io/) is an open source software framework backed by a large ecosystem of tools that helps developers design, build, document, and consume RESTful Web services. 
While most users identify Swagger by the Swagger UI tool, the Swagger toolset includes support for automated documentation, code generation, and test case generation.

* **h2** version 1.4.196
  > [H2](http://www.h2database.com/html/main.html) is a relational database management system written in Java. It can be embedded in Java applications or run in the client-server mode.

### Spring Boot configuration
```
server.port = ${port:8080}

###
#   Actuator
###
management.port=8081
management.address=127.0.0.1
management.info.git.mode=full
management.security.enabled=false
management.context-path=/manage

###
#   Database Settings
###
spring.datasource.url=jdbc:h2:~/db/database.db;DB_CLOSE_ON_EXIT=TRUE;INIT=create schema IF NOT EXISTS test;
spring.datasource.platform=h2
spring.datasource.username =sa
spring.datasource.password =
spring.datasource.driverClassName = org.h2.Driver

###
#   H2 Settings
###
spring.h2.console.enabled=true
spring.h2.console.path=/console
spring.h2.console.settings.trace=false
spring.h2.console.settings.web-allow-others=false

###
#   Hibernate Settings
###
spring.jpa.database-platform=org.hibernate.dialect.H2Dialect
spring.jpa.properties.hibernate.ddl-auto = create-drop
spring.jpa.properties.hibernate.show_sql=true
spring.jpa.properties.hibernate.use_sql_comments=false
spring.jpa.properties.hibernate.format_sql=true
```

* **spring.datasource.***: sets up an in-memory H2 database;
* **spring.datasource.initialize**: tells spring-boot to initialize the database with scripts;
* **spring.datasource.schema**: the schema sql script to load. By default it is schema-${platform}.sql then schema.sql;
* **spring.datasource.data**: the data sql script. By default, it is data-${platform}.sql then data.sql;
* **spring.h2.console.enabled**: allow us to access the memory database from a web interface;
* **spring.jpa.hibernate.ddl-auto**: hibernates also tries to initialize the database. 
When it detects an embedded database, it sets ddl-auto to create-drop and initialize the database with entities annotated with @Table (and also looks for imports.sql). 
This may lead to creating the same table twice. I prefer to stick with Spring Boot magic, so I set this to none

### END POINTS
```
[8080]
[/reporting/network_a/{account_id}/{app_id}/{date}],methods=[POST],produces=[application/json]
[/reporting/network_b/{date}/{account_id}/{app_id}],methods=[POST],produces=[text/plain]
[/v2/api-docs],methods=[GET],produces=[application/json || application/hal+json]
[/swagger-resources]
[/swagger-resources/configuration/security]
[/swagger-resources/configuration/ui]
[/error],produces=[text/html]
[/swagger-ui.html]

```
```
[8081]
[/manage/autoconfig || /manage/autoconfig.json],methods=[GET],produces=[application/vnd.spring-boot.actuator.v1+json || application/json]
[/manage/trace || /manage/trace.json],methods=[GET],produces=[application/vnd.spring-boot.actuator.v1+json || application/json]
[/manage/loggers/{name:.*}],methods=[GET],produces=[application/vnd.spring-boot.actuator.v1+json || application/json]
[/manage/loggers/{name:.*}],methods=[POST],consumes=[application/vnd.spring-boot.actuator.v1+json || application/json],produces=[application/vnd.spring-boot.actuator.v1+json || application/json]
[/manage/loggers || /manage/loggers.json],methods=[GET],produces=[application/vnd.spring-boot.actuator.v1+json || application/json]
[/manage/mappings || /manage/mappings.json],methods=[GET],produces=[application/vnd.spring-boot.actuator.v1+json || application/json]
[/manage/heapdump || /manage/heapdump.json],methods=[GET],produces=[application/octet-stream]
[/manage/configprops || /manage/configprops.json],methods=[GET],produces=[application/vnd.spring-boot.actuator.v1+json || application/json]
[/manage/metrics/{name:.*}],methods=[GET],produces=[application/vnd.spring-boot.actuator.v1+json || application/json]
[/manage/metrics || /manage/metrics.json],methods=[GET],produces=[application/vnd.spring-boot.actuator.v1+json || application/json]
[/manage/health || /manage/health.json],methods=[GET],produces=[application/vnd.spring-boot.actuator.v1+json || application/json]
[/manage/beans || /manage/beans.json],methods=[GET],produces=[application/vnd.spring-boot.actuator.v1+json || application/json]
[/manage/info || /manage/info.json],methods=[GET],produces=[application/vnd.spring-boot.actuator.v1+json || application/json]
[/manage/auditevents || /manage/auditevents.json],methods=[GET],produces=[application/vnd.spring-boot.actuator.v1+json || application/json]
[/manage/dump || /manage/dump.json],methods=[GET],produces=[application/vnd.spring-boot.actuator.v1+json || application/json]
[/manage/env/{name:.*}],methods=[GET],produces=[application/vnd.spring-boot.actuator.v1+json || application/json]
[/manage/env || /manage/env.json],methods=[GET],produces=[application/vnd.spring-boot.actuator.v1+json || application/json]


```
