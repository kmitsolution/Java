# Spring Boot Actuator
1. Monitors and manage your application in production.
2. It provides number of endpoints <br />
    <b>beans:</b> Complete list of beans <br />
    <b>health:</b> Application health information <br />
    <b>metrics:</b> Application metrics <br />
    <b>mappings:</b> Details around Request Mapping <br />
    
Add maven dependency in the pom.xml file

```xml
		<dependency>
			<groupId>org.springframework.boot</groupId>
			<artifactId>spring-boot-starter-actuator</artifactId>
		</dependency>		
```
Run the application and visit to <a href=http://localhost:8080/actuator />http://localhost:8080/actuator</a> url.    

If you want to see all the web monitoring endpoints then add below line in <b>applicaiton.properties</b> file.
```
management.endpoints.web.exposure.include=*
```
In case if you want only limited endpoints to be configured

```
management.endpoints.web.exposure.include=health,metrics
```
