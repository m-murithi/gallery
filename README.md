### Jenkins Implementation

**Overview**
This repository serves as a guide for implementing and using Jenkins, an open-source automation server. Jenkins is widely used for automating repetitive tasks involved in the continuous integration and continuous delivery (CI/CD) of software projects.

_Features_
- Provides step-by-step instructions for setting up Jenkins on various platforms.
- Demonstrates how to create and configure Jenkins jobs for different purposes.
- Includes best practices and tips for optimizing Jenkins performance and scalability.
- Offers troubleshooting guidelines for common Jenkins issues.

#### Installation
#### Installation with Docker
- Docker is a platform for running applications in an isolated environment called a "container." 

**Install Docker**
- Before you install Docker for the first time on a new machine, you need to set up the Docker repository. Afterward, you can install and update Docker from the repository.

1. Update the apt package index and install the following packages:
```bash
sudo apt-get update

sudo apt-get install \  
    apt-transport-https \  
    ca-certificates \  
    curl \  
    gnupg-agent \  
    software-properties-common
```

2. Add Docker's official GPG key:
```bash
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -
```

3. Use the following command to set up the stable repository
```bash
sudo add-apt-repository \  
   "deb [arch=amd64] https://download.docker.com/linux/ubuntu \  
   $(lsb_release -cs) \  
   stable"
```

4. Update the apt package index again and install the latest version of Docker Engine and container:
```bash
sudo apt-get update  
sudo apt-get install docker-ce docker-ce-cli containerd.io
```

5. Verify that Docker Engine is installed correctly by running the hello-world image.
```bash
sudo docker run hello-world
```
- This command downloads a test image and runs it in a container. When the container runs, it prints an informational message and exits.

**Install Jenkins with Docker**
6. After installing Docker, download the latest stable Jenkins image by running:
```bash
sudo docker image pull jenkins/jenkins:lts
```
- Once we have downloaded the image, we can start the container:
```bash
sudo docker container run -d \  
    -p 8080:8080 \  
    -v jenkinsvol:/var/jenkins_home \  
    --name jenkins-local \  
    jenkins/jenkins:lts
```

- Here is what each argument means:
	-d: detached mode.  Runs the Docker container in the background
	-p: assign port target
	-v: creates a new volume. Volumes are used to persist data for the container. 
	—name: name of the container
	jenkins/jenkins:lts - the image Docker will use to create the container.

