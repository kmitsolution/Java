Let's create first RESTful API using <a href="https://start.spring.io/" >spring initalizer </a>
1. Provide project metadata ( <b>Group:</b>->com.example.rest.webservices,<b>Artifact:-</b>restful-webservices,<b>Name:-</b>restful-webservices, <b>Package Name:-</b>com.example.rest.webservices.restful-webservices.
2. Add Dependencies (Spring Web,JPA,DevTools,H2 Database).
3. Click on Generate button.
4. Open the project in Eclipse.
5. create a class <b>HelloWorld</b> in <b>com.example.rest.webservices.restfulwebservices.helloworld package</b>
 ```java
 
package com.example.rest.webservices.restfulwebservices.helloworld;
import org.springframework.web.bind.annotation.RequestMapping;
import org.springframework.web.bind.annotation.RequestMethod;
import org.springframework.web.bind.annotation.RestController;

@RestController
public class HelloWorld {

    @RequestMapping(method = RequestMethod.GET, path="/hello-world")
	public String helloworld()
	{
    	return "<b>Hello World</b";
	}
}

```
6. Run the application and <a href="http://localhost:8080/hello-world" > browse it </a>.
