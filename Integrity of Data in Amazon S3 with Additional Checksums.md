Check the Integrity of Data in Amazon S3 with Additional Checksums 

Steps:
•	Create a S3 Bucket
•	Upload a file and specify the checksum algorithm
•	Verify checksum
•	Cleanup

Step 1: Create a S3 bucket:
•	Choose Buckets from the Amazon S3 menu on the left and then choose the Create bucket button.
![Screenshot 2024-06-10 094148](https://github.com/AJAYKUMARREDDY7373/My-Training-Projects-Aws-/assets/154115376/a8cab462-b1d6-4d41-aed4-d3c7d89bb896)

•	Enter a descriptive globally unique name for your bucket. Select which AWS Region you would like your bucket created in. The default Block Public Access setting is appropriate for this workload, so leave this section as is.
•	You can leave the remaining options as defaults, navigate to the bottom of the page, and choose Create bucket. 
![image](https://github.com/AJAYKUMARREDDY7373/My-Training-Projects-Aws-/assets/154115376/7218333e-6c5b-4826-95bb-be588013b627)
![image](https://github.com/AJAYKUMARREDDY7373/My-Training-Projects-Aws-/assets/154115376/89c3695c-dfcd-45f4-ac0f-ad2e76ef0291)
Step 2: Upload a file and specify the checksum algorithm:
Now that your bucket is created and configured, you are ready to upload a file and have the checksum calculated by Amazon S3.
Upload an object
•	If you have logged out of your AWS Management Console session, log back in. Navigate to the S3 console and select the Buckets menu option. From the list of available buckets, select the bucket name of the bucket you just created.


•	Next, select the Objects tab. Then, from within the Objects section, choose the Upload button.

![image](https://github.com/AJAYKUMARREDDY7373/My-Training-Projects-Aws-/assets/154115376/10f3b90f-2fbc-42ae-9c4c-2f2f06f50512)
Add files

•	Choose the Add files button and then select the file you would like to upload from your file browser.

![image](https://github.com/AJAYKUMARREDDY7373/My-Training-Projects-Aws-/assets/154115376/adedc20e-ba84-4293-ad44-75028e12e281)


 ![image](https://github.com/AJAYKUMARREDDY7373/My-Training-Projects-Aws-/assets/154115376/a8752aa2-18c4-46b2-b285-3793b4f39faa)
Expand properties

•	Navigate down the page to find the Properties section. Then, select Properties and expand the section.
 
Select additional checksums
•	Under Additional checksums select the On option and choose SHA-256.
![image](https://github.com/AJAYKUMARREDDY7373/My-Training-Projects-Aws-/assets/154115376/a8268e10-2d8b-4ae4-b011-9559f80571cd)


If your object is less than 16 MB and you have already calculated the SHA-256 checksum (base64 encoded), you can provide it in the Precalculated value input box. To use this functionality for objects larger than 16 MB, you can use the CLI or SDK. When Amazon S3 receives the object, it calculates the checksum by using the algorithm specified. If the checksum values do not match, Amazon S3 generates an error and rejects the upload, as shown in the screenshot.

 Upload
•	Navigate down the page and choose the Upload button.

![image](https://github.com/AJAYKUMARREDDY7373/My-Training-Projects-Aws-/assets/154115376/6c88a82c-40a1-4862-aaa1-e0ab8f458717)

•	After your upload completes, choose the Close button.
![image](https://github.com/AJAYKUMARREDDY7373/My-Training-Projects-Aws-/assets/154115376/721c261a-4dac-4ee8-aa81-18921fb694a1)
Step 3: Verify checksum:
•	Select the uploaded file by selecting the filename. This will take you to the Properties page.

![image](https://github.com/AJAYKUMARREDDY7373/My-Training-Projects-Aws-/assets/154115376/a306f294-df8c-4278-9e86-570d10f6fd0f)
•	Locate the checksum value
Navigate down the properties page and you will find the Additional checksums section.

![image](https://github.com/AJAYKUMARREDDY7373/My-Training-Projects-Aws-/assets/154115376/375ac2ec-adae-4ae8-9572-43a7552b5685)
•	This section displays the base64 encoded checksum that Amazon S3 calculated and verified at the time of upload.


Compare

•	To compare the object in your local computer, open a terminal window and navigate to where your file is.
•	Use a utility like shasum to calculate the file. The following command performs a sha256 calculation on the same file and converts the hex output to base64: 
shasum -a 256 image.jpg | cut -f1 -d\ | xxd -r -p | base64

![image](https://github.com/AJAYKUMARREDDY7373/My-Training-Projects-Aws-/assets/154115376/e2d17d40-4cc6-46b4-8f88-abb72275cfcb)

•	When comparing this value, it should match the value in the Amazon S3 console.


For windows ------->

![image](https://github.com/AJAYKUMARREDDY7373/My-Training-Projects-Aws-/assets/154115376/faf0f8ea-0dc2-4fbb-bdc0-f9c8bead74a4)

 
 Clean up:
 
In the following steps, you clean up the resources you created in this tutorial. It is a best practice to delete resources that you are no longer using so that you do not incur unintended charges. 
Delete test object

•	If you have logged out of your AWS Management Console session, log back in. Navigate to the S3 console and select the Buckets menu option. First you will need to delete the test object from your test bucket. Select the name of the bucket you have been working with for this tutorial. Put a check mark in the checkbox to the left of your test object name, then choose the Delete button. On the Delete objects page, verify that you have selected the proper object to delete and enter permanently delete into the Permanently delete objects confirmation box. Then, choose the Delete object button to continue. Next, you will be presented with a banner indicating if the deletion has been successful.
Delete test bucket

•	Finally, you need to delete the test bucket you have created. Return to the list of buckets in your account. Select the radio button to the left of the bucket you created for this tutorial, and then choose the Delete button. Review the warning message. If you desire to continue deletion of this bucket, enter the bucket name into the Delete bucket confirmation box, and choose Delete bucket.
