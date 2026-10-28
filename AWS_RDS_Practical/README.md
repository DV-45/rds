# AWS RDS Practical Assignment

## 📌 Objective

This assignment demonstrates how to:

- Create a DB Subnet Group
- Launch an Amazon RDS MySQL database
- Connect to the database using its endpoint
- Create a Read Replica
- Promote the Read Replica into a standalone database instance

---

## 🏗️ Architecture

```text
VPC
│
├── Subnet-A (AZ-1)
├── Subnet-B (AZ-2)
│
├── DB Subnet Group
│
├── RDS Primary Instance
│    │
│    └── Read Replica
│         │
│         └── Promoted Standalone DB
│
└── EC2 Instance
     │
     └── MySQL Connection
```

## ✅ Prerequisites

- AWS Account
- Amazon RDS access
- Amazon EC2 access
- MySQL Client

## Task 1: Create a DB Subnet Group

1. Open AWS Console
2. Navigate to Amazon RDS → Subnet Groups
3. Create a subnet group
4. Select subnets from at least two Availability Zones

## Task 2: Create an RDS Database Instance

- Engine: MySQL
- Identifier: rds-lab-primary
- Port: 3306

## Task 3: Connect to RDS Endpoint

```bash
mysql -h <RDS_ENDPOINT> -P 3306 -u <MASTER_USERNAME> -p
```

## Task 4: Create a Read Replica

1. Select primary database
2. Create Read Replica
3. Wait for Available status

## Task 5: Promote Read Replica

1. Select replica
2. Click Promote Read Replica
3. Verify standalone status

## Conclusion

Successfully created an RDS database, connected through its endpoint, created a Read Replica, and promoted the replica to a standalone database.
