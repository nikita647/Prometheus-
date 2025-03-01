# **NodeExpoter**

| **Author** | **Created on** | **Version** | **Last updated by**|**Last Edited On**|**Level** |**Reviewer** |
|------------|---------------------------|-------------|----------------|-----|-------------|-------------|
| Nikita Joshi|  26-02-2025           | v1         | Nikita Joshi    |26-02-2025    |  internal review | komal jaiswal | 

# Table of Contents

- [Introduction](#introduction)
- [Prerequisites](#prerequisites)
- [What is Node Exporter](#what-is-node-exporter)
- [Why Use Node Exporter?](#why-use-node-exporter)
- [How Node Exporter Works](#how-node-exporter-works)
- [Install Node Exporter on Ubuntu](#install-node-exporter-on-ubuntu)
  - [Step 1: Download Node Exporter from Official Page](#step-1-download-node-exporter-from-official-page)
  - [Step 2: Extract the File](#step-2-extract-the-file)
  - [Step 3: Move Binary to /usr/local/bin](#step-3-move-binary-to-usrlocalbin)
  - [Step 4: Create Node Exporter User](#step-4-create-node-exporter-user)
  - [Step 5: Create a Custom Node Exporter Service](#step-5-create-a-custom-node-exporter-service)
  - [Step 6: Reload Systemd](#step-6-reload-systemd)
  - [Step 7: Start and Enable Node Exporter](#step-7-start-and-enable-node-exporter)
  - [Step 8: Update Prometheus Configuration](#step-8-update-prometheus-configuration)
  - [Step 9: Restart Prometheus](#step-9-restart-prometheus)
- [Conclusion](#conclusion)
- [Contact Information](#contact-information)


## **Introduction**

Node Exporter is a critical component in the Prometheus monitoring ecosystem. It is an open-source tool designed to collect system-level metrics from Unix-based systems, such as CPU usage, memory consumption, disk I/O, network statistics, and more. 

## **Prerequisites**

- Linux-based system (Ubuntu/CentOS)

- Root or sudo privileges
- Sufficient storage on your system and good internet connectivity.
- Ports Required- 9100 (Prometheus)
  
## **What is Node Exporter**
Node exporter is a Prometheus exporter used for collecting hardware and operating system metrics from a target system. 
It is designed to be lightweight and easy to install on a variety of systems.

## **Why Use Node Exporter?**

Node Exporter is used for:

- **System Health Monitoring:** Tracks CPU, memory, disk usage, and network activity.

- **Performance Analysis:** Identifies resource bottlenecks and trends over time.

- **Alerting and Troubleshooting:** Helps detect issues before they impact operations.

- **Integration with Prometheus:** Provides real-time monitoring with PromQL queries.

- **Lightweight and Efficient:** Consumes minimal resources while providing valuable insights.
___

## **How Node Exporter Works**
Node Exporter runs as a service on the target machine and exposes metrics on an HTTP endpoint (typically http://<host>:9100/metrics). 
Prometheus scrapes this endpoint at regular intervals, stores the data in its time-series database, and makes it available for querying and alerting.

## **Install Node Exporter on Ubuntu**

### **Step 1: Download Node Exporter from [Official Page](https://prometheus.io/download/#node_exporter)**
``` bash
wget https://github.com/prometheus/node_exporter/releases/download/v1.9.0/node_exporter-1.9.0.linux-amd64.tar.gz
```
### **Step 2: Extract the File**

``` bash
sudo tar xvfz node_exporter-*.*-amd64.tar.gz
```

### **Step 3: Move Binary to /usr/local/bin**
``` bash
sudo mv node_exporter-*.*-amd64/node_exporter /usr/local/bin/
```
### **Step 4: Create Node Exporter User**

``` bash
sudo useradd -rs /bin/false node_exporter
```
### **Step 5: Create a Custom Node Exporter Service**
``` bash
sudo nano /etc/systemd/system/node_exporter.service
```
``` bash
[Unit]

Description=Node Exporter

After=network.target

 

[Service]

User=node_exporter

Group=node_exporter

Type=simple

ExecStart=/usr/local/bin/node_exporter

 

[Install]

WantedBy=multi-user.target

```

### **Step 6: Reload Systemd**
``` bash
sudo systemctl daemon-reload
```

### **Step 7: Start and Enable Node Exporter**
``` bash
sudo systemctl enable node_exporter
sudo systemctl start node_exporter
sudo systemctl status node_exporter
```

### **Step 8: Update Prometheus Configuration**

``` bash
sudo nano /etc/prometheus/prometheus.yml
```
```
- job_name: 'Node_Exporter'

    scrape_interval: 5s

    static_configs:

      - targets: ['<Server_IP_of_Node_Exporter_Machine>:9100']
```

### **Step 9: Restart Prometheus**
``` bash

sudo systemctl restart prometheus.service
```

## **Conclusion**

Node Exporter is a vital tool for infrastructure monitoring, offering real-time system metrics that help administrators ensure the health and performance of their servers. 
When integrated with Prometheus and Grafana, it becomes a powerful monitoring solution, allowing organizations to proactively detect and resolve system issues.

## **Contact Information**

| **Name** | **Email address**            | **Github ID**
|----------|-------------------------------|-------------------|
| Nikita joshi    | Nikita.Joshi@mygurukulam.co    | https://github.com/jnikita19  |

