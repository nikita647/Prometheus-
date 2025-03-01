# Jenkins | Monitoring metrics

| **Author** | **Created on** | **Version** | **Last updated by**|**Last Edited On**|**Level** |**Reviewer** |
|------------|---------------------------|-------------|----------------|-----|-------------|-------------|
| Nikita Joshi|  2-03-2025           | v1         | Nikita Joshi    |2-03-2025    |  internal review | komal jaiswal | 


## Table of Content
- [Introduction](#introduction)
- [Pre-requisites](#pre-requisites)
- [What is Monitoring?](#what-is-monitoring)
- [What is Jenkins Monitoring ?](#what-is-jenkins-monitoring)
- [Why is Monitoring Important?](#why-is-monitoring-important)
- [Types of Jenkins Metrics ](#types-of-jenkins-metrics)
- [Tools for Monitoring Jenkins](#tools-for-monitoring-jenkins)
- [Step by Step Guide](#step-by-step-guide)
    - [step1. Setup Prometheus](#step1-setup-prometheus)
    - [step2. Setup NodeExpoter](#step2-setup-nodeexpoter)
    - [step3. Setup Grafana](#step3-setup-grafana)
    - [step4. Install Jenkins](#step4-install-jenkins)
      - [1. Installation of Java](#1-installation-of-java)
      - [2. Install Jenkins](#2-install-jenkins)
   - [Step5. Jenkins Monitoring with Prometheus and Grafana]()
   - [Step6. final Output](#step6-final-output)
- [Conclusion](Conclusion)
- [Contact Information](#contact-information)
- [References](#references)


## **Introduction**

Jenkins monitoring means keeping an eye on how well Jenkins is working. It’s important to make sure Jenkins runs smoothly and doesn’t slow down or crash . by monitoring key metrics, you can check if Jenkins is healthy, fix issues early, and keep your development process running without problems.

## **Pre-requisites**


| **Specification**      | **Details**         |
|-------------------------|---------------------|
| **Operating System**    | Ubuntu 22.04      |
| **CPU**                | 2 vCPU             |
| **Hard Disk**             | 20 GB              |
| **RAM**                | 4 GB               |

--- 

# Security ports

| **Port** | **Protocol** | **Source Side**    | **Destination Side** | **Use Case**                     |
|----------|--------------|--------------------|-----------------------|-----------------------------------|
| 80       | TCP          | Any                | Server               | HTTP traffic for web applications|
| 443      | TCP          | Any                | Server               | Secure HTTPS web traffic         |
| 3000     | TCP          | Any | server      | Grafana      |
| 9100     | TCP          | Any                | Server               |  NodeExpoter |
|9090 | TCP| Any|Server|Prometheus |
|8080|TCP|Any|server|jenkins|

___
## **What is Monitoring?**

Monitoring is the process of continuously tracking and observing the performance of the system and application in real time  .


___
## **What is Jenkins Monitoring?**

Monitoring Jenkins ensures it runs smoothly, catches problems early, and prevents downtime. It helps optimize performance by tracking resource usage such as health,disk usage,cpu,etc.

___
## **Why is Monitoring Important?**
**Prevents Downtime:** Catching issues early avoids system crashes.

**Improves Performance:** Ensures Jenkins runs efficiently.

**Saves Time:** Fixing small problems before they become big ones.

**Keeps Developers Happy:** A smooth-running Jenkins means fewer delays in their work.
___
## **Types of Jenkins Metrics**

|       Types      |          Description               |
|:-----------------:|:-------------------------------------:|
| **System Performance Metrics** | Track CPU, memory, and disk usage to ensure Jenkins has enough resources to run smoothly.
| **Build Metrics** | Monitor build duration, success rates, failure counts .
| **Agent Metrics** | Check the health, availability, and resource usage of Jenkins agents 
| **Plugin Metrics** | Monitor the status and updates of plugins to prevent compatibility issues.


##  **Tools for Monitoring Jenkins**

| Tool                     | Description |
|--------------------------|-------------|
| **Prometheus & Grafana** | Prometheus collects Jenkins metrics, and Grafana helps visualize them. |
| **Jenkins Monitoring Plugin** | Provides real-time system metrics for Jenkins. |
| **Elastic Stack (ELK)** | Collects and analyzes Jenkins logs for in-depth insights. |
| **CloudWatch (AWS)** | Monitors Jenkins instances running on AWS, helping track resource usage. |
___
## **Step by Step Guide**

### **step1. Setup Prometheus**
 - To install Prometheus on your system, please follow the link below for the Prometheus Setup Guide. :-[ Prometheus Setup  Guide](https://github.com/nikita647/Prometheus-/blob/main/preometheus/README.md)

### **step2. Setup NodeExpoter**
 - To Setup NodeExpoter on your system, please follow the link below for the NodeExpoter Setup Guide. :-[ NodeExpoter Setup  Guide](https://github.com/nikita647/Prometheus-/blob/main/NodeExpoter/README.md)

### **step3. Setup Grafana**
 - To Setup Grafana on your system, please follow the link below for the Grafana Setup Guide. :-[ Grafana Setup  Guide](https://github.com/nikita647/Prometheus-/edit/main/Grafana/README.md)
### **step4. Install Jenkins**

#### **1. Installation of Java**
``` bash
sudo apt update
sudo apt install fontconfig openjdk-17-jre
java -version
```

#### **2. Install Jenkins**
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

### **Step5. Jenkins Monitoring with Prometheus and Grafana**

####  **1. Go to Manage Jenkins → Plugins → Available Plugins Search for Prometheus and install it**

Once that is done you will Prometheus is set to /Prometheus path in system configurations

![Screenshot 2025-03-01 005840](https://github.com/user-attachments/assets/c9ad63e0-a2c4-4e21-b8b1-215c94f93679)


#### **2. To create a static target, you need to add job_name with static_configs**
``` bash
sudo vim /etc/prometheus/prometheus.yml
```
**Paste below code**

- job_name: 'jenkins'
   metrics_path: '/prometheus'
   static_configs:
     - targets: ['<jenkins-ip>:8080']
![image](https://github.com/user-attachments/assets/cc843c39-bb9f-4c08-af9a-18232e19899c)

#### **3. restart prometheus**
``` bash
sudo systemctl restart prometheus
```

#### **4. Check the targets section**
``` bash
http://<ip>:9090/targets
```


Let’s add Dashboard for a better view in Grafana

Click On Dashboard → + symbol → Import Dashboard

Use Id 9964 and click on load
![image](https://github.com/user-attachments/assets/e2c9fbaf-966a-427c-a63c-a2b9e1a2f183)
### **Step6. final Output**


![Screenshot 2025-03-01 010628](https://github.com/user-attachments/assets/aafc7951-79a3-47b6-bcc4-ba4b8dd1600b)

![Screenshot 2025-03-01 012601](https://github.com/user-attachments/assets/cbe64528-7d6c-4148-b70a-0da6d71b1b55)



## **Conclusion**

Monitoring Jenkins is essential for maintaining a stable and efficient CI/CD environment. By tracking key metrics like system performance, job health, and security, you can quickly detect and resolve issues .

## **Contact Information**

| **Name** | **Email address**            | **Github ID**
|----------|-------------------------------|-------------------|
| Nikita joshi    | Nikita.Joshi@mygurukulam.co    | https://github.com/jnikita19  |


## **References**

| Reference  | Description |
| ---------  | ----------- |
|[Monitoring with Prometheus](https://medium.com/@PriyamChauhan/introduction-to-monitoring-with-prometheus-fe2cfefb0952) |Prometheus's |
|[Monitoring](https://www.geeksforgeeks.org/what-is-a-monitor/)|Monitoring |

