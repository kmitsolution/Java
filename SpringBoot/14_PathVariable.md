You can pass the Path parameter with url (/emps/{id} etc.).<b> @PathVariable </b>is used to refer a Path variable

## HelloWorldBean Class

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


public HelloWorldBean(String message) {
	  this.message=message;
  }
}

```

## HelloWorld Class

```java
package com.example.rest.webservices.restfulwebservices.helloworld;

import org.springframework.web.bind.annotation.GetMapping;
import org.springframework.web.bind.annotation. >PathVariable;</a>
import org.springframework.web.bind.annotation.RestController;

@RestController
public class HelloWorld {

    @GetMapping( path="/hello-world")
	public String helloworld()
	{
    	return "<b>Hello World</b";
	}
    
    @GetMapping( path="/hello-world-bean/{name}")
	public HelloWorldBean helloworldbean(@PathVariable String name)
	{
    	return new HelloWorldBean("Hello " + name);
	}
}

```
< a href=http://localhost:8080/hello-world-bean/raman >Browse</a>
