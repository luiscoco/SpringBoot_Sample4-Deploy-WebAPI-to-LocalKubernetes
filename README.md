## 1. Create a SpringBoot WebAPI with VSCode

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



## 2. Add the Kubernetes manifest files (deployment.yml and service.yml files) to the SpringBoot WebAPI in VSCode

**deployment.yml**

```
apiVersion: apps/v1
kind: Deployment
metadata:
  name: demoapi-deployment
spec:
  replicas: 2  # The number of Pods to run
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
          image: <your-docker-image>  # Replace with your Docker image, e.g., "username/demoapi:latest"
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
  type: LoadBalancer  # Exposes the service externally using a load balancer
  selector:
    app: demoapi
  ports:
    - protocol: TCP
      port: 80  # The port the load balancer listens on
      targetPort: 8080  # The port the container accepts traffic on
```

## 3. Add the project dependencies






## 4. Add the SpringBoot WebAPI source code







## 5. 






