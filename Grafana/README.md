# **Grafana**
![image](https://github.com/user-attachments/assets/b70ac4ae-6407-40b2-8a66-eebcf4ec53a5)

| **Author** | **Created on** | **Version** | **Last updated by**|**Last Edited On**|**Level** |**Reviewer** |
|------------|---------------------------|-------------|----------------|-----|-------------|-------------|
| Nikita Joshi|  26-02-2025           | v1         | Nikita Joshi    |26-02-2025    |  internal review | komal jaiswal | 
___
# Table of Contents

- [Introduction](#introduction)
- [Prerequisites](#prerequisites)
- [What is Grafana?](#what-is-grafana)
- [Why do we Use Grafana?](#why--do-we-use-grafana)
- [How Does Grafana Work?](#how-does-grafana-work)
- [Advantages of Grafana](#advantages-of-grafana)
- [Disadvantages of Grafana](#disadvantages-of-grafana)
- [Installation Steps](#installation-steps)
  - [Download the Grafana GPG key](#download-the-grafana-gpg-key)
  - [Add the Grafana repository](#add-the-grafana-repository)
  - [Update package lists](#update-package-lists)
  - [Install Grafana](#install-grafana)
  - [Start the Grafana server](#start-the-grafana-server)
  - [Check service status](#check-service-status)
  - [Access in browser](#access-in-browser)
  - [Output](#output)
- [Conclusion](#conclusion)
- [Contact Information](#contact-information)

## **Introduction**

Grafana is an open-source analytics and interactive visualization platform. It allows users to query, visualize, and analyze data from various sources, including Prometheus, InfluxDB, MySQL, and Elasticsearch. Grafana provides powerful dashboards that help monitor infrastructure, applications, and services in real-time.

## **Prerequisites**

- Linux-based system (Ubuntu/CentOS)

- user with sudo privileges
- Sufficient storage on your system and good internet connectivity.
- Ports Required- 3000 (Prometheus)


## **what is Grafana?**

Grafana is a data visualization and dashboarding platform that can be used to display the data collected by Prometheus. 
It provides a flexible and user-friendly interface for creating charts, graphs, and dashboards.

## **Why  do we Use Grafana?**

Grafana is used for:

- Real-time data visualization and monitoring

- Custom dashboard creation with rich UI components

- Integration with various data sources

- Setting up alerts and notifications for system performance
 
- Analyzing trends and anomalies over time


## **How Does Grafana Work?**

Grafana works by connecting to data sources and querying them to display visual insights. The workflow includes:

**Data Source Connection:** Users configure data sources like Prometheus, MySQL, or Elasticsearch.

**Query Execution:** Grafana retrieves data from the source using a query language (e.g., PromQL for Prometheus).

**Dashboard Creation:** Users build dashboards using panels to visualize metrics in graphs, tables, or heatmaps.

**Alerting:** Users define conditions to trigger alerts via email, Slack, or webhook integrations.

## **Advantages of Grafana**

**Open-Source:** Free to use and highly customizable.

**Multi-Source Support:** Works with a wide range of data sources.

**Real-Time Monitoring:** Provides live updates on metrics.

**Community Support:** Large community and extensive documentation.

## **Disadvantages of Grafana**

**Learning Curve:** Requires some knowledge of data sources and query languages.

**Limited Data Storage:** Grafana itself does not store data; it relies on external data sources.

**Resource Intensive:** Can consume significant resources for large datasets or complex dashboards.

**Alert Limitations:** Alerting features are not as advanced as some dedicated monitoring tools.

___
## **Installation Steps**

### **Download the Grafana GPG key** 

``` bash
wget -q -O - https://packages.grafana.com/gpg.key | sudo apt-key add -
```

### **Add the Grafana repository**
``` bash
sudo add-apt-repository "deb https://packages.grafana.com/oss/deb stable main"
```

### **Update package lists**
``` bash
sudo apt update
```

### **Install Grafana**
``` bash
sudo apt install grafana
```

### **Start the Grafana server**
``` bash
sudo systemctl start grafana-server
```

### **Check service status**
``` bash
sudo systemctl status grafana-server
sudo systemctl enable grafana-server
```

### **Access in browser**
``` bash
<instance_ip>:3000
```

**NOTE**

default username: admin <br/>
default password: admin

![image](https://github.com/user-attachments/assets/ef86acf8-0649-4ced-a1d8-852b93175bcf)

**To visualize metrics, you need to add a data source first.**

![image](https://github.com/user-attachments/assets/811203f9-62dd-483a-8faf-f74318f31fd8)

**Configuring Data Sources**

For the URL, enter http://localhost:9090 and click Save and test. You can see Data source is working.

Click on Save and Test.

Let’s add Dashboard for a better view in Grafana

Click On Dashboard → + symbol → Import Dashboard

Click on Import Dashboard paste this code 1860 and click on load

![image](https://github.com/user-attachments/assets/79a42540-fa6e-4b1e-a08a-5ab1007b7e9c)
___
### **Output**
![Screenshot 2025-03-01 004708](https://github.com/user-attachments/assets/e1b7bac5-f042-4032-a9c2-c85b40b05dfe)
___
## **Conclusion**

Grafana is a powerful visualization and monitoring tool that provides real-time insights into system and application performance. It integrates with multiple data sources, offers customizable dashboards, and supports alerting mechanisms. While it has some limitations, such as high resource consumption and complex queries, 
it remains a preferred choice for DevOps teams and IT professionals looking to enhance observability.
___
## **Contact Information**

| **Name** | **Email address**            | **Github ID**
|----------|-------------------------------|-------------------|
| Nikita joshi    | Nikita.Joshi@mygurukulam.co    | https://github.com/jnikita19  |


