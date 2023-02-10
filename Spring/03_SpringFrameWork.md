If You want to see that how spring framework is processing the code then add below line in <b>application.properties</b> file <br />
```     
     logging.level.org.springframework=debug
```
When you run the application again then you will find that lot of information displays in the output window like
1. Candidate component class CarSelection
2. Creating shared instance of singleton bean 'carSelection'

## Experiments
1. Remove the @Component from MarutiCar and Run the application
2. Add @Component on more than 1 Classes and Run the application.
