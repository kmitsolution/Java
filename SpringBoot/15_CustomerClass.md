# Customer classes

1. Create a project using Spring Initalizr

# Customer class
```java
package com.cognixia.rest.webservice.restfulwebservices.customer;

import java.time.LocalDate;

public class Customer {
private int id;
private String name;
private LocalDate regdate;
@Override
public String toString() {
	return "Customer [id=" + id + ", name=" + name + ", regdate=" + regdate + "]";
}
public int getId() {
	return id;
}
public String getName() {
	return name;
}
public LocalDate getRegdate() {
	return regdate;
}
public Customer(int id, String name, LocalDate regdate) {
	super();
	this.id = id;
	this.name = name;
	this.regdate = regdate;
}
}

```
