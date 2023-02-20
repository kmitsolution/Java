# Spring Boot Starters
Spring Boot provides variety of starter projects. In current Spring Boot project, pom.xml file contains the dependencies for starter projects

```xml
<dependencies>
		<dependency>
			<groupId>org.springframework.boot</groupId>
			<artifactId>spring-boot-starter-web</artifactId>
		</dependency>

		<dependency>
			<groupId>org.springframework.boot</groupId>
			<artifactId>spring-boot-starter-test</artifactId>
			<scope>test</scope>
		</dependency>
	</dependencies>
```
1. <b>Web Application & REST API</b> Spring Boot Starter Web (spring-webmvc, spring-web, spring-boot-starter-tomcat, spring-boot-starter-json)
2. <b>Unit Tests</b> Spring Boot Starter Test
3. <b>JPA</b> Spring Boot Starter Data JPA
4. <b>JDBC</b> Spring Boot Starter JDBC
5. <b>Secure Web Application & REST API </b> Spring Boot Starter Security
