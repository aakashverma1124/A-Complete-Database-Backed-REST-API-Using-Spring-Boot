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
<pre>
package in.aboutaakash.springbootstarter;

import org.springframework.boot.SpringApplication;
import org.springframework.boot.autoconfigure.SpringBootApplication;

@SpringBootApplication
public class CourseApiApp {

	public static void main(String[] args) {
		SpringApplication.run(CourseApiApp.class, args);
	}
}
</pre>

/ ************* CourseApiApp.java Ends Here ************** /

Now create a controller TopicController and create a method getAllTopics that fetches a list of topics from the database. But as of now, we'll fetch data manually and not from the database.

/ ************* TopicController.java ************** /
<pre>
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
</pre>

/ ************* TopicController.java Ends Here ************** /

Create another class in the same package Topic.java that will consists of getters and setters.

/ ************* Topic.java ************** /
<pre>
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
</pre>


/ ************* Topic.java Ends here ************** /

<h3>Now we'll be creating 3 resources</h3>
<ul>
<li>Topic</li>
<li>Course</li>
<li>Lesson</li>
</ul>

A Topic can have multiple Courses and a Course can consist of multiple Lessons.

Now we'll be working on <b>Topics</b>
<h3>Topics</h3>
<table>
  <tr>
    <th>Type Of Request</th>
    <th>URL</th>
    <th>Description</th>
  </tr>
  <tr>
    <td>GET</td>
    <td>/topics</td>
    <td>Get all the topics</td>
  </tr>
  <tr>
    <td>GET</td>
    <td>/topics/id</td>
    <td>Gets the topic</td>
  </tr>
  <tr>
    <td>POST</td>
    <td>/topics</td>
    <td>Creates a new topic</td>
  </tr>
  <tr>
    <td>PUT</td>
    <td>/topics/id</td>
    <td>Updates the topic</td>
  </tr>
  <tr>
    <td>DELETE</td>
    <td>/topics/id</td>
    <td>Deletes the topic</td>
  </tr>
</table>

Now create a Business Service. Business Service is nothing but a class with @Service annotation. These are used to write business logic in a different layer, separated from @RestController class file. 

So, create a class TopicService with @Service annotation in <b>package in.aboutaakash.springbootstarter.topic;</b> package.

Here we'll be using TopicService resource to get all the topics instead of what we were using earlier. We'll make an instance of TopicService in TopicController to get all the topics.
In the similar way, we'll build all the requests that will be coming through /topics and the updated code will be:

/ ************* TopicController.java ************** /

<pre>

</pre>

/ ************* TopicController.java Ends here ************** /

/ ************* TopicService.java ************** /

<pre>

</pre>

/ ************* TopicService.java Ends here ************** /


