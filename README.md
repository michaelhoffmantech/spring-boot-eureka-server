# spring-boot-eureka-server

Eureka Server for Getting Started with Spring Boot presentation. 

# 1 - Spring Intializr Creation

I used the following at http://start.spring.io to create the Eureka Server application. 

* Build tool - Gradle 
* Language - Java
* Spring Boot Version - 2.0.0 RC1 
* Group = com.scmc
* Artifact = boot-demo-eureka-server
* Name = boot-demo-eureka-server
* Package Name = com.scmc.bootdemo.eureka
* Packaging = JAR
* Java Version = 9
* Dependencies = Eureka Server

# 2 - Eureka Server Updates

## 2.1 - Update Application Class

Next in the class BootDemoEurekaServerApplication, I needed to add the following annotation to the class:

@EnableEurekaServer

This enables a registry that other applications can talk to.

## 2.2 - Update Application Properties

Next, I added the following to the application.properties file found in the main resources directory:

server.port=8761

eureka.client.register-with-eureka=false
eureka.client.fetch-registry=false

logging.level.com.netflix.eureka=OFF
logging.level.com.netflix.discovery=OFF

* This changes the server port so that we don't have conflicts with the 8000's range planned for our microservices.
* This also prevents the registry from attempting to register itself. 
* Finally, I've turned off stacktrace as it will complain about not having replica nodes for the registry to connect to. Replication is recommended for production, but we aren't building that type of environment in the example.

## 2.3 - Update build.gradle

Finally, because I'm using Java 9 and JAXB has been removed from the JDK in favor of being a module, I've explicitly included the dependencies as part of compilation:

	compile('javax.xml.bind:jaxb-api:2.3.0')
	compile('com.sun.xml.bind:jaxb-impl:2.3.0')
	compile('com.sun.xml.bind:jaxb-core:2.3.0')
	compile('javax.activation:activation:1.1.1')

# 3 - Running the Application

Simply run the following command to start the Eureka server:

.\gradlew bootRun

This will start the server on port 8761. 

# 4 - More Details

* You can check out the following link for more details on service registration and discovery from Spring: https://spring.io/guides/gs/service-registration-and-discovery
* You can find more about the pattern here: http://microservices.io/patterns/service-registry.html


