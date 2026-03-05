# SonarQube-Code-Quality-Analysis

Project Overview

This project demonstrates how to perform static code analysis using SonarQube for a Maven-based Java project.

SonarQube is deployed inside a Docker container on an AWS EC2 instance, and a sample Maven project is analyzed using Sonar Scanner. The analysis provides insights into bugs, vulnerabilities, code smells, and overall code quality.

Technologies Used

AWS EC2

Docker

SonarQube

Maven

Git

Linux


Project Architecture:-

Developer Code
      │
      ▼
   Maven Build
      │
      ▼
Sonar Scanner Analysis
      │
      ▼
   SonarQube Server (Docker)
      │
      ▼
  Code Quality Dashboard



Step 1: Configure System Settings

Before running SonarQube, required Linux kernel parameters were configured.

sudo sysctl -w vm.max_map_count=262144
sudo sysctl -w fs.file-max=65536
sudo sysctl -p
These settings are required for Elasticsearch used by SonarQube.

Step 2: Run SonarQube Docker Container

SonarQube was started using Docker with port 9000 exposed.

docker run -d \
--name sonarqube \
-p 9000:9000 \
-e SONAR_ES_BOOTSTRAP_CHECKS_DISABLE=true \
sonarqube:9.9-community

Verify container status:

docker ps


Step 3: Access SonarQube Web Interface

Open the browser and access:

http://<EC2-PUBLIC-IP>:9000

Default credentials:

Username: admin
Password: admin



Step 4: Install Required Tools

Install Git and Maven on the EC2 instance.

sudo yum install git maven -y

Step 5: Clone Sample Maven Project

A sample project repository was cloned for code analysis.

git clone https://github.com/SonarSource/sonar-scanning-examples.git
cd sonar-scanning-examples/sonar-scanner-maven/maven-basic



Step 6: Run SonarQube Code Analysis

Run Sonar Scanner using Maven.

mvn sonar:sonar \
-Dsonar.projectKey=demo \
-Dsonar.host.url=http://localhost:9000 \
-Dsonar.login=<SONAR_TOKEN>

After successful execution, the build output shows:

BUILD SUCCESS



Step 7: View Analysis Results

After scanning, results appear in the SonarQube dashboard.

Example metrics displayed:

Bugs

Vulnerabilities

Code Smells

Security Hotspots

Code Coverage

Duplications

The project status shows Quality Gate Passed.






















