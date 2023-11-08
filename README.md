# Getting Started with MyApp

This guide will walk you through the steps to build and deploy MyApp using Maven, Docker, and Kubernetes.

## Prerequisites

Before you begin, make sure to have the following tools and utilities installed on your system:

- [Maven](https://maven.apache.org/)
- [Docker](https://www.docker.com/)
- [kubectl](https://kubernetes.io/docs/tasks/tools/)
- [minikube](https://minikube.sigs.k8s.io/)

## Building the Application

1. Clone the project from the repository:
    
    ```bash
    git clone https://github.com/dorbanianas/devops-presentation
    ```
    
2. Navigate to the project directory:
    
    ```bash
    cd devops-presentation
    ```
    
3. Clean the project to remove any previous build artifacts:
    
    ```bash
    mvn clean
    ```
    
4. Build the application package:
    
    ```bash
    mvn package
    ```
    

## **Building and Pushing Docker Image**

1. Log in to your Docker Hub account or your preferred container registry:
    
    ```bash
    docker login
    ```
    
2. Build a Docker image for MyApp, giving it a name and version tag (e.g., `devopspresentation/myapp:latest`):
    
    ```bash
    docker build -t devopspresentation/myapp:latest .
    ```
    
3. Push the Docker image to Docker Hub:
    
    ```bash
    docker push devopspresentation/myapp:latest
    ```
    
4. Verify that the Docker image has been successfully built:
    
    ```bash
    docker images
    ```
    

## **Deploying to Kubernetes**

1. Apply the Kubernetes deployment configuration to deploy MyApp using minikube:
    
    ```bash
    minikube start
    ```
    
2. Apply the Kubernetes deployment configuration to deploy MyApp:
    
    ```bash
    kubectl apply -f deployment.yaml
    ```
    
3. Check the nodes in your Kubernetes cluster:
    
    ```bash
    kubectl get nodes -o wide
    ```
    
4. View the deployments in your cluster:
    
    ```bash
    kubectl get deployments
    ```
    
5. Check the pods created by the deployment:
    
    ```bash
    kubectl get pods
    ```
    
6. Access the logs of all the pods if needed using the following script:
    
    ```bash
    ./get_pods_logs.sh
    ```
    
7. Apply the Kubernetes service configuration to expose the application:
    
    ```bash
    kubectl apply -f service.yaml
    ```
    
8. Check the services available in your cluster:
    
    ```bash
    kubectl get service
    ```
    
9. Verify the nodes and their details:
    
    ```bash
    kubectl get nodes -o wide
    ```
    
10. Access your application by obtaining the external IP of the service using the following script:
    
    ```bash
    ./get_app_url.sh
    ```

#  **CI/CD Pipeline**
## Jenkins Installation using Docker

To install Jenkins using Docker, execute the following commands on your terminal:

1. Pull the Jenkins image from Docker Hub:

   ```bash
   docker pull jenkins/jenkins
   ```
This command fetches the latest Jenkins image from Docker Hub, which is the repository for Docker images.

2. Run the Jenkins container in the background with port mapping, a custom container name, and volume mounting:
    ```bash
    docker run -d -p 9090:8080 --name Jenkins --restart=on-failure -v jenkins_home:/var/jenins_home jenkins/jenkins
    ```
    <span style="color:red">-d</span>starts the container in the background (detached mode).

    <span style="color:red">-p 9090:8080</span>maps port 8080 inside the container to port 9090 on the host.
    
    <span style="color:red">--name Jenkins </span>assigns the name <'Jenkins'> to the container.

    <span style="color:red">--restart=on-failure</span>ensures that the container automatically restarts if it fails.

    <span style="color:red">-v jenkins_home:/var/jenins_home</span> mounts the volume 'jenkins_home' to the '/var/jenins_home' directory in the container.

3. If you want to access your Docker container through a terminal/command prompt using this command :

    ```bash
    docker exec --name Jenkins 
    ```

That will access the Jenkins Docker container named "Jenkins".

4. You can access your docker container (through a separate terminal/command prompt window) with a docker exec command such as:
    
    ```bash
    docker exec -it Jenkins bash
    ```

5. You may want to access the Jenkins console log, for instance, when Unlocking Jenkins as part of the Post-installation setup wizard. Access the Jenkins console log through the terminal/command prompt window from which you executed the <docker run>​ command.Alternatively, you can also access the Jenkins console log through the Docker logs of your container using the following command:

    ```bash
    docker logs docker-container-name
    ```
6. Your docker-container-name can be obtained using this command :

    ```bash
    docker ps
    ```

## SonarQube Installation using Docker

To install SonarQube, follow these steps:

1. Pull the SonarQube image from Docker Hub by running the following command:

   ```bash
   docker pull sonarqube
   ```
2. Once the image is pulled, run a SonarQube container with the following command:

   ```bash
   docker run -d --name sonarqube -p 9000:9000 sonarqube
   ```
This command will start a SonarQube container in detached mode (-d) with the name "sonarqube" and port mapping from the host to the container.

3. Check whether the SonarQube container is running by executing:

   ```bash
   docker ps
   ```
This command will display a list of all running Docker containers.

4. Access SonarQube from your web browser using the URL: http://localhost:9000. SonarQube should now be up and running.

5. If necessary, log in to SonarQube with the default credentials:

    Username: admin

    Password: admin
