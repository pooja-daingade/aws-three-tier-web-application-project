# AWS Three-Tier Web Application Deployment

##  Project Overview

This project demonstrates the deployment of a **Three-Tier Web Application on AWS** using a secure and structured architecture.

The application is divided into three layers:

* **Web Tier** – Nginx Reverse Proxy
* **Application Tier** – Apache Tomcat
* **Database Tier** – Amazon RDS MariaDB

The infrastructure was deployed using Amazon VPC, EC2, NAT Gateway, Route Tables, Security Groups, Route 53, and AWS Certificate Manager (ACM).

The application was successfully accessed using the custom domain:

**https://poojadaingade.shop**

---
##  Project Architecture


<img width="1532" height="1027" alt="AWS Three-Tier Web Application Deployment Architecture" src="https://github.com/user-attachments/assets/6215725c-5e06-4400-a969-e1e031fdcfb1" />

### Architecture Components

* Amazon VPC
* Public Subnet
* Private Subnet
* Internet Gateway
* NAT Gateway
* Route Tables
* Security Group
* EC2
* Nginx
* Apache Tomcat
* Amazon RDS MariaDB
* Route 53
* AWS Certificate Manager (ACM)

---

##  AWS Services Used

| Service                | Purpose                                                    |
| ---------------------- | ---------------------------------------------------------- |
| **Amazon VPC**         | Created an isolated network environment                    |
| **Amazon EC2**         | Hosted Jump Server, Application Server and Database Server |
| **Internet Gateway**   | Provided internet connectivity to the public subnet        |
| **NAT Gateway**        | Provided outbound internet access to private subnets       |
| **Route Tables**       | Controlled public and private subnet routing               |
| **Security Groups**    | Controlled inbound and outbound traffic                    |
| **Amazon RDS MariaDB** | Provided managed relational database storage               |
| **Route 53**           | Managed DNS for the custom domain                          |
| **AWS ACM**            | Provided SSL/TLS certificate                               |
| **Nginx**              | Configured as a reverse proxy                              |
| **Apache Tomcat**      | Hosted and served the Java web application                 |

---

##  Network Configuration

### VPC

* VPC Name: `my-vpc`
* CIDR Block: `10.0.0.0/16`

### Subnets

* `public-subnet`
* `private-subnet-1`
* `private-subnet-2`

The public subnet was configured for internet-facing access, while the private subnets were used for the application and database infrastructure.

### Internet Gateway

An Internet Gateway was attached to the VPC to provide internet connectivity to resources in the public subnet.

### NAT Gateway

A NAT Gateway named `my-nat` was created in the public subnet and associated with an Elastic IP.

It provides outbound internet access for resources deployed in the private subnets.

---

##  Security Configuration

A Security Group named `my-sg` was configured to control network traffic.

### Allowed Ports

* SSH – `22`
* HTTP – `80`
* HTTPS – `443`
* MySQL/MariaDB – `3306`
* Custom TCP – `8080`

---

##  EC2 Infrastructure

Three EC2 instances were configured:

### 1. Jump Server

* Name: `jump-server`
* Location: Public Subnet
* Instance Type: `t3.micro`
* OS: Amazon Linux

The Jump Server acts as a **bastion host** for securely accessing the private servers.

### 2. Application Server

* Name: `application-server`
* Location: Private Subnet
* Instance Type: `t3.micro`
* OS: Amazon Linux

Apache Tomcat was installed and configured on this server to host the Java web application.

### 3. Database Server

* Name: `database-server`
* Location: Private Subnet
* Instance Type: `t3.micro`
* OS: Amazon Linux

The server was configured with the MariaDB client to securely connect to Amazon RDS MariaDB.

---

##  Application Deployment

Apache Tomcat was installed on the application server.

The application deployment included:

1. Installed Java.
2. Downloaded and installed Apache Tomcat.
3. Deployed the `student.war` application.
4. Added the MySQL Connector JAR.
5. Configured the Tomcat `context.xml`.
6. Started Apache Tomcat.
7. Verified the application server successfully.

---

##  Database Configuration

Amazon RDS MariaDB was used as the database layer.

### Database Configuration

* Database Engine: **MariaDB**
* DB Identifier: `database-1`
* Database: `studentapp`

The application was successfully connected to the RDS MariaDB database.

The `students` table was verified using SQL queries.

---

##  Nginx Reverse Proxy

Nginx was configured on the Jump Server as a **Reverse Proxy**.

Incoming requests were forwarded to the Apache Tomcat application server running on port `8080`.

```text
User Request
     │
     ▼
Nginx
     │
     ▼
Apache Tomcat :8080
     │
     ▼
RDS MariaDB
```

This configuration allowed the application server to remain inside the private subnet while users accessed the application through the public-facing server.

---

##  Custom Domain & HTTPS

A custom domain was configured for the application:

**poojadaingade.shop**

### Configuration

* Domain purchased from Hostinger
* DNS managed using Amazon Route 53
* SSL/TLS certificate issued using AWS Certificate Manager (ACM)
* HTTPS configured for secure communication

The application was successfully accessed using the custom domain instead of the EC2 public IP.

---

##  Application Verification

The complete application flow was tested successfully.

### Test Flow

```text
User
 ↓
poojadaingade.shop
 ↓
Route 53
 ↓
Nginx Reverse Proxy
 ↓
Apache Tomcat
 ↓
RDS MariaDB
```

A sample student record was submitted through the Student Registration Form.

The submitted data was:

* Displayed successfully on the Students List page
* Stored successfully in the MariaDB database
* Verified using an SQL query

This confirmed successful **end-to-end communication** between the web, application, and database layers.

---

##  Project Outcomes

* Successfully deployed a secure **AWS Three-Tier Web Application Architecture**
* Configured Amazon VPC with public and private subnets
* Configured Internet Gateway and NAT Gateway
* Configured Route Tables and Security Groups
* Deployed EC2-based infrastructure
* Installed and configured Apache Tomcat
* Configured Nginx as a Reverse Proxy
* Integrated the application with Amazon RDS MariaDB
* Configured custom domain using Route 53
* Configured SSL/TLS using AWS Certificate Manager
* Successfully verified application and database connectivity

---

##  Technologies Used

**Cloud:** AWS

**Networking:** VPC, Subnets, Internet Gateway, NAT Gateway, Route Tables, Security Groups

**Compute:** Amazon EC2

**Web Server / Reverse Proxy:** Nginx

**Application Server:** Apache Tomcat

**Database:** Amazon RDS MariaDB

**DNS:** Amazon Route 53

**SSL/TLS:** AWS Certificate Manager

**OS:** Amazon Linux

**Application:** Java WAR Application

---

##  Author

**Pooja Daingade**
