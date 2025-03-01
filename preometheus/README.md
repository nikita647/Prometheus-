## **Prometheus**

![image](https://github.com/user-attachments/assets/0528d4d9-daad-4bfe-85ee-a07db00880ef)


| **Author** | **Created on** | **Version** | **Last updated by**|**Last Edited On**|**Level** |**Reviewer** |
|------------|---------------------------|-------------|----------------|-----|-------------|-------------|
| Nikita Joshi|  2-03-2025           | v1         | Nikita Joshi    |2-03-2025    |  internal review | komal jaiswal | 

## **Table of Contents**

1. [Introduction](#introduction)
2. [Prerequisites for Prometheus](#prerequisites-for-prometheus)
3. [Why Use Prometheus?](#why-use-prometheus)
4. [Advantages of Prometheus](#advantages-of-prometheus)
5. [Disadvantages of Prometheus](#disadvantages-of-prometheus)
6. [Steps to Install Prometheus](#steps-to-install-prometheus)
   - [Create a system user for Prometheus](#create-a-system-user-for-prometheus)
   - [Create configuration directories](#create-configuration-directories)
   - [Set directory ownership](#set-directory-ownership)
   - [Navigate to `/tmp`](#navigate-to-tmp)
   - [Download Prometheus from the official page](#download-prometheus-from-the-official-page)
   - [Extract the Prometheus package](#extract-the-prometheus-package)
   - [Move and set ownership of configuration files](#move-and-set-ownership-of-configuration-files)
   - [Move binaries and set ownership](#move-binaries-and-set-ownership)
   - [Create a Systemd Service File](#create-a-systemd-service-file)
   - [Reload systemd and start Prometheus](#reload-systemd-and-start-prometheus)
   - [Access Prometheus in the browser](#access-prometheus-in-the-browser)
7. [Conclusion](#conclusion)
8. [Contact Information](#contact-information)

## **Introduction**
Prometheus is an open-source monitoring system used for collecting and storing time-series data. It was originally built at SoundCloud to monitor their large-scale infrastructure. 
With Prometheus, you can monitor everything from server CPU and memory usage to application-specific metrics.Prometheus supports powerful querying, visualization, and alerting functionalities.
__
## **Prerequisites for Prometheus:**

- Linux-based system (Ubuntu/CentOS)
- user with sudo  privilege.
- Prometheus system user and group.
- Sufficient storage on your system and good internet connectivity.
- Ports Required- 9090 (Prometheus)
  ___

## **Why Use Prometheus?**

Prometheus is used for monitoring system performance, identifying issues, and setting up alerts. It provides:

- Real-time monitoring of applications and infrastructure

- Scalability for cloud-native and distributed environments

- Flexible querying with PromQL (Prometheus Query Language)

- Integration with various exporters and visualization tools like Grafana
  
- Supports third-party tools via exporters.
- Creates visual dashboards with Grafana.

___




##  **Advantages of Prometheus**
| Advantage | Description |
|-----------|-------------|
| Open-source and Free | No licensing costs |
| Multi-dimensional Data Model | Supports labels for advanced filtering |
| Efficient Storage | Uses a time-series database optimized for high performance |
| Powerful Query Language | PromQL allows advanced queries and analysis |
| Auto-Discovery | Can dynamically discover targets in cloud environments |
| Alerting Mechanism | Built-in alerting with Alertmanager |


___

##  **Disadvantages of Prometheus**
| Disadvantage | Description |
|-------------|-------------|
| Limited Long-Term Storage | Data retention is limited without external storage solutions |
| Scaling Challenges | May require additional components like Thanos for high availability |
| No Built-in Authentication | Requires external solutions for authentication and authorization |

___




## **Steps to Install Prometheus**

### **Create a system user for Prometheus**
  ```
  sudo useradd --no-create-home --shell /bin/false prometheus
  ```
___
### **Create configuration directories**

  ``` bash
  sudo mkdir /etc/prometheus
  sudo mkdir /var/lib/prometheus
  ```
___
### **Set directory ownership**
  ``` bash
  sudo chown prometheus:prometheus /var/lib/prometheus
  ```
___
### **Navigate to `/tmp`**
  ``` bash
  cd /tmp/
  ```
___
### **Download Prometheus from the [Official Page](https://prometheus.io/download/#prometheus)**
  ``` bash
  wget https://github.com/prometheus/prometheus/releases/download/v3.2.1/prometheus-3.2.1.linux-amd64.tar.gz
 ```

___
###  **Extract the Prometheus package**
  ``` bash
  sudo tar -xvf prometheus-3.2.1.linux-amd64.tar.gz
  ```
___
###  **Move and set ownership of configuration files**

  ``` bash
  cd prometheus-2.47.2.linux-amd64
```
``` bash
  sudo mv prometheus.yml /etc/prometheus
```
``` bash  
sudo chown -R prometheus:prometheus /etc/prometheus
```
___
### **Move binaries and set ownership**

``` bash
sudo mv prometheus /usr/local/bin/
```
``` bash
sudo chown prometheus:prometheus /usr/local/bin/prometheus
```
___
### **Create a Systemd Service File**
``` bash
sudo nano /etc/systemd/system/prometheus.service
```

``` bash
[Unit]
Description=Prometheus
Wants=network-online.target
After=network-online.target

[Service]
User=prometheus
Group=prometheus
Type=simple
ExecStart=/usr/local/bin/prometheus \
    --config.file /etc/prometheus/prometheus.yml \
    --storage.tsdb.path /var/lib/prometheus/ \
    --web.console.templates=/etc/prometheus/consoles \
    --web.console.libraries=/etc/prometheus/console_libraries

[Install]
WantedBy=multi-user.target
```
___
### **Reload systemd and start Prometheus**
``` bash
sudo systemctl daemon-reload
sudo systemctl start prometheus
sudo systemctl enable prometheus
sudo systemctl status prometheus
```

___
### **Access Prometheus in the browser**
``` bash
<server-ip>:9090
```
___
## **Conclusion**

Prometheus is a powerful monitoring tool that provides real-time insights into system performance. Its flexibility and integration with other tools make it a preferred choice for DevOps and SRE teams. However, it requires careful scaling and security considerations for large environments.
By following best practices, organizations can maximize the benefits of Prometheus for robust monitoring and alerting.
___
## **Contact Information**

| **Name** | **Email address**            | **Github ID**
|----------|-------------------------------|-------------------|
| Nikita joshi    | Nikita.Joshi@mygurukulam.co    | https://github.com/jnikita19  |

