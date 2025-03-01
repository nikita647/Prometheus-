# Jenkins | Monitoring metrics



## Table of Content
- [Introduction](#introduction)
- [What is Monitoring?](#what-is-jenkins-monitoring)
- [What is Jenkins Monitoring ?](#what-is-jenkins-monitoring)
- [Types of Jenkins Metrics ](#types-of-jenkins-metrics)
- [How to monitor jenkins metrics ?](#how-to-monitor-jenkins-metrics)
- [Final output](#final-output)
- [Conclusion](Conclusion)
- [Contact](#contact)
- [References](#references)


## Introduction

Jenkins monitoring means keeping an eye on how well Jenkins is working. It’s important to make sure Jenkins runs smoothly and doesn’t slow down or crash . by monitoring key metrics, you can check if Jenkins is healthy, fix issues early, and keep your development process running without problems.


## What is Monitoring?

Monitoring is the process of continuously tracking and observing the performance of the system and application in real time  .



## What is Jenkins Monitoring ?

Monitoring Jenkins ensures it runs smoothly, catches problems early, and prevents downtime. It helps optimize performance by tracking resource usage such as health,disk usage,cpu,etc.

## **Why is Monitoring Important?**
**Prevents Downtime:** Catching issues early avoids system crashes.

**Improves Performance:** Ensures Jenkins runs efficiently.

**Saves Time:** Fixing small problems before they become big ones.

**Keeps Developers Happy:** A smooth-running Jenkins means fewer delays in their work.

## Types of Jenkins Metrics 

|       Types      |          Description               |
|:-----------------:|:-------------------------------------:|
| **System Performance Metrics** | Track CPU, memory, and disk usage to ensure Jenkins has enough resources to run smoothly.
| **Build Metrics** | Monitor build duration, success rates, failure counts .
| **Agent Metrics** | Check the health, availability, and resource usage of Jenkins agents 
| **Plugin Metrics** | Monitor the status and updates of plugins to prevent compatibility issues.


# Tools for Monitoring Jenkins

| Tool                     | Description |
|--------------------------|-------------|
| **Prometheus & Grafana** | Prometheus collects Jenkins metrics, and Grafana helps visualize them. |
| **Jenkins Monitoring Plugin** | Provides real-time system metrics for Jenkins. |
| **Elastic Stack (ELK)** | Collects and analyzes Jenkins logs for in-depth insights. |
| **CloudWatch (AWS)** | Monitors Jenkins instances running on AWS, helping track resource usage. |
___
## How to monitor jenkins usign Prometheus ,NodeExpoter and Grafana ? 

### **step1. Install Prometheus**
 - To install Prometheus on your system, please follow the link below for the Prometheus Setup Guide. :-[ Prometheus Setup  Guide](https://github.com/snaatak-Zero-Downtime-Crew/Documentation/blob/Rohit-SCRUM-16/Common/Software/ScyllaDB/Installation/README.md)

### **step2. Setup NodeExpoter**
 - To Setup NodeExpoter on your system, please follow the link below for the NodeExpoter Setup Guide. :-[ NodeExpoter Setup  Guide](https://github.com/snaatak-Zero-Downtime-Crew/Documentation/blob/Rohit-SCRUM-16/Common/Software/ScyllaDB/Installation/README.md)

### **step3. Setup Grafana**
 - To Setup Grafana on your system, please follow the link below for the Grafana Setup Guide. :-[ Grafana Setup  Guide](https://github.com/snaatak-Zero-Downtime-Crew/Documentation/blob/Rohit-SCRUM-16/Common/Software/ScyllaDB/Installation/README.md)
### **step4. Install Jenkins**

Installation of Java:
``` bash
sudo apt update
sudo apt install fontconfig openjdk-17-jre
java -version
```

Install Jenkins:
``` bash
sudo wget -O /usr/share/keyrings/jenkins-keyring.asc \
  https://pkg.jenkins.io/debian/jenkins.io-2023.key
 ```
``` bash
echo "deb [signed-by=/usr/share/keyrings/jenkins-keyring.asc]" \
  https://pkg.jenkins.io/debian binary/ | sudo tee \
  /etc/apt/sources.list.d/jenkins.list > /dev/null
```
```
sudo apt-get update
sudo apt-get install jenkins
```

## **Step5:Jenkins Monitoring with Prometheus and Grafana**

Go to Manage Jenkins → Plugins → Available Plugins Search for Prometheus and install it

Once that is done you will Prometheus is set to /Prometheus path in system configurations

![Screenshot 2025-03-01 005840](https://github.com/user-attachments/assets/c9ad63e0-a2c4-4e21-b8b1-215c94f93679)


To create a static target, you need to add job_name with static_configs

sudo vim /etc/prometheus/prometheus.yml
Paste below code

- job_name: 'jenkins'
   metrics_path: '/prometheus'
   static_configs:
     - targets: ['<jenkins-ip>:8080']
![image](https://github.com/user-attachments/assets/cc843c39-bb9f-4c08-af9a-18232e19899c)

restart prometheus

sudo systemctl restart prometheus
Check the targets section

http://<ip>:9090/targets




Let’s add Dashboard for a better view in Grafana

Click On Dashboard → + symbol → Import Dashboard

Use Id 9964 and click on load
![image](https://github.com/user-attachments/assets/e2c9fbaf-966a-427c-a63c-a2b9e1a2f183)
### Step6. Output**


## Final output
![Screenshot 2025-03-01 010628](https://github.com/user-attachments/assets/aafc7951-79a3-47b6-bcc4-ba4b8dd1600b)

![Screenshot 2025-03-01 012601](https://github.com/user-attachments/assets/cbe64528-7d6c-4148-b70a-0da6d71b1b55)




## Conclusion

Monitoring Jenkins is essential for maintaining a stable and efficient CI/CD environment. By tracking key metrics like system performance, job health, and security, you can quickly detect and resolve issues .



## References

- Jenkins Metrics : [Jenkins Metrics](https://plugins.jenkins.io/metrics/)
- Monitoring : [Monitoring](https://www.geeksforgeeks.org/what-is-a-monitor/)
