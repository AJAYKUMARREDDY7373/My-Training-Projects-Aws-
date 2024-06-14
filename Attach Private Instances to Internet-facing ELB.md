  How do I attach backend instances with private IP addresses to my internet-facing load balancer in ELB.

  Network Topology - ALB in private subnet

  ![image](https://github.com/AJAYKUMARREDDY7373/My-Training-Projects-Aws-/assets/154115376/96f900f6-b364-4bba-9500-c9f702841127)

  Open the Amazon VPC console

  ![image](https://github.com/AJAYKUMARREDDY7373/My-Training-Projects-Aws-/assets/154115376/2fdb0547-23f4-4e90-85b6-6e3eb6c9ccf5)

  In the navigation pane, choose Your VPCs, Create VPC.

  ![image](https://github.com/AJAYKUMARREDDY7373/My-Training-Projects-Aws-/assets/154115376/e3328b8c-e3d8-49c5-9ed4-9b8bc575c45e)

  Under Resources to create, choose VPC only.
 
 ![image](https://github.com/AJAYKUMARREDDY7373/My-Training-Projects-Aws-/assets/154115376/63ecc63f-193c-4c62-965b-7db95d1b886f)

 Specify the following VPC details as needed.

![image](https://github.com/AJAYKUMARREDDY7373/My-Training-Projects-Aws-/assets/154115376/5c18ff5a-d5e1-4a0e-94bc-a890653eb63f)

o Name
o IPv4 CIDR block - for example, 10.0.0.0/16, or 192.168.0.0/16
 Tenancy: Choose the tenancy option for this VPC. (Should go with Default)
o Select Default to ensure that EC2 instances launched in this VPC use the EC2 instance
tenancy attribute specified when the EC2 instance is launched.
o Select Dedicated to ensure that EC2 instances launched in this VPC are run on tenancy
instances regardless of the tenancy attribute specified at launch.
o Choose Create VPC

*****************************************************************

To create a Subnet
 In the navigation pane, choose Subnets. Then choose Create Subnet.

![image](https://github.com/AJAYKUMARREDDY7373/My-Training-Projects-Aws-/assets/154115376/832eacaa-06a6-41a2-acd9-3b6ff982641c)

 In the Create Subnet dialog box, do the following:
o Name (private-subnet)
o For VPC, choose the VPC that you created previously.
o For Availability Zone, choose the first Availability Zone in the list.
o For CIDR block, type the CIDR block to use for the subnet. If you used the default values
for the VPC in the previous procedure, then type  192.168.1.0/28.
o Choose Yes, Create.
 Repeat above steps to create subnets for each remaining Availability Zone in the region. For the
subnet CIDR blocks, you can use  192.168.2.0/28., 192.168.3.0/28., and soon.

![image](https://github.com/AJAYKUMARREDDY7373/My-Training-Projects-Aws-/assets/154115376/03ca907a-0213-42be-aee8-0454f97ff1ea)


*******************************************************************

To create Security group

Choose Create security group.

![image](https://github.com/AJAYKUMARREDDY7373/My-Training-Projects-Aws-/assets/154115376/aa357d63-49ec-43a2-b886-f1b4e6be4b60)

Enter a name and description for the security group. You cannot change the name and description of a
security group after it is created.
From VPC, choose the VPC (created in above step )
You can add security group rules, or you can add them later.
For Inbound rules, create rules that allow specific traffic to reach your instance
 Choose Add rule. For Type, choose HTTP. For Source, choose Anywhere.
 Choose Add rule. For Type, choose SSH. For Source, choose Anywhere

![image](https://github.com/AJAYKUMARREDDY7373/My-Training-Projects-Aws-/assets/154115376/595fe23f-92de-451e-97f6-8330aee77a31)

For Outbound rules, keep the default rule, which allows all outbound traffic.
Choose Create security group

![image](https://github.com/AJAYKUMARREDDY7373/My-Training-Projects-Aws-/assets/154115376/47e373b8-44ef-41cd-806e-4efb3c05607f)


*********************************************************************

To create EC2 machines
Create Keypair first
Open the Amazon EC2 console 
In the navigation pane, choose Key Pairs.
Choose Create key pair.

![image](https://github.com/AJAYKUMARREDDY7373/My-Training-Projects-Aws-/assets/154115376/5b163499-cf02-4491-90a8-0ee173918d03)

For Name, enter a descriptive name for the key pair.
For Key pair type, choose either RSA or ED25519.
Note that ED25519 keys are not supported for Windows instances, EC2 Instance Connect, or EC2
Serial Console.

![image](https://github.com/AJAYKUMARREDDY7373/My-Training-Projects-Aws-/assets/154115376/01d31fbf-e422-4ed1-9121-2a5286772550)

For Private key file format, choose the format in which to save the private key.
To save the private key in a format that can be used with OpenSSH, choose pem.
To save the private key in a format that can be used with PuTTY, choose ppk.
Choose Create key pair.
The private key file is automatically downloaded by your browser. The base file name is the name
you specified as the name of your key pair, and the file name extension is determined by the file
format you chose. Save the private key file in a safe place.
Important –
This is the only chance for you to save the private key file.
If you will use an SSH client on a macOS or Linux computer to connect to your Linux instance,
use the following command to set the permissions of your private key file so that only you can
read it.
**chmod 400 my-key-pair.pem**

*****************************************************************

choose Launch Instance.
The Choose an Amazon Machine Image (AMI) – Select Linux AMI 2
On the Choose an Instance Type page - Select the t2.micro instance type, which is selected by default
On the Configure Instance page -
In Number of instances – change it to 2

![image](https://github.com/AJAYKUMARREDDY7373/My-Training-Projects-Aws-/assets/154115376/a3e160af-e47c-43c7-afa2-503b1de8cb49)

In the Network section – Select VPC – select Subnet (private subnet create in above step)
Go with default setting in ADD Storage tab
Under Security Groups – select the security group created in above step
On the Review Instance Launch page, choose Launch.
When prompted for a key pair, select choose an existing key pair (select the key pair created in above
step)
Auto-assign Public IP – Disabled

![image](https://github.com/AJAYKUMARREDDY7373/My-Training-Projects-Aws-/assets/154115376/ea99bab4-ac7b-489c-b0cb-df8f8285aa35)

Scroll down to the last and select user data – select as text – enter the below script to install Apache
web server at startup

**#!/bin/bash
yum install httpd -y
service httpd start
chkconfig httpd on
echo "Sample Content " > /var/www/html/index.html**  

![image](https://github.com/AJAYKUMARREDDY7373/My-Training-Projects-Aws-/assets/154115376/e0c96c5d-b591-43c6-bfdb-650d4d567ae0)

Choose Launch Instance

********************************************************************

Step to create NAT Gateway
Open the Amazon VPC console 
Choose NAT Gateways.

![image](https://github.com/AJAYKUMARREDDY7373/My-Training-Projects-Aws-/assets/154115376/4301efcd-eb2f-4fac-93fd-9e80d2f926ab)

. (Optional) Specify a name for the NAT gateway. This creates a tag where the key
is Name and the value is the name that you specify.
2. Select the subnet in which to create the NAT gateway.
3. For Connectivity type, select Private to create a private NAT gateway or Public (the
default) to create a public NAT gateway.
4. (Public NAT gateway only) For Elastic IP allocation ID, select an Elastic IP address to
associate with the NAT gateway.
5. (Optional) For each tag, choose Add new tag and enter the key name and value.
6. Choose Create a NAT Gateway.

*************************************************************************
Steps to create IGW

Open the Amazon VPC console

![image](https://github.com/AJAYKUMARREDDY7373/My-Training-Projects-Aws-/assets/154115376/4d891be2-84a2-41fe-814f-6a19d3cb0ab3)


In the navigation pane, choose Internet Gateways, and then choose Create internet gateway.
Optionally name your internet gateway.
Choose Create internet gateway.
Select the internet gateway that you just created, and then choose Actions, Attach to VPC.

![image](https://github.com/AJAYKUMARREDDY7373/My-Training-Projects-Aws-/assets/154115376/f24dbf25-6023-4eaa-b385-4e561edf3306)

Select your VPC from the list, and then choose Attach internet gateway.

![image](https://github.com/AJAYKUMARREDDY7373/My-Training-Projects-Aws-/assets/154115376/c6dd3176-39e1-419e-90af-0f710b6bdaab)

Internet gateway  successfully attached to  vpc 

![image](https://github.com/AJAYKUMARREDDY7373/My-Training-Projects-Aws-/assets/154115376/ad48d838-eda2-4d93-9734-251aaaa353ee)

*****************************************************************

Step to create Route Table

![image](https://github.com/AJAYKUMARREDDY7373/My-Training-Projects-Aws-/assets/154115376/4a98794b-8527-421e-975f-c8be8651e51f)

For Name tag, enter a name for your route table.
For VPC, choose your VPC.
Choose Create.

*********************************************************

Step to create Load Balancer
Open the Amazon EC2 console.
Select Classic Load Balancer

![image](https://github.com/AJAYKUMARREDDY7373/My-Training-Projects-Aws-/assets/154115376/f7c33b12-331a-4ad2-bfc3-ed0d279938cd)

Select the VPC and than Associate the public subnets with your load

![image](https://github.com/AJAYKUMARREDDY7373/My-Training-Projects-Aws-/assets/154115376/e237f7e5-15f1-4865-a8d4-e0ec3742975f)

Register the backend instances (created in private subnet ) with your load balancer
Select Security group ( created in above step )

![image](https://github.com/AJAYKUMARREDDY7373/My-Training-Projects-Aws-/assets/154115376/b29a708e-803d-447f-bdde-565dd01dd0ac)

![image](https://github.com/AJAYKUMARREDDY7373/My-Training-Projects-Aws-/assets/154115376/877b0034-9e36-48a5-874b-58dd4c29a2fc)

![image](https://github.com/AJAYKUMARREDDY7373/My-Training-Projects-Aws-/assets/154115376/69d08f80-2ebb-4046-b11a-3e85eda56aab)

Create LoadBalancer

Test with DNS Name























