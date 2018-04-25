---

title: 'Executing automated steps.'
weight: 60

menu:
  main:
    name: "Service Task"
    parent: "get-started-language-agnostic"
    identifier: "get-started-language-agnostic-java-service-task"
    pre: "Executing automated steps in the Process."

---


In this section of this tutorial we learn how to execute automated steps using code using a BPMN 2.0 service task.


# Add a Service Task to the Process

Use the Camunda Modeler to add a service task after the user task. To do so, select the activity shape (rectangle) and drag it onto a sequence flow (see screenshot). Name it *Process Request*. Change the activity type to *Service Task* by clicking on it and using the wrench button.


{{< img src="../img/modeler-service-task1.png" >}}
{{< img src="../img/modeler-service-task2.png" >}}

# Configure the Service Task

Open the Properties Panel within the Camunda Modeler and click on the Service Task you just created. Change the Implementation to `External` and use processRequest as the Topic.

{{< img src="../img/modeler-service-task3.png" >}}

Save the file and deploy it to the process engine again using the Deploy Button in the Modeler.

# Implement an external task worker

Camunda is build in a way that the business logic can be implemented in different languages.
You have the choice which language suits your project best.

## a) Using Java

In this section you will learn how to implement an external task worker in Java.

### Prerequisites

Make sure you have the following set of tools installed:

* JDK 1.8
* Editor for Java projects (e.g. [Eclipse](https://eclipse.org/))

### Create a new Maven project in Eclipse.

In Eclipse, go to File / New / Other .... This opens the New Project Wizard. In the New Project Wizard select Maven / Maven Project. Click Next.

On the first page of the New Maven Project Wizard select Create a simple project (skip archetype selection). Click Next.

On the second page (see screenshot), configure the Maven coordinates for the project. Since we are setting up a JAR Project, make sure to select Packaging: jar.

{{< img src="../img/eclipse-new-project.png" >}}

When you are done, click Finish. Eclipse sets up a new Maven project. The project appears in the Project Explorer View.

### Add Camunda External Task Client Dependency

The next step consists of setting up the Maven dependency to the external task client for your new process application.
Your pom.xml file of your project should look like this:

```xml
<project xmlns="http://maven.apache.org/POM/4.0.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
	xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">
	<modelVersion>4.0.0</modelVersion>
	<groupId>org.camunda.bpm.getstarted</groupId>
	<artifactId>loan-approval</artifactId>
	<version>0.0.1-SNAPSHOT</version>

	<dependencies>
		<dependency>
			<groupId>org.camunda.bpm</groupId>
			<artifactId>camunda-external-task-client</artifactId>
			<version>0.1.0-alpha1</version>
		</dependency>
	</dependencies>
</project>
```

### Add the Java class

Next, you need to create a package, e.g., org.camunda.bpm.getstarted.loanapproval and add a Java class, e.g. ProcessRequest, to it.

```java
  package org.camunda.bpm.getstarted.loanapproval;

  import java.util.logging.Logger;

  public class ProcessRequest {

    public static void main(String[] args) {
      ExternalTaskClient client = ExternalTaskClient.create()
          .baseUrl("http://localhost:8080/engine-rest")
          .build();

      client.subscribe("processRequest")
        .lockDuration(1000)
        .handler((externalTask, externalTaskService) -> {

          // interact with the external task
          String customerId = (String) externalTask.getVariable("customerId");
          LOGGER.info("Processing request by '" + execution.getVariable("customerId") + "'...");

          externalTaskService.complete(externalTask);
      }).open();
    }
  }

### Run the worker

You can run the Java application by right clicking on the class `ProcessRequest` and choose `Run as Java`.

You can verify your results by creating a new process instance using the Tasklist and checking the Console in Eclipse for your running Task Worker.

```

{{< get-tag repo="camunda-get-started-language-agnostic" tag="2-Service-Task-Java" >}}

## b) Using NodeJS

In this section you will learn how to implement an external task worker in NodeJS.

### Prerequisites

Make sure you have the following set of tools installed:

* NodeJS >= v8.9.4
* Editor for JavaScript files (e.g. [Atom](https://atom.io/))

### Create a new NodeJS project

```sh
mkdir process-request-worker
cd ./process-request-worker
npm init process-request-worker -y
```

### Add Camunda External Task Client JS library

```sh
npm install -s camunda-external-task-client-js
```

### Implement the NodeJS script

```javascript

const { Client, logger } = require('camunda-external-task-client-js');

// configuration for the Client:
//  - 'baseUrl': url to the Process Engine
//  - 'logger': utility to automatically log important events
const config = { baseUrl: 'http://localhost:8080/engine-rest', use: logger };

// create a Client instance with custom configuration
const client = new Client(config);

// susbscribe to the topic: 'processRequest'
client.subscribe('processRequest', async function({ task, taskService }) {
  // Put your business logic here
  const customerId = task.variables.get('customerId');

  console.log(`Processing request by ${customerId} ... `);

  // complete the task
  await taskService.complete(task);
});
```

### Run the NodeJS script

```sh
npm run ./worker.js
```

{{< get-tag repo="camunda-get-started-language-agnostic" tag="2-Service-Task-JS" >}}
