## 1. Run Docker Desktop and enable Kubernetes

![image](https://github.com/luiscoco/SpringBoot_Sample4-Deploy-WebAPI-to-LocalKubernetes/assets/32194879/75fad4f1-82dc-4edf-93b0-62d3547a2d23)

## 2. Create a SpringBoot WebAPI with VSCode

See this rep: https://github.com/luiscoco/SpringBoot_Sample1-created-with-VSCode

Press **Ctrl+Shift+P** for creating a new project in VSCode

We select the first option "**Spring Initializer: Create a Maven Project...**" 

![image](https://github.com/luiscoco/SpringBoot_Sample4-Deploy-WebAPI-to-LocalKubernetes/assets/32194879/43535475-48ff-4230-892f-78395b429184)

Set Spring Boot **version 3.2.1** 

![image](https://github.com/luiscoco/SpringBoot_Sample4-Deploy-WebAPI-to-LocalKubernetes/assets/32194879/6704a46b-c10e-445d-a498-a7cfa35a4d51)

Set the language **Java**

![image](https://github.com/luiscoco/SpringBoot_Sample4-Deploy-WebAPI-to-LocalKubernetes/assets/32194879/994b73a4-7378-4b03-8ec6-be699d5393c9)

Input the **Group Id project**

![image](https://github.com/luiscoco/SpringBoot_Sample4-Deploy-WebAPI-to-LocalKubernetes/assets/32194879/3b292fa8-a665-46ed-a570-13e3eff334c1)

Input the **Artifact Id**

![image](https://github.com/luiscoco/SpringBoot_Sample4-Deploy-WebAPI-to-LocalKubernetes/assets/32194879/c04d51ae-0eb0-45c0-a898-8ab4cef88469)

Specify the packing type **Jar**

![image](https://github.com/luiscoco/SpringBoot_Sample4-Deploy-WebAPI-to-LocalKubernetes/assets/32194879/c220c59e-29b8-4dba-b5fe-7660102ff89a)

Se the **Java version 21**

![image](https://github.com/luiscoco/SpringBoot_Sample4-Deploy-WebAPI-to-LocalKubernetes/assets/32194879/69f92e20-d5f6-4912-b388-e7dbc3bb08b6)

## 3. Add the Kubernetes manifest files (deployment.yml and service.yml files) to the SpringBoot WebAPI in VSCode

**deployment.yml**

```
apiVersion: apps/v1
kind: Deployment
metadata:
  name: demoapi-deployment
spec:
  replicas: 2
  selector:
    matchLabels:
      app: demoapi
  template:
    metadata:
      labels:
        app: demoapi
    spec:
      containers:
      - name: demoapi
        image: luiscoco/demoapi:latest
        ports:
        - containerPort: 8080
```

**service.yml**

```
apiVersion: v1
kind: Service
metadata:
  name: demoapi-service
spec:
  type: LoadBalancer
  ports:
  - port: 80
    targetPort: 8080
  selector:
    app: demoapi
```

## 4. Install the project dependencies 

Include the following libraries in the pom.xml file:

- spring-boot-starter-actuator
- spring-boot-starter-web
- spring-boot-starter-test

```
...
<dependency>
   <groupId>org.springframework.boot</groupId>
   <artifactId>spring-boot-starter-actuator</artifactId>
</dependency>
<dependency>
   <groupId>org.springframework.boot</groupId>
   <artifactId>spring-boot-starter-web</artifactId>
</dependency>
<dependency>
   <groupId>org.springframework.boot</groupId>
   <artifactId>spring-boot-starter-test</artifactId>
   <scope>test</scope>
</dependency>
...
```

## 5. Add the SpringBoot WebAPI source code

**DemoapiApplication.java**

```java
package com.example.demoapi;

import org.springframework.boot.SpringApplication;
import org.springframework.boot.autoconfigure.SpringBootApplication;

@SpringBootApplication
public class DemoapiApplication {
    public static void main(String[] args) {
        SpringApplication.run(DemoapiApplication.class, args);
    }
}
```

**HelloController.java**

http://localhost:8080/hello

```java
package com.example.demoapi.controller;

import org.springframework.web.bind.annotation.GetMapping;
import org.springframework.web.bind.annotation.RestController;

@RestController
public class HelloController {
    @GetMapping("/hello")
    public String sayHello() {
        return "Hello, World!";
    }
}
```

## 6. How build the Docker image and run it

To build the Docker image execute this command:

```
docker build -t luiscoco/demoapi:latest .
```

To push the Web API docker image run this command:

```
docker build -t luiscoco/demoapi:latest .
```

To run a Docker image execute the command:

```
docker run -p 8080:8080 luiscoco/demoapi:latest
```

## 7. 







