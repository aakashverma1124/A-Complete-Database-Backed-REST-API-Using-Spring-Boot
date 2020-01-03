# A-Complete-Database-Backed-REST-API-Using-Spring-Boot
An end-to-end Spring application using Spring Boot. It's a complete hands-on guide to building a complete database backed REST API using Spring Boot.

Open STS(Spring Tool Suite) or Eclipse.
Create a maven project using this tutorial and name your project course-api.

Make sure to use Java 8+ since Spring Boot doesn't work with earlier versions. Here I am using STS (Spring Tool Suite). It looks like eclipse.

Now, configure pom.xml
The second step is to configure Spring Boot in pom.xml.

All Spring Boot applications extend from spring-boot-starter-parent, so before defining our dependencies, define the parent starter as follows:

<parent>
  <groupId>org.springframework.boot</groupId>
  <artifactId>spring-boot-starter-parent</artifactId>
  <version>2.2.2.RELEASE</version>
</parent>

Since we're creating a REST API, we're going to use spring-boot-starter-web as a dependency which would implicitly define all the required dependencies.

Add the below code in pom.xml as follows:

<dependencies>
  <dependency>
  <groupId>org.springframework.boot</groupId>
  <artifactId>spring-boot-starter-web</artifactId>
  </dependency>
</dependencies>

This will load all the necessary dependencies(all jar files needed for running a Spring Application).



