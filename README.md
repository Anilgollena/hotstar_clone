# DevSecOps CI/CD : Deploying a Secure Hotstar Clone

![image](https://github.com/user-attachments/assets/29439485-4925-48b4-9924-5d810557fd8f)

# Prerequisites
AWS account setup
Basic knowledge of AWS services
Understanding of DevSecOps principles
Familiarity with Docker, Jenkins, Java, SonarQube, AWS CLI, Kubectl, and Terraform,Docker Scout
# Step-by-Step Deployment Process
Step 1: Setting up AWS EC2 Instance
Creating an EC2 instance with Ubuntu AMI, t2.large, and 30 GB storage
Assigning an IAM role with Admin
ccess for learning purposes
![Screenshot (1143)](https://github.com/user-attachments/assets/90c89246-96fe-42ee-a208-5de299d0c329)


Step 2: Installation of Required Tools on the Instance
# Writing a script to automate the installation of:
Docker
Jenkins
Java
SonarQube container
AWS CLI
Kubectl
Terraform
Step 3: Jenkins Job Configuration
#!/bin/bash
sudo apt update -y
wget -O - https://packages.adoptium.net/artifactory/api/gpg/key/public | tee /etc/apt/keyrings/adoptium.asc
echo "deb [signed-by=/etc/apt/keyrings/adoptium.asc] https://packages.adoptium.net/artifactory/deb $(awk -F= '/^VERSION_CODENAME/{print$2}' /etc/os-release) main" | tee /etc/apt/sources.list.d/adoptium.list
sudo apt update -y
sudo apt install temurin-17-jdk -y
/usr/bin/java --version
curl -fsSL https://pkg.jenkins.io/debian-stable/jenkins.io-2023.key | sudo tee /usr/share/keyrings/jenkins-keyring.asc > /dev/null
echo deb [signed-by=/usr/share/keyrings/jenkins-keyring.asc] https://pkg.jenkins.io/debian-stable binary/ | sudo tee /etc/apt/sources.list.d/jenkins.list > /dev/null
sudo apt-get update -y
sudo apt-get install jenkins -y
sudo systemctl start jenkins
#install docker
# Add Docker's official GPG key:
sudo apt-get update
sudo apt-get install ca-certificates curl gnupg -y
sudo install -m 0755 -d /etc/apt/keyrings
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /etc/apt/keyrings/docker.gpg
sudo chmod a+r /etc/apt/keyrings/docker.gpg
# Add the repository to Apt sources:
echo \
  "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.gpg] https://download.docker.com/linux/ubuntu \
  $(. /etc/os-release && echo "$VERSION_CODENAME") stable" | \
  sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
sudo apt-get update
sudo apt-get install docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin -y
sudo usermod -aG docker ubuntu
newgrp docker

#!/bin/bash
#install terraform
sudo apt install wget -y
wget -O- https://apt.releases.hashicorp.com/gpg | sudo gpg --dearmor -o /usr/share/keyrings/hashicorp-archive-keyring.gpg
echo "deb [signed-by=/usr/share/keyrings/hashicorp-archive-keyring.gpg] https://apt.releases.hashicorp.com $(lsb_release -cs) main" | sudo tee /etc/apt/sources.list.d/hashicorp.list
sudo apt update && sudo apt install terraform
#install Kubectl on Jenkins
sudo apt update
sudo apt install curl -y
curl -LO https://dl.k8s.io/release/$(curl -L -s https://dl.k8s.io/release/stable.txt)/bin/linux/amd64/kubectl
sudo install -o root -g root -m 0755 kubectl /usr/local/bin/kubectl
kubectl version --client
#install Aws cli
curl "https://awscli.amazonaws.cli
om/awscli-exe-linux-x86_64.zip" -o "awscliv2.zip"
sudo apt-get install unzip -y
unzip awscliv2.zip
sudo ./aws/install
sudo chmod 777 /var/run/docker.sock
docker run -d --name sonar -p 9000:9000 sonarqube:lts-community

![Screenshot (1141)](https://github.com/user-attachments/assets/4fd73e54-43ff-4151-9983-04f531569173)

# Creating Jenkins jobs for:
Creating an EKS cluster
Deploying the Hotstar clone application
Configuring the Jenkins job stages:
Sending files to SonarQube for static code analysis
![Screenshot (1142)](https://github.com/user-attachments/assets/0166081b-4c2c-4954-b416-25932b23e53a)

Running npm install
# Implementing OWASP for security checks
Installing and running Docker Scout for container security

![Screenshot (1138)](https://github.com/user-attachments/assets/d5000f83-eb8c-4e85-97eb-f24dd66e4fd5)

![Screenshot (1139)](https://github.com/user-attachments/assets/276e03d6-ab92-4dda-a784-04b06d1d02b1)

Scanning files and Docker images with Docker Scout
Building and pushing Docker images
![Screenshot (1144)](https://github.com/user-attachments/assets/9b29a144-0565-468f-b5a7-0c2b68bdf06a)

Deploying the application to the EKS cluster

 ![Screenshot (1137)](https://github.com/user-attachments/assets/23b46a90-913c-4a52-8cd0-c444a1e9789c)


