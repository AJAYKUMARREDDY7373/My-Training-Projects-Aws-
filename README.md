Creating a Website on S3

Create an Amazon Simple Storage Service (Amazon S3) bucket.

Create a new AWS Identity and Access Management (IAM) user that has full access to the Amazon S3 service.

Upload files to Amazon S3 to host a simple website for the Café & Bakery.

Create a batch file that can be used to update the static website when you change any of the website files locally.

![image](https://github.com/AJAYKUMARREDDY7373/My-Training-Projects-Aws-/assets/154115376/a874a474-5393-443b-ab49-3d5a842cf009)

Objectives


Run AWS CLI commands that use IAM and Amazon S3 services.

Deploy a static website to an S3 bucket.

Create a script that uses the AWS CLI to copy files in a local directory to Amazon S3.

Step 1: Connect to an Amazon Linux EC2 instance using SSM

Run the following commands to change the user and home directory:

![image](https://github.com/AJAYKUMARREDDY7373/My-Training-Projects-Aws-/assets/154115376/33fb96c3-9d3c-4da0-ac92-5b92420e908f)

Step 2: Configure the AWS CLI
Unlike some other Linux distributions that are available through Amazon Web Services (AWS), Amazon Linux instances already have the AWS CLI pre-installed on them.

![image](https://github.com/AJAYKUMARREDDY7373/My-Training-Projects-Aws-/assets/154115376/b023b845-e901-4a87-9f20-9c43c6a1bf53)

AWS Access Key ID: Copy and paste the value for AccessKey from my notes or where you you saved

AWS Secret Access Key: Copy and paste the value for SecretKey from my notes or where you you saved

Default region name: Enter ap-south-1

Default output format: Enter json

Step 3: Create an S3 bucket using the AWS CLI

When you create a new S3 bucket, the bucket must have a unique name, such as the combination of your first initial, last name, and three random numbers. For example, if a user's name is Terry Whitlock, a bucket name could be twhitlock256

To create a bucket in Amazon S3, you use the aws s3api create-bucket command. When you use this command to create an S3 bucket, you also include the following:

Specify --region  ap-south-1

Add --create-bucket-configuration LocationConstraint=ap-south-1 to the end of the command.

The following  command is  to create a new S3 bucket

aws s3api create-bucket --bucket Kaminopg123 --region us-west-2 --create-bucket-configuration LocationConstraint=us-west-2 ansd output in json (sucessful bucket creation)

Step 4: Create a new IAM user that has full access to Amazon S3

Using the AWS CLI, create a new IAM user with the command aws iam create-user and username awsS3user

![image](https://github.com/AJAYKUMARREDDY7373/My-Training-Projects-Aws-/assets/154115376/36c17ae8-e561-4779-8e71-495ddba0067c)

Create a login profile for the new user by using the following command:

![image](https://github.com/AJAYKUMARREDDY7373/My-Training-Projects-Aws-/assets/154115376/cc9223e3-f41a-4c82-baae-9d4842f50db5)

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

![image](https://github.com/AJAYKUMARREDDY7373/My-Training-Projects-Aws-/assets/154115376/223e3be3-a004-442b-a41f-b77a7ba77536)


Note: The bucket that you created might not be visible. Refresh the Amazon S3 console page to see if it appears. The awsS3user user does not have Amazon S3 access to the bucket that you created, so you might see an error for Access to this bucket.  

In the terminal window, to find the AWS managed policy that grants full access to Amazon S3, run the following command:

![image](https://github.com/AJAYKUMARREDDY7373/My-Training-Projects-Aws-/assets/154115376/e8f7c69a-0d2e-4b97-a9fb-9c5649fb07de)

The result displays policies that have a PolicyName attribute containing the term S3. Locate the policy that grants full access to Amazon S3. You use this policy in the next step.

To grant the awsS3user user full access to the S3 bucket, replace <policyYouFound> in following command with the appropriate PolicyName from the results, and run the adjusted command:

![image](https://github.com/AJAYKUMARREDDY7373/My-Training-Projects-Aws-/assets/154115376/f4290845-8d93-4ee6-9b99-dff26f27ddcd)

eturn to the AWS Management Console, and refresh the browser tab.

Step 5: Adjust S3 bucket permissions
On the AWS Management Console, on the Amazon S3 console, choose your bucket name.

Go to permissions, under Block public access (bucket settings), choose Edit

DeSelect/UnSelect Block all public access

Choose Save changes (confirm on the prompt)

On to permissions tab, under Object Ownership, choose Edit

Choose ACLs enabled

Choose I acknowledge that ACLs will be restored.

Choose Save changes

Step 6: Extract the files that you need for this lab
A file containing the static-website contents for the Amazon S3 bucket will need to be extracted in the following step.

Back in the SSH terminal, extract the files that you need for this lab by running the following commands:
![image](https://github.com/AJAYKUMARREDDY7373/My-Training-Projects-Aws-/assets/154115376/7e2659fa-dbfc-4719-8ef0-697a222b0c99)

To confirm that the files were extracted correctly, run the ls command.

Step 7: Upload files to Amazon S3 by using the AWS CLI
Once the files are extracted, you upload the contents of the file to Amazon S3. These files include what you explored when you ran the ls command.

So that the bucket can function as a website, replace <my-bucket> in the following command with your bucket name, and run the adjusted command. 


![image](https://github.com/AJAYKUMARREDDY7373/My-Training-Projects-Aws-/assets/154115376/357d3c17-3073-4d92-a152-74327d1e5ce9)

This process helps ensure that the index.html file will be known as the index document.

To upload the files to the bucket, replace <my-bucket> in the following command with your bucket name, and run the adjusted command:


![image](https://github.com/AJAYKUMARREDDY7373/My-Training-Projects-Aws-/assets/154115376/fc2d5e3e-9fe2-4ec7-bcdf-2b829b92c160)

To verify that the files were uploaded, replace <my-bucket> in the following command with your bucket name, and run the adjusted command:


![image](https://github.com/AJAYKUMARREDDY7373/My-Training-Projects-Aws-/assets/154115376/8de789d6-639e-429d-a5f5-bc37de7fac80)

On the AWS Management Console, on the Amazon S3 console, choose your bucket name.

Choose the Properties tab. At the bottom of the this tab, note that Static website hosting is Enabled. Running the aws s3 website AWS CLI command turns on the static website hosting for an Amazon S3 bucket. This option is usually turned off by default.

To open the URL on a new page, choose the Bucket website endpoint URL that displays.

Task 8: Create a batch file to make updating the website repeatable
To create a repeatable deployment, you create a batch file by using the VI editor. 

Locate the line where you ran the aws s3 cp command. You will put this line in your new batch file.

To change directories and create an empty file, run the following command in the SSH terminal session:


![image](https://github.com/AJAYKUMARREDDY7373/My-Training-Projects-Aws-/assets/154115376/efd2d94f-4629-4feb-9d53-5edd806dc045)

To open the empty file in the VI editor, run the following command.


![image](https://github.com/AJAYKUMARREDDY7373/My-Training-Projects-Aws-/assets/154115376/b0f9c44d-a7b6-4dbd-8848-0223cd7251bf)

To enter edit mode in the VI editor, press i

Next, you add the standard first line of a bash file and then add the s3 cp line from your history. To do so, replace <my-bucket> in the following command with your bucket name, and copy and paste the adjusted command into your file:


![image](https://github.com/AJAYKUMARREDDY7373/My-Training-Projects-Aws-/assets/154115376/8f6bcbdc-93fa-48e8-a04e-bbba63b573f4)

To write the changes and quit the file, press Esc, enter :wq and then press Enter.

To make the file an executable batch file, run the following command:

![image](https://github.com/AJAYKUMARREDDY7373/My-Training-Projects-Aws-/assets/154115376/7858bef9-0ebc-4e56-bb14-374589f2f277)

S3 static website .......

![image](https://github.com/AJAYKUMARREDDY7373/My-Training-Projects-Aws-/assets/154115376/e41b8f7d-3b65-4717-be2a-983ce69a3bed)


Step 9: Clean up

If you created your static website only as a learning exercise, delete the AWS resources that you allocated so that you no longer accrue charges. After you delete your AWS resources, your website is no longer available. For more information, see Deleting a bucket.

Source : @ Aws/Restart 













































