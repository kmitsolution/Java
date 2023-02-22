# Example to return class object 

## Create a class HelloWorldBean

```java
package com.example.rest.webservices.restfulwebservices.helloworld;


public class HelloWorldBean {
  private String message;


  public String getMessage() {
	return message;
}


public void setMessage(String message) {
	this.message = message;
}


public HelloWorldBean() {
	  this.message="Test";
  }
}

```

## HelloWorld class with GetMapping to HelloWorldBean class
```java
package com.example.rest.webservices.restfulwebservices.helloworld;

import org.springframework.web.bind.annotation.GetMapping;
import org.springframework.web.bind.annotation.RequestMapping;
import org.springframework.web.bind.annotation.RequestMethod;
import org.springframework.web.bind.annotation.RestController;

@RestController
public class HelloWorld {

    @GetMapping( path="/hello-world")
	public String helloworld()
	{
    	return "<b>Hello World</b";
	}
    
    @GetMapping( path="/hello-world-bean")
	public HelloWorldBean helloworldbean()
	{
    	return new HelloWorldBean();
	}
}

```
Run the application in <a href="http://localhost:8080/hello-world-bean"> browser</a>

Let's explore few points from above example

1. DispatcherServlet - Front Controller Pattern
   <ul>
      <li> Mapping servlets: dispatcherServlet urls=[/] </li>
      <li> Auto Configuration (DispatchServletAutoConfiguration)
   </ul>
2. HelloWorldBean object is converted into JSON because @RestController returns @ResponseBody + JacksonHttpMessageConverters which converts object into JSON and configuration is available in <b>AutoConfiguration</b>(JacksonHttpMessageConvertersConfiguration).
3. Auto Configuration(ErrorMvcAutoConfiguration) configure Error Mapping.   
  </ul>
