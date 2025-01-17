# Webapplication with RDS, Global Accelerator and Elasticache
![Screenshot_1](https://github.com/user-attachments/assets/331cc1bb-d725-4088-9ec8-53266dae83bd)

## Overview
This project is a scalable web application built on AWS, utilizing various services to enhance performance, reliability, and user experience.

## Features
- **Relational Database Management**: Utilized Amazon RDS for efficient data handling.
- **Global Traffic Management**: Implemented AWS Global Accelerator to optimize performance and availability.
- **Caching Mechanism**: Integrated Amazon ElastiCache to improve application speed and reduce database load.

<strong> Created two EC2 instance. One in us-east-1 and the other in ap-south-1: </strong><br>
- **US East (Virginia):**
![ec2 usa](https://github.com/user-attachments/assets/59d48613-a36a-413f-bdb6-1d8abf06622b)

- **AP South (Mumbai):**
![ec2 mumbai](https://github.com/user-attachments/assets/9f6b5f04-5feb-4507-b4ab-ca0959ea25f0)

<strong> Created RDS MySQL: </strong>
![rds](https://github.com/user-attachments/assets/7cceac53-5457-47c3-934d-7057aef0a06a)

<strong> You can connect to the RDS MySQL instance using MySQL Workbench. Sample data is available as "MOCK_DATA" in the repository</strong>
![uploading data in a database](https://github.com/user-attachments/assets/35089ef5-801c-44e6-a6de-4357673fac0d)

<strong> Created Elasticache Redis Cluster: </strong><br>
<strong>Amazon ElastiCache enhances performance by ensuring that the data most frequently accessed is always available.</strong>
![redis cluster](https://github.com/user-attachments/assets/614adcf9-4fab-42bb-ba7e-7b40cca158a4)

<strong>External access to the Redis cluster has been enabled through a Security Group, which is attached to both the EC2 instances and ElastiCache:</strong>
![sg](https://github.com/user-attachments/assets/ddcce567-07b9-47e8-ac7f-393bb01caa3f)

<strong> A Global Accelerator has been configured with endpoints in both us-east-1 and ap-south-1 regions: </strong><br>
<strong> Amazon Global Accelerator facilitates automatic traffic routing to the nearest endpoint, significantly enhancing performance. Additionally, the system provides an automatic failover to a secondary region in the event of primary region unavailability, thereby increasing overall high availability. <strong>
![global accelerator 1](https://github.com/user-attachments/assets/2ced94cc-0159-4252-a2ed-7bdb081ebde1)
![global accelerator 2](https://github.com/user-attachments/assets/1c22e497-cc71-47c3-92d2-307625044cc1)
![global accelerator 3](https://github.com/user-attachments/assets/734dcab4-87c6-4a55-90ff-8b6334283900)
![global accelerator mumbai endpoint](https://github.com/user-attachments/assets/0723e75f-2ffb-4ee6-b06d-1cff6032619d)
![global accelerator useast endpoint](https://github.com/user-attachments/assets/fa8d744b-d5a5-480b-ae23-0596665fe694)

# [Testing]
<strong>Geographic Routing:</strong>
- **Accessing from Asia: Users are routed to the nearest endpoint in Mumbai, enhancing performance:**
![from mumbai](https://github.com/user-attachments/assets/89c6cc26-9297-4a9b-ab75-7eeeb5f0d183)

- **Accessing from America: Users are routed to the nearest endpoint in US-EAST, enhancing performance:**
![from us east](https://github.com/user-attachments/assets/6604de91-9ac5-4215-814b-d22327f2321b)

# [Speed Difference without redis]
- **It took 0.0071 seconds to fetch the data from database**
![cache miss](https://github.com/user-attachments/assets/59cd1903-acd7-4d2d-9c59-4e0bb5b6e12e)

# [Speed Difference with redis]
- **Fetching data with Redis took only 0.0016 seconds, resulting in a 77.5% reduction in latency**
![cache hit](https://github.com/user-attachments/assets/bd54a9e8-30df-4fe6-83ee-d8af3ac96f0a)

# [Monitoring redis]
<Strong>Monitor Redis performance metrics using the following visuals:</strong>
![redis metric 2](https://github.com/user-attachments/assets/1591537f-dbdf-438a-b4bc-555a47c3773a)
![redis metric](https://github.com/user-attachments/assets/63e2a0c3-adfc-4a90-9e56-9495722aaca7)


