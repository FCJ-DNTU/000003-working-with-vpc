---
title : "Create Security Group"
date : "`r Sys.Date()`"
weight : 5
chapter : false
pre : " <b> 3.5 </b> "
---

## Create Security Groups

### Create Security Group for Servers in Public Subnet

1. In the **VPC** interface:
    - Select **Security Group**
    - Select **Create security group**

![Create VPC](/images/3-Preparation-steps-update/5-Security-Group/SG-1.png?featherlight=false&width=60pc)

2. Configure the **Security Group**:
    - **Security Group name**: Enter **Public subnet - SG**
    - **Description**: Enter **Allow SSH and Ping for servers in the public subnet.**
    - Select the **ASG** VPC

![Create VPC](/images/3-Preparation-steps-update/5-Security-Group/SG-2.png?featherlight=false&width=60pc)

3. Configure **Inbound rules**:
    - In **Inbound rules**, click **Add rule**.
    - Select **Type**: **SSH** and **Source**: **My IP**. (Use your public IPv4 address)
    - Select **Add rule** to add a new rule.
    - Select **Type**: **All ICMP - IPv4** and **Source**: **Anywhere**. Allow ping from any IP address.

![Create VPC](/images/3-Preparation-steps-update/5-Security-Group/SG-3.png?featherlight=false&width=60pc)

4. Check **Outbound rules** and select **Create security group**

![Create VPC](/images/3-Preparation-steps-update/5-Security-Group/SG-4.png?featherlight=false&width=60pc)

5. Complete the creation of the security group for the server located in the public subnet

![Create VPC](/images/3-Preparation-steps-update/5-Security-Group/SG-5.png?featherlight=false&width=60pc)

### Create a Security Group for a Server in a Private Subnet

6. In the **VPC** interface:
    - Select **Security Groups**
    - Select **Create security group**

![Create VPC](/images/3-Preparation-steps-update/5-Security-Group/SG-6.png?featherlight=false&width=60pc)

7. Configure the **Security Group**:
    - In the **Security group name** field, enter **Private subnet - SG**
    - In the **Description** section, enter **Allow SSH and Ping for servers in the private subnet.**
    - Select the **VPC** named **ASG**

![Create VPC](/images/3-Preparation-steps-update/5-Security-Group/SG-7.png?featherlight=false&width=60pc)

8. Configure **Inbound rules**:
    - In **Inbound rules**, select **Add rule**.
    - Select **Type**: **SSH** and leave **Source**: **Custom**. Search and select **Public subnet SG** to allow SSH from servers in the public subnet.
    
![Create VPC](/images/3-Preparation-steps-update/5-Security-Group/SG-8.png?featherlight=false&width=60pc)

9. Select **Add rule** to add a new rule:
    - Select **Type**: **All ICMP IPv4** and **Source**: **Anywhere**. Allow ping from any IP address.

![Create VPC](/images/3-Preparation-steps-update/5-Security-Group/SG-9.png?featherlight=false&width=60pc)

10. Select **Create security group**

![Create VPC](/images/3-Preparation-steps-update/5-Security-Group/SG-10.png?featherlight=false&width=60pc)

11. Two **Security Groups** have been created for servers located in the public and private subnets:
    - Next, we will proceed to create two EC2 servers.

![Create VPC](/images/3-Preparation-steps-update/5-Security-Group/SG-11.png?featherlight=false&width=60pc)
