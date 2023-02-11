## Dependency Injection Types
1. <b>Constructor-based:</b> Dependencies are set by creating the Bean using its Constructuor.
```java
	@Autowired
	public BusinessService() {
		super();
		// TODO Auto-generated constructor stub
		System.out.println("Business Class constructor");
	}
```

2. <b>Setter-based:</b> Dependencies are set by calling setting methods on your beans.
```java
	private DataService dataService;
	@Autowired
	public void setDataService(DataService dataService) {
		System.out.println("Setter injection");
		this.dataService = dataService;
	}
```

3. <b>Field:</b> No setter pr constructor Dependency is injected using reflection. eg 

   ```java
   @Autowired
	private DataService dataService;
   ```
<b>Note:</b> Constructor based injection is recommended to use
