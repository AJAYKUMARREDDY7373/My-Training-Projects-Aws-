Creating a Website on S3



Create an Amazon Simple Storage Service (Amazon S3) bucket.

Create a new AWS Identity and Access Management (IAM) user that has full access to the Amazon S3 service.

Upload files to Amazon S3 to host a simple website for the Café & Bakery.

Create a batch file that can be used to update the static website when you change any of the website files locally.

![image](https://github.com/AJAYKUMARREDDY7373/My-Training-Projects-Aws-/assets/154115376/05274e43-afee-424d-b2d9-99e0c6d61e71)

***Objectives***

Run AWS CLI commands that use IAM and Amazon S3 services.

Deploy a static website to an S3 bucket.

Create a script that uses the AWS CLI to copy files in a local directory to Amazon S3.

Step 1: Connect to an Amazon Linux EC2 instance using SSM

Run the following commands to change the user and home directory:

![image](https://github.com/AJAYKUMARREDDY7373/My-Training-Projects-Aws-/assets/154115376/8714e8e9-23ba-440c-9820-be9a20333895)

Step 2: Configure the AWS CLI Unlike some other Linux distributions that are available through Amazon Web Services (AWS), Amazon Linux instances already have the AWS CLI pre-installed on them.

![image](https://github.com/AJAYKUMARREDDY7373/My-Training-Projects-Aws-/assets/154115376/01ac127c-c007-4adc-a7bd-dd9214dc79b9)

AWS Access Key ID: Copy and paste the value for AccessKey from my notes or where you you saved

AWS Secret Access Key: Copy and paste the value for SecretKey from my notes or where you you saved

Default region name: Enter ap-south-1

Default output format: Enter json

Step 3: Create an S3 bucket using the AWS CLI

When you create a new S3 bucket, the bucket must have a unique name, such as the combination of your first initial, last name, and three random numbers. For example, if a user's name is Terry Whitlock, a bucket name could be twhitlock256

To create a bucket in Amazon S3, you use the aws s3api create-bucket command. When you use this command to create an S3 bucket, you also include the following:

Specify --region ap-south-1

Add --create-bucket-configuration LocationConstraint=ap-south-1 to the end of the command.

The following command is to create a new S3 bucket

aws s3api create-bucket --bucket Kaminopg123 --region us-west-2 --create-bucket-configuration LocationConstraint=us-west-2 ansd output in json (sucessful bucket creation)

Step 4: Create a new IAM user that has full access to Amazon S3

Using the AWS CLI, create a new IAM user with the command aws iam create-user and username awsS3user

![image](https://github.com/AJAYKUMARREDDY7373/My-Training-Projects-Aws-/assets/154115376/a9206932-2d7f-4d99-ab1c-2dfe259c4b3a)

Create a login profile for the new user by using the following command:

![image](https://github.com/AJAYKUMARREDDY7373/My-Training-Projects-Aws-/assets/154115376/1c084c25-a8c8-46f0-8636-db57321f8ee0)

Copy the 12 digit Account ID number.

In the current drop down menu, choose Sign Out.

Log in to the AWS Management Console as the new awsS3user user:

In the browser tab where you just signed out of the AWS Management Console, choose Log back in or Sign in to the Console.

In the sign-in screen, choose the radio button IAM user.

In the text field, paste or enter the account ID with no dashes.

Choose Next.

A new login screen with Sign in as IAM user field will show. The account ID will be filled in from the previous screen.

For IAM user name, enter awsS3user

For Password, enter Training123!

Choose Sign In

On the AWS Management Console, in the Search box, enter S3 and choose S3. This option takes you to the Amazon S3 console page.

![image](https://github.com/AJAYKUMARREDDY7373/My-Training-Projects-Aws-/assets/154115376/9a17c565-aecf-4cb3-b7ff-3eaadfc2083d)

Note: The bucket that you created might not be visible. Refresh the Amazon S3 console page to see if it appears. The awsS3user user does not have Amazon S3 access to the bucket that you created, so you might see an error for Access to this bucket.

In the terminal window, to find the AWS managed policy that grants full access to Amazon S3, run the following command:

![image](https://github.com/AJAYKUMARREDDY7373/My-Training-Projects-Aws-/assets/154115376/61a7b583-c530-400b-951b-113f415ee1a4)

The result displays policies that have a PolicyName attribute containing the term S3. Locate the policy that grants full access to Amazon S3. You use this policy in the next step.

To grant the awsS3user user full access to the S3 bucket, replace in following command with the appropriate PolicyName from the results, and run the adjusted command:

![image](https://github.com/AJAYKUMARREDDY7373/My-Training-Projects-Aws-/assets/154115376/5efbbf21-3ef7-4066-89e3-1f7e8f14bb90)

Return to the AWS Management Console, and refresh the browser tab.

Step 5: Adjust S3 bucket permissions On the AWS Management Console, on the Amazon S3 console, choose your bucket name.

Go to permissions, under Block public access (bucket settings), choose Edit

DeSelect/UnSelect Block all public access

Choose Save changes (confirm on the prompt)

On to permissions tab, under Object Ownership, choose Edit

Choose ACLs enabled

Choose I acknowledge that ACLs will be restored.

Choose Save changes

Step 6: Extract the files that you need for this lab A file containing the static-website contents for the Amazon S3 bucket will need to be extracted in the following step.

Back in the SSH terminal, extract the files that you need for this lab by running the following commands:

![image](https://github.com/AJAYKUMARREDDY7373/My-Training-Projects-Aws-/assets/154115376/bd9975e8-5e82-4400-9370-37426acac5b5)

To confirm that the files were extracted correctly, run the ls command.

Step 7: Upload files to Amazon S3 by using the AWS CLI Once the files are extracted, you upload the contents of the file to Amazon S3. These files include what you explored when you ran the ls command.

So that the bucket can function as a website, replace in the following command with your bucket name, and run the adjusted command.

![image](https://github.com/AJAYKUMARREDDY7373/My-Training-Projects-Aws-/assets/154115376/ac7b321f-55a4-45d5-a613-55352e1ac16f)

This process helps ensure that the index.html file will be known as the index document.

To upload the files to the bucket, replace in the following command with your bucket name, and run the adjusted command:

![image](https://github.com/AJAYKUMARREDDY7373/My-Training-Projects-Aws-/assets/154115376/6bfa94a8-3253-4e0d-8c08-3e20405e086c)

To verify that the files were uploaded, replace in the following command with your bucket name, and run the adjusted command:

![image](https://github.com/AJAYKUMARREDDY7373/My-Training-Projects-Aws-/assets/154115376/7aa133b1-01ed-4504-8b34-fe3f1cb1e7b6)

On the AWS Management Console, on the Amazon S3 console, choose your bucket name.

Choose the Properties tab. At the bottom of the this tab, note that Static website hosting is Enabled. Running the aws s3 website AWS CLI command turns on the static website hosting for an Amazon S3 bucket. This option is usually turned off by default.

To open the URL on a new page, choose the Bucket website endpoint URL that displays.

Task 8: Create a batch file to make updating the website repeatable To create a repeatable deployment, you create a batch file by using the VI editor.

Locate the line where you ran the aws s3 cp command. You will put this line in your new batch file.

To change directories and create an empty file, run the following command in the SSH terminal session:

![image](https://github.com/AJAYKUMARREDDY7373/My-Training-Projects-Aws-/assets/154115376/6bc3a75f-3141-4038-80ad-02feb89df796)

To open the empty file in the VI editor, run the following command.

![image](https://github.com/AJAYKUMARREDDY7373/My-Training-Projects-Aws-/assets/154115376/44a8954a-5ad6-451e-bb7b-95a1e9c3b442)

To enter edit mode in the VI editor, press i

Next, you add the standard first line of a bash file and then add the s3 cp line from your history. To do so, replace in the following command with your bucket name, and copy and paste the adjusted command into your file:

![image](https://github.com/AJAYKUMARREDDY7373/My-Training-Projects-Aws-/assets/154115376/9c48c8c3-b9a8-4821-8581-4803cc01d97e)

To write the changes and quit the file, press Esc, enter :wq and then press Enter.

To make the file an executable batch file, run the following command:

![image](https://github.com/AJAYKUMARREDDY7373/My-Training-Projects-Aws-/assets/154115376/206032de-f342-42c7-a141-e1bb1ac5077b)

S3 static website(Cafe) .......

![image](https://github.com/AJAYKUMARREDDY7373/My-Training-Projects-Aws-/assets/154115376/7640c14c-bab1-47c9-bd1d-4c92d98a5af9)

Step 9: Clean up

created your static website only as a learning exercise, delete the AWS resources that you allocated so that you no longer accrue charges. After you delete your AWS resources, your website is no longer available.

Source : @ Aws/Restart














