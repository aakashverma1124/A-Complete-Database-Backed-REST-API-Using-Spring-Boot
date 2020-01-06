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

The pom.xml file looks like:

	<project xmlns="http://maven.apache.org/POM/4.0.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 https://maven.apache.org/xsd/maven-4.0.0.xsd">

	<modelVersion>4.0.0</modelVersion>
	<groupId>in.aboutaakash.springbootquickstart</groupId>
	<artifactId>course-api</artifactId>
	<version>0.0.1-SNAPSHOT</version>
	<name>Java Course API</name>

	<parent>
	<groupId>org.springframework.boot</groupId>
	<artifactId>spring-boot-starter-parent</artifactId>
	<version>2.2.2.RELEASE</version>
	</parent>

	<dependencies>
	<dependency>
	<groupId>org.springframework.boot</groupId>
	<artifactId>spring-boot-starter-web</artifactId>
	</dependency>
	</dependencies>

	<properties>
	<java.version>1.8</java.version>
	</properties>

	</project>

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
package in.aboutaakash.springbootstarter.topic;

import java.util.Arrays;
import java.util.List;

import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.web.bind.annotation.PathVariable;
import org.springframework.web.bind.annotation.RequestBody;
import org.springframework.web.bind.annotation.RequestMapping;
import org.springframework.web.bind.annotation.RequestMethod;
import org.springframework.web.bind.annotation.RestController;

@RestController
public class TopicController {
	
	@Autowired
	private TopicService topicService;
	
	@RequestMapping("/topics")
	public List<Topic> getAllTopics() {
		
		return topicService.getAllTopics();		
	}
	
	@RequestMapping("/topics/{id}")
	public Topic getTopic(@PathVariable String id) {
		return topicService.getTopic(id);
	}
	
	@RequestMapping(method=RequestMethod.POST, value="/topics") 
	public void addTopic(@RequestBody Topic topic) {
		topicService.addTopic(topic);
	}
	
	@RequestMapping(method=RequestMethod.PUT, value="/topics/{id}") 
	public void updateTopic(@RequestBody Topic topic, @PathVariable String id) {
		topicService.updateTopic(id, topic);
	}
	
	@RequestMapping(method=RequestMethod.DELETE, value="/topics/{id}") 
	public void deleteTopic(@PathVariable String id) {
		topicService.deleteTopic(id);
	}
}

</pre>

/ ************* TopicController.java Ends here ************** /

/ ************* TopicService.java ************** /

<pre>
package in.aboutaakash.springbootstarter.topic;

import java.util.ArrayList;
import java.util.Arrays;
import java.util.List;

import org.springframework.stereotype.Service;


@Service
public class TopicService {

	private List<Topic> topics = new ArrayList<>(Arrays.asList(
			new Topic("spring", "Spring Framework", "Spring Framework Description"),
			new Topic("laravel", "Laravel Framework", "Laravel Framework Description"),
			new Topic("django", "Django Framework", "Django Framework Description")
			));
	
	public List<Topic> getAllTopics() {
		return topics;
	}
	
	public Topic getTopic(String id) {
		return topics.stream().filter(t -> t.getId().equals(id)).findFirst().get();		
	}
	
	public void addTopic(Topic topic) {
		topics.add(topic);
	}
	
	public void updateTopic(String id, Topic topic) {
		for (int i = 0; i < topics.size(); i++) {
			Topic t = topics.get(i);
			if(t.getId().equals(id)) {
				topics.set(i, topic);
				return;
			}
		}
	}

	public void deleteTopic(String id) {
		topics.removeIf(t -> t.getId().equals(id));
		
	}
}


</pre>

/ ************* TopicService.java Ends here ************** /

We can now use these functionalities using Postman. Postman is currently one of the most popular tools used in API testing.
We can select what kind of request we want to make and as per our requirement we can test it. You can learn a little bit from some youtube channel, how to use postman.



