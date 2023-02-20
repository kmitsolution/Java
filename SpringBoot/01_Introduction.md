## Why Spring Boot
Setting uo Spring Projects before Spring Boot was NOT easy.
1. Dependency Management(pom.xml).
2. Define Web App Configuration(web.xml).
3. Manage Spring Beans(context.xml).
4. Implement Non Functional Requirements(NFRS).

## Create First SpringBoot Project
1. Creating the Spring Boot Application is easy by using <a href="https://start.spring.io/"> spring initializr </a> .
2. Select Project= Maven, Spring Boot 3.0.0(M3) and Provide the Project metadata.
3. For Spring Boot we need to add dependency <b>Spring Web </b> .
4. Once Projetct is created then open on in your favourite IDE.
5. Run the application, it should be successfully executed.

<b>Note:</b> If you get the error that port 8080 is already in use then you can kill the process which is using tomcat server
1. netstat -ao | find "8080"
2. Taskkill /PID  <<pid number>> /F


