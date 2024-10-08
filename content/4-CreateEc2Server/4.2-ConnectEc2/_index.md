---
title : "Test Connection"
date : "`r Sys.Date()`"
weight : 2
chapter : false
pre : " <b> 4.2 </b> "
---

## Checking Connection

{{% notice note %}}
 There are several ways to connect to EC2 instances. You can follow the instructions to [connect to EC2 using PuTTY](https://000004.awsstudygroup.com/en/4-launchlinuxinstance/4.2-connectlinuxinstance/). In this lab, we will use [Visual Studio Code](https://code.visualstudio.com/download) to establish the connection.
 {{% /notice %}}


1. **Download Visual Studio Code**
   - [Visual Studio Code](https://code.visualstudio.com/download)
  
   ![Create VPC](/images/4-CreateEc2Server-update/2-Test-Connection/Connect-img1.png?featherlight=false&width=60pc)

2. Access the **EC2** page

   - Select **Instances**
   - Select **EC2 Public**
   - Select **Connect**


   ![Create VPC](/images/4-CreateEc2Server-update/2-Test-Connection/Connect-img2.png?featherlight=false&width=60pc)

3. In the **Connect** section

   - Select **SSH Client**
   - Copy the code in the **Example** section

   ![Create VPC](/images/4-CreateEc2Server-update/2-Test-Connection/Connect-3.png?featherlight=false&width=60pc)

4. In the **Visual Studio Code** interface

   - Download **SSH**

   ![Create VPC](/images/4-CreateEc2Server-update/2-Test-Connection/Connect-img4.png?featherlight=false&width=60pc)

5. In the **Visual Studio Code** search bar

   - Follow the instructions to connect via **SSH**

   ![Create VPC](/images/4-CreateEc2Server-update/2-Test-Connection/Connect-img5.png?featherlight=false&width=60pc)

   ![Create VPC](/images/4-CreateEc2Server-update/2-Test-Connection/Connect-img6.png?featherlight=false&width=60pc)

   ![Create VPC](/images/4-CreateEc2Server-update/2-Test-Connection/Connect-img7.png?featherlight=false&width=60pc)

6. Configure **SSH**.
   - Paste the copied path from **EC2 Public** here
   - Edit the **key pair** path to point to the correct file location
   - Save the file
  
   ![Create VPC](/images/4-CreateEc2Server-update/2-Test-Connection/Connect-6.png?featherlight=false&width=60pc)

7. Connect via **SSH**.
   - Re-run the commands in the search bar as shown above
   - Search for and select the **IP public EC2** to connect
  
   ![Create VPC](/images/4-CreateEc2Server-update/2-Test-Connection/Connect-7.png?featherlight=false&width=60pc)

   ![Create VPC](/images/4-CreateEc2Server-update/2-Test-Connection/Connect-8.png?featherlight=false&width=60pc)


8. Test the internet connection of EC2 Public by running the command:

   ```
   ping amazon.com -c5
   ```

   ![Create VPC](/images/4-CreateEc2Server-update/2-Test-Connection/Connect-9.png?featherlight=false&width=60pc)



## Connect to the EC2 Private Server and Check Internet Connection

9. Access to **EC2**

   - Select **Instances**
   - Select **EC2 Private**
   - Select **Details**
   - Select **Private IPv4 addresses**
   - Then connect SSH to **EC2 Public**

   ![Create VPC](/images/4-CreateEc2Server-update/2-Test-Connection/Connect-10.png?featherlight=false&width=60pc)

10. Perform a ping test to the EC2 Private's private IP address to test the connection from the EC2 Public server to the EC2 Private server. Use the following command:


```
ping <IP Private EC2 Private> -c5
```
   ![Create VPC](/images/4-CreateEc2Server-update/2-Test-Connection/Connect-11.png?featherlight=false&width=60pc)

11. **EC2 Private** will not have a **public IP address** because we are not assigning this server a public IP. To be able to ssh into **EC2 Private**, we will make an ssh connection from EC2 Public through EC2 Private **private IP address**

     - Download the **pscp** tool to the same folder containing the **aws-keypair.ppk** file to copy the **aws-keypair.pem** file from our computer to **EC2 Public** .

{{% notice info %}}
You download [an RSA and DSA key generation utility](https://the.earth.li/~sgtatham/putty/latest/w64/puttygen.exe) as **puttygen.exe**
{{% /notice %}}

{{% notice info %}}
You download [an SCP client, i.e. command-line secure file copy](https://the.earth.li/~sgtatham/putty/latest/w64/pscp.exe) is **pscp.exe**
{{% /notice %}}

12. We use **puttygen.exe** to generate key

     - Select **Load**

   ![Create VPC](/images/4-CreateEc2Server-update/2-Test-Connection/Connect-img12.png?featherlight=false&width=60pc)

13. Select **aws-keypair.pem**

     - Select **OK**
     - Select **Save private key** with the name **aws-keypair.ppk**

   ![Create VPC](/images/4-CreateEc2Server-update/2-Test-Connection/Connect-img13.png?featherlight=false&width=60pc)

14. Complete the generation key

   ![Create VPC](/images/4-CreateEc2Server-update/2-Test-Connection/Connect-img14.png?featherlight=false&width=60pc)

15. Launch **Command Prompt**. Change the path to the folder you just downloaded **pscp**. Run the command below to upload the **aws-keypair.pem** file to the **/home/ec2-user/** directory of the EC2 Public server.

    - You will need to replace the **public IP address of EC2 Public** parameter before running the command.

```
pscp -i aws-keypair.ppk aws-keypair.pem ec2-user@<EC2 PUBLIC public IP address>:/home/ec2-user/
```

   ![Create VPC](/images/4-CreateEc2Server-update/2-Test-Connection/Connect-15.png?featherlight=false&width=60pc)

16. Access to **EC2**

     - Select **Instances**
     - Select **EC2 Public**
     - Select **Details**
     - View **Public IPv4 address**

   ![Create VPC](/images/4-CreateEc2Server-update/2-Test-Connection/Connect-16.png?featherlight=false&width=60pc)

17. Return to the EC2 connection interface. Make sure you copy the **aws-keypair.pem** file to the **EC2 Public** server, we execute the command

```
ls
```

   ![Create VPC](/images/4-CreateEc2Server-update/2-Test-Connection/Connect-17.png?featherlight=false&width=60pc)

18. Update the permissions for the **aws-keypair.pem** file by running the **chmod 400 aws-keypair.pem** command. AWS requires the key pair file to be restricted before it can be used to connect to the EC2 server.

```
chmod 400 aws-keypair.pem
```
   ![Create VPC](/images/4-CreateEc2Server-update/2-Test-Connection/Connect-18.png?featherlight=false&width=60pc)

19. **SSH** to **EC2 Private** server

```
ssh -i aws-keypair.pem ec2-user@<EC2 Private server's private IP address>
```

   ![Create VPC](/images/4-CreateEc2Server-update/2-Test-Connection/Connect-19.png?featherlight=false&width=60pc)

20. Perform **ping test to amazon.com**. As you can see, we cannot connect **internet from EC2 Private**. In the next step, we will create **NAT Gateway** to allow the **EC2 Private** server to connect to the internet in the outbound direction. Keep the connection to **EC2 Private** so that we can check the connection to **internet** after finishing creating and configuring **NAT Gateway**.

```
ping amazon.com
```

   ![Create VPC](/images/4-CreateEc2Server-update/2-Test-Connection/Connect-20.png?featherlight=false&width=60pc)
