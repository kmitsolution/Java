## @Primary
1. When you have multiple classes decorated with @Component annotation then @Primary is used to determine which class is to autowire.
2. For example if you add @Component on MarutiCar,HyundaiCar,MahindraCar classes (these classes has been created in our previous examples), then Spring will throw the error because it does not know which Component is to call 
3. Add <b>@Primary</b> along with @Component on <b>MarutiCar</b> class then CarSelection will wired up <b>MarutiCar</b> class.

```java
@Component
@Primary
public class MarutiCar implements  CarShowroom {
```
