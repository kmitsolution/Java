# Spring Boot AutoConfigure
If you are using Spring Framework alone then there are lot of configuration that you need to configure by yourself like ComponentScan, DispatcherServlet,DataSources,JSONConversion etc

You can find the Configuration information in MavenDependency(spring-boot-autoconfigure-3.0.2.jar)

By using Spring Boot you can simplify it by using <b>AutoConfiguration</b> for your app.To explore more on it let's enable logging in application.properties file <b>logging.level.org.springframework=debug </b>

Check the output and you will find the Positive(which are auto configured) and Negative Matches(which are not configured)
