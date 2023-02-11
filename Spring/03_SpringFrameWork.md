If You want to see that how spring framework is processing the code then add below line in <b>application.properties</b> file <br />
```     
     logging.level.org.springframework=debug
```
When you run the application again then you will find that lot of information displays in the output window like
1. Candidate component class CarSelection
2. Creating shared instance of singleton bean 'carSelection'

## Important Terminology
<b> @Component:</b> Class managed by Spring framework <br />
<b> Dependency:</b> CarSelection needs ClassShowroom implementation <br />
<b> Component Scan: </b> How does Spring Framework find component classes? If you mouse hover @SpringBootApplication, you will find @ComponentScan, which is by default pointing (or scanning) the current package, if you want to change the package then you need to pass package name as parameter.You can scan as many packages you want to scan(@ComponentScan({"com.package1","com.package2"}) <br />
<b> Dependency Injection: </b> Identify beans, their dependencies and wire them together(provides IOC- Inversion of Control) <br />
    <ul>
     <li><b>Spring Beans:</b> An object managed by Spring Framework.</li>
     <li><b>IoC container</b> Manages the lifecycle of beans and dependencies with following Types <br />
          1. ApplicationContext (complex) <br />
          2. BeanFactory (simple features but very rarely used). </li>
     <li><b>Autowiring:</b> Process of wiring in dependencies of Spring Bean </li>
    </ul>
          
          


## Experiments
1. Remove the @Component from MarutiCar and Run the application
2. Add @Component on more than 1 Classes and Run the application.
