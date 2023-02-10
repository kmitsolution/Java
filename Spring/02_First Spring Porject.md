## Let's Create first Spring Project.
1. Open <a href="https://start.spring.io/">Spring Initializer </a>
2. Provide the details like spring version(3.x) and packagename, artifact etc.
3. Download the code and open in IDE (Eclipse)
4. Add all the Car Classes in this project
5. Add @Component to MarutiCar Class
```java
@Component
public class MarutiCar implements  CarShowroom {
```

6. Change the code for the CarSelection Class
```java
package com.kmit.Cars;

import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.stereotype.Component;

@Component
public class CarSelection {
	@Autowired
	CarShowroom cs;
	public CarSelection(CarShowroom cs1) {
		// TODO Auto-generated constructor stub
		this.cs=cs1;
		  cs.carname();
		  cs.seats();
		  cs.color();
		  cs.speed();
		  
	}
}
```
7. Add below code to Application File

```java
package com.kmit;

import org.springframework.boot.SpringApplication;
import org.springframework.boot.autoconfigure.SpringBootApplication;
import org.springframework.context.ConfigurableApplicationContext;

import com.kmit.Cars.CarSelection;

@SpringBootApplication
public class Spring01Application {

	public static void main(String[] args) {
	//creates instance for all the components	
	//Spring is managing all the classes and components(Beans) 
	ConfigurableApplicationContext context	=
			 SpringApplication.run(Spring01Application.class, args);
	 
	 CarSelection carSelection= context.getBean(CarSelection.class);
	}

}

8. Run the application and you will get the output of CarSelection Constructor which is pointing to MarutiCar (because we added the @Component to MarutiCar)
```
