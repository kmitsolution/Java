# Managing Application configuration using Profile

With the help of Profile you can configure environment specific application. For example connect with Prod/dev/stag database.

## How To Create the profile
1. Take a copy of application.properties file and make application-dev.properties and application-stag.properties
2. By default the default profile(application.properties) get executed.
3. In application-dev.properties add <b>logging.level.org.springframework=trace</b>
4. In application-prod.properties add <b>logging.level.org.springframework=info</b>
5. 3. In application.properties add <br /> <b>logging.level.org.springframework=trace</b> <br /> <b>spring.profiles.active=prod</b>

### Below are the logging level which is supported by Spring Boot
1. trace
2. info
3. debug
4. error
5. warning
6. off
