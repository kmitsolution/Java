<p>In Real World application there are many dependencies like Business Layer, Web Layer, Data Access Layer etc and to manage them is a challenging task. With Spring Framework instead of focusing on objects, their dependencies and wiring, you can focus on the business logic of your application. Spring Framework manages the lifecycle of objects by marking @Component(and others..) </p>

## Example
Controller > BusinessService > DataService

### DataService Class
```java
package com.kmit.enterprise.dataservice;

import java.util.Arrays;
import java.util.List;

import org.springframework.stereotype.Component;

@Component
public class DataService{
	public List<Integer> getData(){
		return Arrays.asList(10,100,1000);
	}
}
```
### BusinessService Class
```java
package com.kmit.enterprise.business;

import java.util.List;

import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.stereotype.Component;

import com.kmit.enterprise.dataservice.DataService;

@Component
public class BusinessService{
	@Autowired
	private DataService dataService;
	public long calculateSum() {
		List<Integer> data = dataService.getData();
		return data.stream().reduce(Integer::sum).get();
	}
}

```
### MyController Class
```java
@Component
public class MyController {
	@Autowired 
    private BusinessService businessService;
	public long returnFromBusinessService() {
		return businessService.calculateSum();
	}
}
```

### Spring Application Class
```java
package com.kmit;

import org.springframework.boot.SpringApplication;
import org.springframework.boot.autoconfigure.SpringBootApplication;
import org.springframework.context.ConfigurableApplicationContext;

import com.kmit.Cars.CarSelection;
import com.kmit.enterprise.MyController;

@SpringBootApplication
public class Spring01Application {

	public static void main(String[] args) {
	//creates instance for all the components	
	//Spring is managing all the classes and components(Beans) 
	ConfigurableApplicationContext context	=
			 SpringApplication.run(Spring01Application.class, args);
	 
	 CarSelection carSelection= context.getBean(CarSelection.class);
	 MyController controller = context.getBean(MyController.class);
	 System.out.println(controller.returnFromBusinessService());
	}

}

```
