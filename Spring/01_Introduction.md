# Tightly Coupled Classes
Create classes for different types of cars and their features.
```java

package com.learning.springframework;
//Creating interface CarShowroom which will be implemented by all the cars
public interface CarShowroom {
	 void speed();
     void seats();
     void color();
     void carname();
}

```
### MarutiCar Class

```java
package com.learning.springframework;
//Maruti is a type of car which implements CarShowroom interface
public class MarutiCar implements  CarShowroom {

	public void speed() {
		System.out.println("100kms/hr");
	}
    public void seats() {
    	System.out.println("5");
    }
    public void color() {
    	System.out.println("White");
    }
    public void carname() {
    	System.out.println("Maruti");
    }
}

```

### HyundaiCar Class

```java
package com.learning.springframework;
//HyundaiCar is a type of car which implements CarShowroom interface
public class HyundaiCar implements CarShowroom {
	public void speed() {
		System.out.println("120kms/hr");
	}
    public void seats() {
    	System.out.println("5");
    }
    public void color() {
    	System.out.println("Red");
    }
    public void carname() {
    	System.out.println("Hyundai");
    }
}

```

### MahindraCar Class
```java
package com.learning.springframework;
//MahindraCar is a type of car which implements CarShowroom interface
public class MahindraCar implements CarShowroom{

	public void speed() {
		System.out.println("150kms/hr");
	}
    public void seats() {
    	System.out.println("6");
    }
    public void color() {
    	System.out.println("Grey");
    }
    public void carname() {
    	System.out.println("Mahindra");
    }
}

```
### CarSelection Class
```java
package com.learning.springframework;
//CarSelection is the car which is selected by a buyer
public class CarSelection {
	
  public CarSelection(CarShowroom cs) {
	// TODO Auto-generated constructor stub
	  cs.carname();
	  cs.seats();
	  cs.color();
	  cs.speed();
	  
}
}
```
### Run Class
```java
package com.learning.springframework;

//Run class is the execution of the main method
public class Run {

	public static void main(String[] args) {
		// TODO Auto-generated method stub
     CarShowroom car = new HyundaiCar();
     CarSelection selectedCar = new CarSelection(car); 
	}

}

```
