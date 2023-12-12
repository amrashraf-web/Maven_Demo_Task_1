Deploying a Java Application with Maven, SonarQube, Docker, Nexus, and Helm on Kubernetes
Infrastructure Setup
SonarQube, Postgres, Nexus Setup
Utilize a Docker Compose file to orchestrate the deployment of SonarQube, Postgres, and Nexus. Make sure Docker Hub Desktop is installed for Docker and Kubernetes. Install Helm for deploying applications on Kubernetes.

Project Initialization
Hello World Java Project
Install Maven:

```bash
sudo apt update && sudo apt install maven
```

Create a Maven Project:

```bash
mvn archetype:generate -DgroupId=com.example -DartifactId=my-java-app -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false
```

Project Build and Integration
Build with Maven and Integrate with SonarQube
Build the Project:

```bash
mvn clean install
```

Integrate with SonarQube:

```bash
mvn sonar:sonar -Dsonar.projectKey=my-java-app -Dsonar.host.url=http://127.0.0.1:9000 -Dsonar.login=token
```


Docker Image Build and Nexus Push

Build Docker Image with Dockerfile:

```bash
docker build -t 127.0.0.1:8082/my-java-app:1.0 .
```
Push Image to Nexus:

```bash
docker login 127.0.0.1:8082 -u username -p password
docker push 127.0.0.1:8082/my-java-app:1.0
```

Helm Chart Creation
Create Helm Charts
Create a mycharts folder and define necessary YAML files:
Chart.yaml: Metadata about the Helm chart.
values.yaml: Default configuration values for the Helm chart.
templates/deployment.yaml: Describes how the application should be deployed.
templates/service.yaml: Describes how the application can be accessed within the Kubernetes cluster.
Deployment with Helm on Kubernetes
Deploy Project using Helm on Kubernetes
Install the Helm chart:

```bash
helm install my-release ./mycharts --values ./mycharts/values.yaml
```

Verify Deployment
Check Project Logs after Deployment
View logs of the deployed pod:

```bash
kubectl logs pod_name
```
Expected Result: "Hello World!"
