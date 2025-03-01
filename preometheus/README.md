## **Prometheus**

![image](https://github.com/user-attachments/assets/0528d4d9-daad-4bfe-85ee-a07db00880ef)


| **Author** | **Created on** | **Version** | **Last updated by**|**Last Edited On**|**Level** |**Reviewer** |
|------------|---------------------------|-------------|----------------|-----|-------------|-------------|
| Nikita Joshi|  26-02-2025           | v1         | Nikita Joshi    |26-02-2025    |  internal review | komal jaiswal | 



## **What is Prometheus?**

Prometheus is an open-source monitoring system used for collecting and storing time-series data. It was originally built at SoundCloud to monitor their large-scale infrastructure. 
With Prometheus, you can monitor everything from server CPU and memory usage to application-specific metrics.Prometheus supports powerful querying, visualization, and alerting functionalities.

## **Why Use Prometheus?**

Prometheus is used for monitoring system performance, identifying issues, and setting up alerts. It provides:

- Real-time monitoring of applications and infrastructure

- Scalability for cloud-native and distributed environments

- Flexible querying with PromQL (Prometheus Query Language)

- Integration with various exporters and visualization tools like Grafana
  
- Supports third-party tools via exporters.
- Creates visual dashboards with Grafana.

___


![image](https://github.com/user-attachments/assets/12bfa798-148b-47e9-9e2b-5b51b0baeb74)


# Advantages of Prometheus
| Advantage | Description |
|-----------|-------------|
| Open-source and Free | No licensing costs |
| Multi-dimensional Data Model | Supports labels for advanced filtering |
| Efficient Storage | Uses a time-series database optimized for high performance |
| Powerful Query Language | PromQL allows advanced queries and analysis |
| Auto-Discovery | Can dynamically discover targets in cloud environments |
| Alerting Mechanism | Built-in alerting with Alertmanager |


___

# Disadvantages of Prometheus
| Disadvantage | Description |
|-------------|-------------|
| Limited Long-Term Storage | Data retention is limited without external storage solutions |
| Scaling Challenges | May require additional components like Thanos for high availability |
| No Built-in Authentication | Requires external solutions for authentication and authorization |

___

## **Prerequisites for Prometheus:**

- Linux-based system (Ubuntu/CentOS)
- Root user account with sudo  privilege.
- Prometheus system user and group.
- Sufficient storage on your system and good internet connectivity.
- Ports Required- 9090 (Prometheus)


 # **Steps to Install Prometheus**

  Create a system user for Prometheus using below commnds:
  ```
  sudo useradd --no-create-home --shell /bin/false prometheus
  ```

## **Create the directories in which we will be storing our configuration files and libraries:**

  ``` bash
  sudo mkdir /etc/prometheus
  sudo mkdir /var/lib/prometheus
  ```

## **Set the ownership of the /var/lib/prometheus directory with below command:**
  ``` bash
  sudo chown prometheus:prometheus /var/lib/prometheus
  ```

## **You need to inside /tmp :**
  ``` bash
  cd /tmp/
  ```

 ## **Go to the [Official Page](https://prometheus.io/download/#prometheus) downloads Prometheus:**
  ``` bash
  wget https://github.com/prometheus/prometheus/releases/download/v3.2.1/prometheus-3.2.1.linux-amd64.tar.gz
  ```
 ##  **Extract the files using tar :**
  ``` bash
  sudo tar -xvf prometheus-3.2.1.linux-amd64.tar.gz
  ```

 ##  **Move the configuration file and set the owner to the prometheus**

  ``` bash
  cd prometheus-2.47.2.linux-amd64
```
``` bash
  sudo mv prometheus.yml /etc/prometheus
```
``` bash  
sudo chown -R prometheus:prometheus /etc/prometheus
```

## **Move the binaries and set the owner**

``` bash
sudo mv prometheus /usr/local/bin/
```
``` bash
sudo chown prometheus:prometheus /usr/local/bin/prometheus
```

## **Create a Systemd Service File::**
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

## **Reload systemd:**
``` bash
sudo systemctl daemon-reload
```

## **Start and enable Prometheus service:**

``` bash
sudo systemctl start prometheus
sudo systemctl enable prometheus
sudo systemctl status prometheus
```
## **Now access Prometheus in your browser**
``` bash
<server-ip>:9090
```

## **Conclusion**

Prometheus is a powerful monitoring tool that provides real-time insights into system performance. Its flexibility and integration with other tools make it a preferred choice for DevOps and SRE teams. However, it requires careful scaling and security considerations for large environments.
By following best practices, organizations can maximize the benefits of Prometheus for robust monitoring and alerting.

## **Contact Information**

| **Name** | **Email address**            | **Github ID**
|----------|-------------------------------|-------------------|
| Nikita joshi    | Nikita.Joshi@mygurukulam.co    | https://github.com/jnikita19  |

