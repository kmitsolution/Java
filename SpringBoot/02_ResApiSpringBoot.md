# First App in Spring Boot (Rest Api)

Create a Spring Boot Project using <a href="https://start.spring.io/"> Spring Initializr </a>
### Emp Controller Class

```java
package com.example.demo;


import java.util.Arrays;
import java.util.List;

import org.springframework.web.bind.annotation.RequestMapping;
import org.springframework.web.bind.annotation.RestController;

@RestController
public class EmpController {

	@RequestMapping("/emps")
	public List<Emp> getAllEmps()
	{
		return Arrays.asList(
				 new Emp(1,"Raman",90000),
				 new Emp(1,"Manoj",100000)
				);
		
	}
}

```

### Emp Class

```java
package com.example.demo;

public class Emp {
 private int Id;
 private String name;
 private int sal;
 
 
public Emp(int id, String name, int sal) {
	super();
	Id = id;
	this.name = name;
	this.sal = sal;
}


public int getId() {
	return Id;
}


public String getName() {
	return name;
}


public int getSal() {
	return sal;
}


@Override
public String toString() {
	return "Emp [Id=" + Id + ", name=" + name + ", sal=" + sal + "]";
}

}

```

Run the application and visit on <a href="http://localhost:8080/emps"> this link </a>

## Congratulation !! You have created your first Spring Boot project
