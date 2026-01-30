
# Enterprise VPC Design with Multi-Size Subnets & Controlled Internet Access


This document explains the complete setup of an AWS VPC with properly planned CIDR ranges, multiple subnets, routing, and EC2 connectivity testing. All steps are aligned with AWS best practices and supported by screenshots.


---

##  Steps to Build 

### Step 1: Create VPC

* Create a VPC with CIDR **10.0.0.0/16**
* This provides a large IP range for future expansion

---

### Step 2: Create Internet Gateway (IGW)

* Create one Internet Gateway
* Attach it to the VPC
* This allows public subnets to access the internet

---

### Step 3: Create Subnets (6 Total)

Create exactly **6 subnets** with different sizes inside the VPC:

1. **Shared Subnet** – `/19` → Internal services
2. **Platform Subnet** – `/20` → Containers and tools
3. **App Subnet** – `/21` → Application tier
4. **Web Subnet** – `/22` → Web tier
5. **Edge Subnet** – `/23` → Load balancers
6. **Admin Subnet** – `/24` → Bastion / Ops

 Ensure no CIDR overlap
 Allocate largest subnets first

---

### Step 4: Create Route Tables

* Create **Public Route Table**
* Create **Private Route Table**

---

### Step 5: Configure Routes

* In **Public Route Table**, add route:

  * `0.0.0.0/0 → Internet Gateway`
* **Private Route Table** should only have the local VPC route

---

### Step 6: Associate Subnets to Route Tables

* **Public Route Table**

  * Admin Subnet
  * Edge Subnet
* **Private Route Table**

  * Web Subnet
  * App Subnet
  * Platform Subnet
  * Shared Subnet

---

### Step 7: Launch EC2 Instances

* Launch one EC2 in a **public subnet**
* Launch one EC2 in a **private subnet**

---

### Step 8: Test Connectivity

* Public EC2:

  * Can access the internet 
* Private EC2:

  * Cannot access the internet 
* All subnets:

  * Can communicate internally within the VPC 

---

### Step 9: Verify Design

* Confirm IGW is attached only once
* Ensure private subnets have no internet route
* Verify correct route table associations


---

## Step 1: Create VPC

**VPC CIDR:** `10.0.0.0/16`

### Why `/16` CIDR?

* Provides **65,536 IP addresses**
* Allows creation of multiple large and small subnets
* Supports future scalability
* Commonly used in enterprise AWS architectures



![VPC Creation](https://github.com/user-attachments/assets/414840a6-640a-477e-b2c0-9dbee5680771)
![VPC CIDR](https://github.com/user-attachments/assets/eee58d4b-38b2-4036-809a-555b2e940d48)

---

## Step 2: Create and Attach Internet Gateway

An **Internet Gateway (IGW)** enables communication between the VPC and the internet.

### Actions Performed

* Created Internet Gateway
* Attached it to the VPC

### Why IGW is Required?

* Allows public subnets to access the internet
* Enables inbound/outbound traffic for public EC2 instances



![IGW Creation](https://github.com/user-attachments/assets/55f06dc9-1a1d-4a8c-8763-852fd2ad28e9)
![IGW Attach](https://github.com/user-attachments/assets/ce22ec56-e96b-4bd9-a3d7-d2cd5f049cb1)
![IGW Attached](https://github.com/user-attachments/assets/19202879-5832-4bd3-b06c-60392e6f40e2)

---

## Step 3: Create 6 Subnets (Unequal CIDR Allocation)

Exactly **6 subnets** are created with different IP capacities based on usage.

### Subnet Allocation Table

| Subnet Name | Purpose            | CIDR | Address Range           |
| ----------- | ------------------ | ---- | ----------------------- |
| Shared      | Internal Services  | /19  | 10.0.0.0 – 10.0.31.255  |
| Platform    | Containers & Tools | /20  | 10.0.32.0 – 10.0.47.255 |
| App         | Application Tier   | /21  | 10.0.48.0 – 10.0.55.255 |
| Web         | Web Tier           | /22  | 10.0.56.0 – 10.0.59.255 |
| Edge        | Load Balancers     | /23  | 10.0.60.0 – 10.0.61.255 |
| Admin       | Bastion / Ops      | /24  | 10.0.62.0 – 10.0.62.255 |

### Why Unequal Subnets?

* Optimized IP usage
* Prevents IP wastage
* Matches real-world workload needs



![Subnet 1](https://github.com/user-attachments/assets/22978a49-a9da-47fd-b806-16060331b04e)
![Subnet 2](https://github.com/user-attachments/assets/ec50145c-4272-46f5-860a-03e37aab91e7)
![Subnet 3](https://github.com/user-attachments/assets/f4c06a88-a35b-41db-b519-3e57b16d4f4b)
![Subnet 4](https://github.com/user-attachments/assets/df4339ed-ccae-4f7d-979e-13d227b6a3fd)
![Subnet 5](https://github.com/user-attachments/assets/7257bc06-6f1b-4c7c-a405-f976df293b80)
![Subnet 6](https://github.com/user-attachments/assets/63cf6e68-22f6-4c45-8012-da505c58746a)
![All Subnets](https://github.com/user-attachments/assets/228b6696-68a1-441d-893a-9a4b73926960)
<img width="1919" height="720" alt="Screenshot 2026-01-30 121954" src="https://github.com/user-attachments/assets/a8ab4ae4-b41f-497c-99fa-995b6169165b" />


---

## Step 4: Create Route Tables

Two route tables are created:

* **Public Route Table** → Has route to Internet Gateway
* **Private Route Table** → No direct internet access



![RT Creation](https://github.com/user-attachments/assets/88d2c23a-e5f0-4bef-a3d1-5d60735e3a6e)
![RT List](https://github.com/user-attachments/assets/b6558cc5-e4fb-44d2-ad1e-1a3367925c8c)

### Subnet to Route Table Mapping

**Public Route Table**

* Admin Subnet
* Edge Subnet

**Private Route Table**

* Web Subnet
* App Subnet
* Platform Subnet
* Shared Subnet



![Public RT Attach](https://github.com/user-attachments/assets/f25ab63d-0ee6-432f-997e-74681d706493)
![Public RT IGW](https://github.com/user-attachments/assets/b249ff72-8860-43b6-9b97-7a36cfea4a34)
![Private RT Attach](https://github.com/user-attachments/assets/4e1084cc-5c87-41ea-99ee-5b7709307cb2)

---

## Step 5: EC2 Instance Creation

To verify network connectivity:

* One EC2 launched in **Public (Admin) Subnet**
* One EC2 launched in **Private Subnet**

### Purpose

* Validate internet access for public subnet
* Validate isolation of private subnet



![EC2 Public](https://github.com/user-attachments/assets/64a8c7b1-49d5-4c01-ae04-82de027cc7b9)
![EC2 Private](https://github.com/user-attachments/assets/dd9f823d-62af-4ea0-b486-972c2d22b98f)
![Instances](https://github.com/user-attachments/assets/eac3a5f8-2b3f-49f8-8df4-8fa85e36b588)

---

## Step 6: Connectivity Testing

### Results

* Public EC2 → Successfully accessed via SSH and internet
* Private EC2 → No direct internet access (expected behavior)

This confirms:

* Correct routing
* Proper subnet isolation
* Secure VPC design



![Public Access](https://github.com/user-attachments/assets/f0d98c43-4bb8-4ef1-aa39-8e7a6cd8b071)
![Private Isolation](https://github.com/user-attachments/assets/5c04d9fb-9b2d-43db-81f3-c5f1fa698e82)

---

