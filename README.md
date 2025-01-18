# Scalable Web Application with RDS, Global Accelerator, and ElastiCache

This project demonstrates how to build a **scalable web application** on **AWS**, utilizing several AWS services to enhance performance, reliability, and user experience. The application leverages **Amazon RDS**, **Global Accelerator**, and **ElastiCache** to optimize data management, traffic routing, and caching.
![Screenshot_1](https://github.com/user-attachments/assets/331cc1bb-d725-4088-9ec8-53266dae83bd)


## Overview

This web application is designed to scale efficiently by:
- Using **Amazon RDS** for relational database management.
- Implementing **AWS Global Accelerator** for global traffic management and high availability.
- Integrating **Amazon ElastiCache (Redis)** to improve performance by caching frequently accessed data.

## Features

- **Relational Database Management**: Amazon **RDS (MySQL)** is used for efficient data handling, ensuring high availability and scalability.
- **Global Traffic Management**: **AWS Global Accelerator** optimizes performance by routing traffic to the nearest available endpoints, reducing latency and improving user experience.
- **Caching Mechanism**: **Amazon ElastiCache** improves speed by caching data and reducing database load.

---

## Architecture Overview

### EC2 Instances

Two EC2 instances were created in different regions to enhance fault tolerance and performance:
- **US East (Virginia)**: Hosting one EC2 instance.
  ![EC2 US East](https://github.com/user-attachments/assets/59d48613-a36a-413f-bdb6-1d8abf06622b)

- **AP South (Mumbai)**: Hosting another EC2 instance for Asia-based users.
  ![EC2 Mumbai](https://github.com/user-attachments/assets/9f6b5f04-5feb-4507-b4ab-ca0959ea25f0)

### RDS MySQL Instance

An **RDS MySQL** instance is used to store the application data, which can be accessed securely by the EC2 instances.

![RDS MySQL](https://github.com/user-attachments/assets/7cceac53-5457-47c3-934d-7057aef0a06a)

> You can connect to the RDS MySQL instance using **MySQL Workbench**. Sample data is available as **"MOCK_DATA"** in the repository.

#### Screenshot of uploading data:
![Uploading Data to RDS](https://github.com/user-attachments/assets/35089ef5-801c-44e6-a6de-4357673fac0d)

### ElastiCache Redis Cluster

**Amazon ElastiCache Redis** is used to cache frequently accessed data, reducing database load and improving application speed.

![Redis Cluster](https://github.com/user-attachments/assets/614adcf9-4fab-42bb-ba7e-7b40cca158a4)

**Security Groups** were configured to allow external access to the Redis cluster. This security group is attached to both the EC2 instances and ElastiCache cluster.

![Security Group](https://github.com/user-attachments/assets/ddcce567-07b9-47e8-ac7f-393bb01caa3f)

### Global Accelerator

**AWS Global Accelerator** is configured with endpoints in both **us-east-1** and **ap-south-1** regions. This service automatically routes user traffic to the nearest available endpoint, ensuring low-latency access and providing automatic failover to a secondary region in case of primary region failure.

#### Screenshots of Global Accelerator:
- Global Accelerator setup:
  ![Global Accelerator 1](https://github.com/user-attachments/assets/2ced94cc-0159-4252-a2ed-7bdb081ebde1)
  ![Global Accelerator 2](https://github.com/user-attachments/assets/1c22e497-cc71-47c3-92d2-307625044cc1)
  ![Global Accelerator 3](https://github.com/user-attachments/assets/734dcab4-87c6-4a55-90ff-8b6334283900)

- Mumbai endpoint:
  ![Global Accelerator Mumbai](https://github.com/user-attachments/assets/0723e75f-2ffb-4ee6-b06d-1cff6032619d)

- US East endpoint:
  ![Global Accelerator US East](https://github.com/user-attachments/assets/fa8d744b-d5a5-480b-ae23-0596665fe694)

---

## Testing

### Geographic Routing

#### From Asia (Mumbai):
- **Users from Asia** are routed to the nearest endpoint in Mumbai, optimizing performance.
  ![From Mumbai](https://github.com/user-attachments/assets/89c6cc26-9297-4a9b-ab75-7eeeb5f0d183)

#### From America (US East):
- **Users from the US** are routed to the nearest endpoint in US East (Virginia), improving performance.
  ![From US East](https://github.com/user-attachments/assets/6604de91-9ac5-4215-814b-d22327f2321b)

---

### Speed Testing: Without Redis (Cache Miss)

When data is fetched directly from the database without Redis caching, the request took **0.0071 seconds**.

![Cache Miss](https://github.com/user-attachments/assets/59cd1903-acd7-4d2d-9c59-4e0bb5b6e12e)

### Speed Testing: With Redis (Cache Hit)

With Redis caching enabled, the same data fetch took only **0.0016 seconds**, resulting in a **77.5% reduction in latency**.

![Cache Hit](https://github.com/user-attachments/assets/bd54a9e8-30df-4fe6-83ee-d8af3ac96f0a)

---

### Monitoring Redis Performance

Here are some Redis performance metrics to help monitor the health and performance of the Redis cache.

![Redis Metric 2](https://github.com/user-attachments/assets/1591537f-dbdf-438a-b4bc-555a47c3773a)
![Redis Metric](https://github.com/user-attachments/assets/63e2a0c3-adfc-4a90-9e56-9495722aaca7)
