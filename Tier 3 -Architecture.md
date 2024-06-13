The three-tier architecture is the most popular implementation of a multi-tier architecture and consists of a single presentation tier, logic tier, and data tier. The following illustration shows an example of a simple, generic three-tier application.

![image](https://github.com/AJAYKUMARREDDY7373/My-Training-Projects-Aws-/assets/154115376/4c6fd091-f577-4b7f-9c0d-e1de80f5a8bb)

Step 1: Create a VPC and Subnets as well as routing and security groups
● Go to “Your VPCs” from the VPC service on the AWS management console and click on
the orange “Create VPC” button
● Only create a vpc here and give it a name. You are free to make your own name or
follow along with the one put here

![image](https://github.com/AJAYKUMARREDDY7373/My-Training-Projects-Aws-/assets/154115376/98584029-2896-4bef-a971-8ac726f1904f)

Only create a vpc here and give it a name. You are free to make your own name or
follow along with the one put here

GIve it a 192.168.0.0/16 CIDR block and leave everything else as default. Click create.
● To create your subnets go to Subnets on the left hand side of the VPC service and click
on it
● Add your VPC ID to where it asks

![image](https://github.com/AJAYKUMARREDDY7373/My-Training-Projects-Aws-/assets/154115376/af2ac60e-5e57-4230-9935-e5ff0bf2e2e5)

![image](https://github.com/AJAYKUMARREDDY7373/My-Training-Projects-Aws-/assets/154115376/02e91c93-5daa-401f-b225-efd494aad509)

● Assign it a name letting you know what it is your first public subnet
● Put it in any availability zone and give it a CIDR of 192.168.1.0/24

![image](https://github.com/AJAYKUMARREDDY7373/My-Training-Projects-Aws-/assets/154115376/a796fbd3-d675-4385-b013-f0fd125a84f3)

● Add a second subnet and name it Private Subnet 1 or something to let you know it is
your first private subnet
● Put it in the same availability zone as the first subnet you made and give it a CIDR of
192.168.2.0/24

![image](https://github.com/AJAYKUMARREDDY7373/My-Training-Projects-Aws-/assets/154115376/960b53cc-2c7f-427c-950a-5093e0972d64)

● Add a third subnet and assign a name letting you know it is the second private subnet
you will be making
● Put it in the same availability zone as your first public subnet and give it a CIDR of
192.168.3.0/24

![image](https://github.com/AJAYKUMARREDDY7373/My-Training-Projects-Aws-/assets/154115376/4ce2627a-1f3a-4103-8b64-b84b289cf4f5)

● Add a fourth and final subnet and give it a name letting you know it is the third private
subnet
● Put it in a different availability zone from the rest of your subnets and give it a CIDR of
192.168.4.0/24

![image](https://github.com/AJAYKUMARREDDY7373/My-Training-Projects-Aws-/assets/154115376/05f983b5-c255-4053-a35e-7615c3ae9bd3)

● Set up for route tables
● Allocate an Elastic IP address by going to Elastic IPs on the left hand side and click
“Allocate Elastic IP address”

![image](https://github.com/AJAYKUMARREDDY7373/My-Training-Projects-Aws-/assets/154115376/6d6efd94-46e0-4958-b1ca-a4a506172f3f)

● Everything should be good as default but make sure that you are in the same region you
have been creating everything in and then press “Allocate”. You can also add a name
tag if you wish but it isn’t necessary

![image](https://github.com/AJAYKUMARREDDY7373/My-Training-Projects-Aws-/assets/154115376/61d93900-d730-4c8f-bbf5-b457370729ed)

● Now create an internet gateway and attach it to the VPC by going to Internet Gateways
on the left hand side and clicking “Create Internet Gateway”

![image](https://github.com/AJAYKUMARREDDY7373/My-Training-Projects-Aws-/assets/154115376/a8dcf9b9-9e3a-4f7a-af0f-6e337c62f909)

● Name it something similar to what is below and then click “Create Internet Gateway”

![image](https://github.com/AJAYKUMARREDDY7373/My-Training-Projects-Aws-/assets/154115376/e2014f45-067e-490b-8243-6e89e05119a4)

● Once it is created attach it to your VPC by clicking “Attach to a VPC” on the top of the
screen

![image](https://github.com/AJAYKUMARREDDY7373/My-Training-Projects-Aws-/assets/154115376/1beb3b06-c379-4b65-aa03-9e46cf170e0b)

● Click the drop down and select your vpc that you made

![image](https://github.com/AJAYKUMARREDDY7373/My-Training-Projects-Aws-/assets/154115376/8fb4b865-dc56-4529-978e-07b902102534)

●	Create a NAT Gateway by clicking on Nat Gateways on the left hand side and then clicking “Create NAT Gateway”

![image](https://github.com/AJAYKUMARREDDY7373/My-Training-Projects-Aws-/assets/154115376/b5437be9-6c41-4570-9400-40772ec9d151)

●	Give it a name similar to the one below and assign it to a public subnet
●	Click the drop down for Elastic IPs and click the one you created previously
●	Click “Create NAT gateway”

![image](https://github.com/AJAYKUMARREDDY7373/My-Training-Projects-Aws-/assets/154115376/c2c66f3e-14dd-41e1-b0dc-451dfa2eab00)

●	Create Route Tables by first heading to “Route Tables” on the left hand side
●	Click “Create route table”

![image](https://github.com/AJAYKUMARREDDY7373/My-Training-Projects-Aws-/assets/154115376/4b4d1c23-05eb-4ef7-b9e5-027b5dc2c1f5)

●	Give it a name letting you know this is the public route table for your lab
●	Assign your VPC to it and click “Create route table”

![image](https://github.com/AJAYKUMARREDDY7373/My-Training-Projects-Aws-/assets/154115376/df39eecd-3df9-4558-b41e-544f5730cccf)

●	Make a second route table naming it something to let you know that this is the private route table for your lab and assign your VPC to it

![image](https://github.com/AJAYKUMARREDDY7373/My-Training-Projects-Aws-/assets/154115376/537fa29a-0e16-4f5e-9499-e54c65ce2d1b)

●	Now associate your subnets with their respective route table
●	Click on the public route table and click on “Subnet association” next to “Details”

![image](https://github.com/AJAYKUMARREDDY7373/My-Training-Projects-Aws-/assets/154115376/a3fefa90-ac96-4566-a4a7-fdfe9ad61c42)

●	Click on “Edit subnet associations”

![image](https://github.com/AJAYKUMARREDDY7373/My-Training-Projects-Aws-/assets/154115376/a9c82149-9134-45e8-948c-8baa1f3dcba6)

●	Click on your public subnet and then click “Save associations”

![image](https://github.com/AJAYKUMARREDDY7373/My-Training-Projects-Aws-/assets/154115376/31d8ddbc-5f53-4b52-8e1d-1c78e0f7e4aa)

●	Now add a route to our public route table to get access to the internet gateway
●	Click on “Routes” next to “Details” and click “Edit routes”

![image](https://github.com/AJAYKUMARREDDY7373/My-Training-Projects-Aws-/assets/154115376/a6a24672-e343-41e9-a754-6483db2e2232)

●	Add a new route having a destination of anywhere and a target of your internet gateway and click “Save changes”

![image](https://github.com/AJAYKUMARREDDY7373/My-Training-Projects-Aws-/assets/154115376/05d26c4c-467f-4815-b755-6a3fffcff2b0)

●	Do the same thing for your private route table by clicking on it and going to its subnet associations and editing them

![image](https://github.com/AJAYKUMARREDDY7373/My-Training-Projects-Aws-/assets/154115376/177e3e01-3150-46a8-94a8-7ec4bb706bca)

●	Click on all three of your private subnets and save the associations
●	Go to edit the routes of the private table
●	Add a route to the private table that has a destination of anywhere and a target of your Nat gateway that you made earlier
●	Now to create our security groups (One for our bastion host, web server, app server, and our database) we will head to Security Groups on the left and click “Create security group


![image](https://github.com/AJAYKUMARREDDY7373/My-Training-Projects-Aws-/assets/154115376/4cb39012-e4dd-49eb-9af3-6e43ce008e38)

●	Give it a name and description letting you know it is for a bastion host
●	Assign your VPC to it
●	Give it three inbound rules, one for SSH using your IP and one for HTTP using 0.0.0.0/0 as well as https using 0.0.0.0/0

![image](https://github.com/AJAYKUMARREDDY7373/My-Training-Projects-Aws-/assets/154115376/9af76b92-f39b-452c-b93c-b9fb9cb69732)

●	Create another security group
●	Give it a name and description letting you know it is for a Web server
●	Assign your VPC to it
●	Give it the same inbound rules as the Bastion Host security group

![image](https://github.com/AJAYKUMARREDDY7373/My-Training-Projects-Aws-/assets/154115376/9388b40c-ebd9-48a7-8f6e-335b1fcee713)

●	Create another security group
●	Give it a name and description letting you know it is for an app server
●	Assign your VPC to it
●	Give it an inbound rule for All ICMP -IPv4 with a source of your web server SG and another inbound rule for SSH with a source of your bastion host SG

![image](https://github.com/AJAYKUMARREDDY7373/My-Training-Projects-Aws-/assets/154115376/7451f5ae-4042-4d56-8264-e66f5acae9b8)

●	Create one final security group
●	Give it a name and description letting you know it is for a database server
●	Assign your VPC to it
●	Give it two inbound rules both for MYSQL/Aurora and give one of them a source of your app server SG and the other one a source of your bastion host SG

![image](https://github.com/AJAYKUMARREDDY7373/My-Training-Projects-Aws-/assets/154115376/48447332-13d8-404a-8274-6ceec4bc9e87)

●	Go back to your bastion host inbound rules and add one more for MYSQL/Aurora and a source of your database SG
●	Go back to your web server inbound rules and add one more for All ICMP - IPv4 and a source of your app server SG
●	Go back to your app server inbound rules and add one more for MYSQL/Aurora and a source of your database SG and then an HTTP and HTTPS rule both with a source of 0.0.0.0/0 

**Step 2**: Create Servers
●	Create Bastion Host
●	Select Amazon Linux 2 AMI
●	Select t2.micro
●	Put in your VPC and Public Subnet and enable auto assign public IP
●	Launch and choose an existing keypair. This can be downloaded from the lab page
●	To make the Web Server follow the same steps until you get to Step 3
●	Follow along like previously and change your network, subnet, and enable auto assign public ip
●	Then go to user data and type this into it to set up the web server

" ○	#!/bin/bash
○	sudo yum update -y
○	sudo amazon-linux-extras install -y lamp-mariadb10.2-php7.2 php7.2
○	Sudo yum install -y httpd
○	sudo systemctl start httpd
○	sudo systemctl enable httpd "

![image](https://github.com/AJAYKUMARREDDY7373/My-Training-Projects-Aws-/assets/154115376/6356939f-0020-472c-b32e-0cf19695a697)

●	Storage leave default
●	Give it a name tag letting you know it is the Web Server
●	Select an existing security group and select your web server SG
●	Just like before launch and use the existing keypair
![image](https://github.com/AJAYKUMARREDDY7373/My-Training-Projects-Aws-/assets/154115376/7238f74d-977f-43ad-af14-62ccb02a28e2)

●	Follow the same steps once again to create the app server until you get to step 3
●	Put in your VPC and then choose Private Subnet 1 for the subnet and leave auto assign public ip disabled
●	Then go into metadata and type this out to set up a database server on our app server
○ "	#!/bin/bash
○	sudo yum install -y mariadb-server
○	Sudo service mariadb start (note that the image is incorrect, make sure to add sudo) "

![image](https://github.com/AJAYKUMARREDDY7373/My-Training-Projects-Aws-/assets/154115376/497862f2-29c0-4e0d-80a7-a9bef2201278)

●	Select an existing security group and select the app server SG
●	Just like before launch and use the existing keypair

**Step 3**: Create a Database
●	Create a DB subnet group by first heading to the Amazon RDS service page on the AWS management console
●	Click on Subnet Groups on the left hand side and the click on “Create DB subnet group”

![image](https://github.com/AJAYKUMARREDDY7373/My-Training-Projects-Aws-/assets/154115376/52e232fe-4943-47bb-b471-1c38c2d877ac)

●	Give it a name and description letting you know what it is and then assign your VPC to it
●	Put in the availability zones you used for your subnets
●	Select subnets 3 and 4

![image](https://github.com/AJAYKUMARREDDY7373/My-Training-Projects-Aws-/assets/154115376/b5ff24d2-1798-47b9-ad50-c22c1423ad1e)

●	Go to Databases on the left hand side and click on “Create Database”

![image](https://github.com/AJAYKUMARREDDY7373/My-Training-Projects-Aws-/assets/154115376/c1d2a11b-b950-4655-95ba-981732507055)

●	Click on Standard create and MariaDB for the engine type

![image](https://github.com/AJAYKUMARREDDY7373/My-Training-Projects-Aws-/assets/154115376/ee0cc038-91c7-4277-a5c7-dcffa6022fb8)

●	Make sure you click on Free tier here

![image](https://github.com/AJAYKUMARREDDY7373/My-Training-Projects-Aws-/assets/154115376/5cabdb21-e794-40a5-9671-6bdadeef321d)

●	Give it an identifier you can easily identify it with
●	Give it a master username or leave it as default admin. For the purpose of these instructions I will be using root
●	Give it a password that you write down somewhere else to make sure you have the correct one. For the purpose of these instructions I will be using Re:Start!9

![image](https://github.com/AJAYKUMARREDDY7373/My-Training-Projects-Aws-/assets/154115376/3ea7cb83-110a-4e68-aef9-7f36b04f64ea)

●	Everything between this and the last step is left default
●	Assign your vpc
●	Make sure your subnet group is listed under the subnet group section
●	Public access is no
●	Choose existing VPC security groups
●	Remove the default security group and add your database security group
●	Select your first availability zone as well

![image](https://github.com/AJAYKUMARREDDY7373/My-Training-Projects-Aws-/assets/154115376/0072beb3-8216-4ea3-9405-da404bc90e42)
![image](https://github.com/AJAYKUMARREDDY7373/My-Training-Projects-Aws-/assets/154115376/c0c75cb3-50c4-456f-a89e-d20e0602723f)

●	Scroll down to Additional configuration on the bottom and give it an initial database name and save it in the same spot as your password since it will be used later
●	Disable automated backups and encryption since they are not needed (These are normally best practice to leave enabled but the database will spin up faster with those checked off as they are not needed).
●	Scroll down all the way to the bottom and create your database

![image](https://github.com/AJAYKUMARREDDY7373/My-Training-Projects-Aws-/assets/154115376/a82738ec-8a17-43be-9da3-074e8a273061)

**Step 4**: Test connections -------> Use Existing Pem or Ppk file , create newone

![image](https://github.com/AJAYKUMARREDDY7373/My-Training-Projects-Aws-/assets/154115376/b96ca86d-ce83-4b16-a602-0ea9a288ba92)

●	This is for windows only as I only have a windows machine to work on, sorry mac and linux users
●	Go into your powershell and type this command out
○	Pscp -scp -P 22 -i ’.\Downloads\labsuser.ppk’ -| user ec2-user ‘.\Downloads\labsuser.pem’ ec2-user@bastion-host-public-ip:/home/ec2-user 
○	Replace bastion-host-public-ip with the public ip address of your bastion host
●	Hit enter and it should upload those keys to your bastion host for use on other servers

![image](https://github.com/AJAYKUMARREDDY7373/My-Training-Projects-Aws-/assets/154115376/a6aa4658-5923-436f-8ce2-5e425ce627cf)

●	Test on your ssh to see if the file is uploaded by using ls. Should return something like this

●	Change file permissions for the file we just downloaded to our bastion host by typing
○	chmod 400 labsuser.pem
●	Then ssh into our app server by typing
○	ssh -i my-key-pair.pem ec2-user@app-server-private-ip
○	Replace my-key-pair with the name of your key
○	Replace app-server-private-ip with your app server’s private ip address
●	Type yes when it prompts you to
●	Use ls to see that you are now ssh into a different server since there is no more key

![image](https://github.com/AJAYKUMARREDDY7373/My-Training-Projects-Aws-/assets/154115376/4f5605e9-7b13-4a91-8fd4-ac6d5516698f)

●	Use ping and the private ip address of your web server to ping the web server and see it connect

![image](https://github.com/AJAYKUMARREDDY7373/My-Training-Projects-Aws-/assets/154115376/1c1fd30c-7316-4517-9f66-b47bf0cae01b)

●	Test out connecting to the database by typing out mysql –user=root -password=’Re:Start!9’ –host=database-server-endpoint
●	Replace database-server-endpoint with the database server endpoint 
●	Type show databases; to see your database from the app server

![image](https://github.com/AJAYKUMARREDDY7373/My-Training-Projects-Aws-/assets/154115376/bec280c8-6b01-4be4-b5de-29cf45759c44)

![image](https://github.com/AJAYKUMARREDDY7373/My-Training-Projects-Aws-/assets/154115376/a9b9409e-e7fd-4a93-af87-b85711285a7e)

Source : AWS/Restart

























































