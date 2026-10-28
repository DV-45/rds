\# AWS RDS Practical Assignment



\## 📌 Objective



This assignment demonstrates how to:



\- Create a DB Subnet Group

\- Launch an Amazon RDS MySQL database

\- Connect to the database using its endpoint

\- Create a Read Replica

\- Promote the Read Replica into a standalone database instance



Reference: AWS\_RDS\_Practical\_Assignment.pdf 【1-9f08f9】



\---



\## 🏗️ Architecture



```text

VPC

│

├── Subnet-A (AZ-1)

├── Subnet-B (AZ-2)

│

├── DB Subnet Group

│

├── RDS Primary Instance

│     │

│     └── Read Replica

│             │

│             └── Promoted Standalone DB

│

└── EC2 Instance

&#x20;     │

&#x20;     └── MySQL Connection via RDS Endpoint

```



\---



\## ✅ Prerequisites



Before starting, ensure you have:



\- AWS Account

\- Amazon RDS access

\- Amazon EC2 access

\- VPC with subnets in at least two Availability Zones

\- Security Group configured for MySQL access (TCP Port 3306)

\- MySQL client installed on EC2 or local machine



> \*\*Note:\*\* RDS resources may incur AWS charges. Use free-tier eligible configurations whenever possible. 【1-9f08f9】



\---



\# Task 1: Create a DB Subnet Group



\### Steps



1\. Open \*\*AWS Console\*\*

2\. Navigate to \*\*Amazon RDS → Subnet Groups\*\*

3\. Click \*\*Create DB Subnet Group\*\*

4\. Configure:



| Parameter | Value |

|------------|---------|

| Name | `rds-lab-subnet-group` |

| Description | RDS Lab Subnet Group |

| VPC | Your VPC |

| Subnets | At least 2 Availability Zones |



5\. Click \*\*Create\*\*



\### Expected Result



DB Subnet Group successfully created.



\---



\# Task 2: Create an RDS Database Instance



\### Configuration



| Parameter | Value |

|------------|---------|

| Engine | MySQL |

| Database Identifier | `rds-lab-primary` |

| Public Access | No |

| Port | 3306 |

| Subnet Group | `rds-lab-subnet-group` |



\### Steps



1\. Navigate to \*\*RDS → Databases\*\*

2\. Click \*\*Create Database\*\*

3\. Select \*\*Standard Create\*\*

4\. Choose \*\*MySQL\*\*

5\. Configure database settings

6\. Select the subnet group created earlier

7\. Configure security group rules

8\. Click \*\*Create Database\*\*

9\. Wait until status becomes \*\*Available\*\*



\### Record Details



```text

DB Identifier :

Endpoint      :

Port          :

Status        :

```



\### Verification



Ensure:



\- Database status = Available

\- Endpoint is generated

\- Automated backups are enabled



\---



\# Task 3: Connect to RDS Endpoint



\### Retrieve Endpoint



```text

RDS

&#x20;└── Databases

&#x20;     └── rds-lab-primary

&#x20;          └── Connectivity \& Security

```



Copy:



\- Endpoint

\- Port



\### Connect Using MySQL



```bash

mysql -h <RDS\_ENDPOINT> -P 3306 -u <MASTER\_USERNAME> -p

```



\### Verify Connection



```sql

SELECT VERSION();



SHOW DATABASES();

```



\### Create Sample Database



```sql

CREATE DATABASE rds\_lab;



USE rds\_lab;



CREATE TABLE demo (

&#x20;   id INT PRIMARY KEY,

&#x20;   note VARCHAR(50)

);



INSERT INTO demo VALUES (1, 'hello');



SELECT \* FROM demo;

```



\### Expected Output



```text

+----+-------+

| id | note  |

+----+-------+

|  1 | hello |

+----+-------+

```



\---



\# Task 4: Create a Read Replica



\### Steps



1\. Open \*\*Amazon RDS\*\*

2\. Select 

