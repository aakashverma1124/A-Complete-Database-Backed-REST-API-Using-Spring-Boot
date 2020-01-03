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

Now create a main class CourseApiApp that will be run.
/ ************* CourseApiApp.java ************** /

package in.aboutaakash.springbootstarter;

import org.springframework.boot.SpringApplication;
import org.springframework.boot.autoconfigure.SpringBootApplication;

@SpringBootApplication
public class CourseApiApp {

	public static void main(String[] args) {
		SpringApplication.run(CourseApiApp.class, args);
	}
}

/ ************* CourseApiApp.java Ends Here ************** /

Now create a controller TopicController and create a method getAllTopics that fetches a list of topics from the database. But as of now, we'll fetch data manually and not from the database.

/ ************* TopicController.java ************** /

package in.aboutaakash.springbootstarter.topic;

import java.util.Arrays;
import java.util.List;

import org.springframework.web.bind.annotation.RequestMapping;
import org.springframework.web.bind.annotation.RestController;

@RestController
public class TopicController {
	
	@RequestMapping("/topics")
	public List<Topic> getAllTopics() {
		
		return Arrays.asList(
				new Topic("spring", "Spring Framework", "Spring Framework Description"),
				new Topic("laravel", "Laravel Framework", "Laravel Framework Description"),
				new Topic("django", "Django Framework", "Django Framework Description")
				);
		
	}

}

/ ************* TopicController.java Ends Here ************** /

Create another class in the same package Topic.java that will consists of getters and setters.

/ ************* Topic.java ************** /

package in.aboutaakash.springbootstarter.topic;

public class Topic {
	
	private String id;
	private String name;
	private String description;
	
	public Topic() {
		
	}
	
	public Topic(String id, String name, String description) {
		super();
		this.id = id;
		this.name = name;
		this.description = description;
	}
	
	public String getId() {
		return id;
	}
	public void setId(String id) {
		this.id = id;
	}
	public String getName() {
		return name;
	}
	public void setName(String name) {
		this.name = name;
	}
	public String getDescription() {
		return description;
	}
	public void setDescription(String description) {
		this.description = description;
	}
  
}


/ ************* Topic.java Ends here ************** /


