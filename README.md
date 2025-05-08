# Hotstar Cloud Deployment

## Overview
This project demonstrates how to deploy a Hotstar application using Docker. The application is containerized using Docker, and the process includes building, pushing the Docker image to Docker Hub, and running the container. The entire process is automated using Jenkins.

The following steps outline how to build and deploy the Hotstar application with Docker and Jenkins.

## Prerequisites

Before you begin, ensure you have the following tools installed:

- **Docker**: To build, push, and run containers.
- **Jenkins**: For continuous integration and continuous deployment (CI/CD).
- **Git**: For version control and retrieving the source code.
- **Node.js and npm**: To install dependencies and run the ReactJS application.
- **Docker Hub account**: To push the Docker image to Docker Hub.
- **Jenkins credentials**: Store the GitHub and Docker Hub credentials for Jenkins.

## Steps

### 1. Clone the Repository

Clone the repository from GitHub to your local machine:

```bash
git clone https://github.com/teja94411/Hotstar-Cloud-Deployment.git
cd Hotstar-Cloud-Deployment
```

### 2. Install Dependencies
Once the repository is cloned, you need to install the necessary dependencies for the ReactJS application.

```bash
npm install
```
This will install the dependencies listed in package.json.

### 3. Build Docker Image
Build the Docker image for the Hotstar application:

```bash
docker build -t hotstar .
```

This will create an image named hotstar using the Dockerfile in the current directory.

### 4. Tag the Docker Image
Once the image is built, tag it with your Docker Hub username and the latest tag:

```bash
docker tag hotstar yourusername/hotstar:latest
```

### 5. Push the Docker Image to Docker Hub
Login to Docker Hub and push the image:

```bash
docker login
docker push yourusername/hotstar:latest
```

Replace yourusername with your actual Docker Hub username.

### 6. Deploy the Docker Container
After the image is pushed to Docker Hub, deploy the container locally or in any cloud environment (e.g., AWS, GCP, Azure). You can run the container with the following command:

```bash
docker run -d --name hotstar -p 3000:3000 yourusername/hotstar:latest
```

This will start the Hotstar application in a Docker container and expose it on port 3000.

### 7. Access the Application

Once the container is running, you can access the Hotstar application by navigating to http://localhost:3000 in your browser.

### 8. Jenkins CI/CD Pipeline

The deployment process is automated using Jenkins. Here’s a breakdown of the stages in the Jenkins pipeline:

- Clean Workspace: Cleans the workspace to ensure a fresh environment.

- Checkout from Git: Pulls the latest changes from the GitHub repository.

- Install Dependencies: Installs the necessary dependencies for the ReactJS application using npm install.

- Login to Docker Hub: Logs into Docker Hub using stored credentials to push the Docker image.

- Docker Build & Push: Builds the Docker image, tags it, and pushes it to Docker Hub.

- Deploy to Container: Runs the Docker container locally on port 3000.

### Conclusion

By following the steps above, you can easily Dockerize your Hotstar application, push it to Docker Hub, and deploy it using Jenkins for automation. You can access the running application via http://localhost:3000 or deploy it on any cloud service or production environment.

## License

This project is licensed under the MIT License.

# Post Hotstar-Cloud-Deployment

![image](https://github.com/user-attachments/assets/115a4451-014c-4873-b613-4178ac602dd0)
![image](https://github.com/user-attachments/assets/903e46c8-aa74-4540-a963-cfef9e1e52ee)
