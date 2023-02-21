Whenever you have complex properties for your application then it is prefered to use Configuration Properties instead of profiles<br />
For Example to setup
```
payroll-service.url
payroll-service.username
payroll-service.key
```

It is better to create a class Configuration class and annotate with @ConfigurationProperties

## PayrollServiceConfiguration class

```java
package com.example.demo;

import org.springframework.boot.context.properties.ConfigurationProperties;
import org.springframework.stereotype.Component;

@ConfigurationProperties(prefix = "payroll-service")
@Component //so that spring is to manage as bean
public class PayrollServiceConfiguration {
    private String url;
    private String username;
    private String key;
	public String getUrl() {
		return url;
	}
	public String getUsername() {
		return username;
	}
	public String getKey() {
		return key;
	}
	public void setUrl(String url) {
		this.url = url;
	}
	public void setUsername(String username) {
		this.username = username;
	}
	public void setKey(String key) {
		this.key = key;
	}
}

```
## application.properties
```
payroll-service.url="testing.com"
payroll-service.username="user1"
payroll-service.key="testkey"
```

## PayrollServiceController class
```java
package com.example.demo;



import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.web.bind.annotation.RequestMapping;
import org.springframework.web.bind.annotation.RestController;

@RestController
public class PayrollServiceController {

	@Autowired
	PayrollServiceConfiguration configuration;
	
	@RequestMapping("/payroll")
	public PayrollServiceConfiguration getPayroll()
	{
		return configuration;
		
	}
}

```
Save and run the application and browse <a href="http://localhost:8080/payroll" /> 
