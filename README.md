# Deploying a Java Application with Maven, SonarQube, Docker, Nexus, and Helm on Kubernetes

# Overview

## This guide demonstrates the end-to-end process of deploying a Java application using Maven, SonarQube, Docker, Nexus, and Helm on a Kubernetes cluster.

# Prerequisites

## - Docker Hub Desktop For ( docker - docker-compose - kubernetes ) commands
## - Helm
## - Maven

# Infrastructure Setup

```bash
# Deploy SonarQube, Postgres, and Nexus
docker-compose up -d
```

# Project Initialization

### Create a Hello World Java Project

```bash
sudo apt update && sudo apt install maven
mvn archetype:generate -DgroupId=com.example -DartifactId=my-java-app -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false
```

# Project Build and Integration

### Step 1 : Build with Maven

```bash
mvn clean install
```

# Step 2 : Integrate with SonarQube

```bash
mvn sonar:sonar -Dsonar.projectKey=my-java-app -Dsonar.host.url=http://127.0.0.1:9000 -Dsonar.login=token
```

# Docker Image Build and Nexus Push

### Step 1 : Build Docker Image

```bash
docker build -t 127.0.0.1:8082/my-java-app:1.0 .
```

### Step 2 : Push to Nexus

```bash
docker login 127.0.0.1:8082 -u username -p password
docker push 127.0.0.1:8082/my-java-app:1.0
```

# Helm Chart Creation

### Step 1 : Create a mycharts folder with necessary YAML files

    1 - Create Folder mycharts and inside it i create my yaml files
    2 - Create Chart.yaml for Describes the chart, including name, version, description, and other metadata.
    3 - Create values.yaml for Centralized location for default values that can be overridden during deployment And Facilitates customization for different environments without modifying templates.
    4 - Create deployment.yaml inside tempaltes Folder for Defines how the application should be deployed, including replicas, containers, and volumes
    5 - Create service.yaml inside tempaltes Folder For Defines how the application can be accessed within the Kubernetes cluster


# Deployment with Helm on Kubernetes

### Step 1 : Deploy Project using Helm

```bash
helm install my-release ./mycharts --values ./mycharts/values.yaml
```

# Verify Deployment

### Step 1 : Check Project Logs after Deployment

```bash
kubectl logs pod_name
```

# Expected Result: "Hello World!"













