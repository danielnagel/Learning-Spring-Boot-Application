# Learning Spring Boot Application

The main goal of this repository is to learn spring boot from scratch by myself.

## What I've learned

Learning the basics of Spring Boot 2.2.0.M5 by writing a small REST application.

> I used [Postman](https://www.getpostman.com/) to examine all of my HTTP Requests.

1. Running a Spring Boot application
    1. How to use the [spring initializr](https://start.spring.io/)
        * Starting right away creating a new application, without setting up the environment
        * Project Setup: Gradle, Java, Spring Boot (2.2.0.M5), Spring Reactive Web,
        Spring Data Reactive MongoDB, Thymeleaf, Lombok
    1. Writing a REST controller:
    [HomeController.java](src/main/java/com/danielnagel/learningspringboot/learningspringboot/HomeController.java)
        * Setting up a controller, which writes its results straight to the response body.
    1. Setting up a Document for MongoDB using Lombok:
    [Chapter.java](src/main/java/com/danielnagel/learningspringboot/learningspringboot/Chapter.java)
        * This MongoDB uses this Document to create a collection named chapters.
    1. Creating a Spring Data repository:
    [ChapterRepository.java](src/main/java/com/danielnagel/learningspringboot/learningspringboot/ChapterRepository.java)
        * Writing an interface, so MongoDB will use it to wire up a concrete implementation
        * This implementation comes with some predefined CRUD operations
    1. Writing a bean that loads the database:
    [LoadDatabase.java](src/main/java/com/danielnagel/learningspringboot/learningspringboot/LoadDatabase.java)
        * Writing new Chapters into the database and printing them out, using the data repository.
        * What a CommandLineRunner is and when Spring runs them.
    1. Writing a controller to server data from the database:
    [ChapterController.java](src/main/java/com/danielnagel/learningspringboot/learningspringboot/ChapterController.java)
        * Serving the data, written to the database by the bean.
        * Mapping other routes then the default "/" route.
1. Spring Boot's property support
    [application.properties](src/main/resources/application.properties)
    1. Changing the port Tomcat listens on
    1. Customizing log levels
    1. Customizing the app name
    1. Adding a description
1. Bundling a runnable JAR file with: `gradlew clean build`
    1. Using gradlew to build a runnable JAR file
    1. Running the JAR file with: `java -jar build/libs/learning-spring-boot-0.0.1-SNAPSHOT.jar`
1. Deploying to [Cloud Foundry](https://www.cloudfoundry.org/) at [Pivotal](https://pivotal.io/)
    1. Deploying CLoud-native applications using cf cli tool. (Only Unix-Like OS).
        * Logging in: `cf login -a api.run.pivotal.io`
        * Push application: `cf push danieel-learns-spring-boot -p build/libs/learning-spring-boot-0.0.1-SNAPSHOT.jar`
            * Yes it was late and I made a typo in my own name.
1. Adding production-ready support, appending [build.gradle](build.gradle)
    1. Using Spring Boot's Actuator module to provide Ops-oriented features
        * Adding `compile('org.springframework.boot:spring-boot-starter-actuator')` to build.gradle
    1. Enabling additional Actuator endpoints in
    [application.properties](src/main/resources/application.properties)
        * Adding `management.endpoint.health.show-details=always` to show health details
        * Enabling `metrics` to track the performance of the application
    1. Updated cloud instance with the cf cli tool.