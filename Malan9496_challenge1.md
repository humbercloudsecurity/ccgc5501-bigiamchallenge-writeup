# Big IAM Challenge Lab 1 Writeup by Malan Venkatesan Sathyanaarayan - N01639496

## Overview  
This lab focused on analyzing an IAM policy, understanding its permissions, and using the AWS CLI to find and retrieve a flag stored in an S3 bucket.

-----------------------------------------------------------------------------------------------------------------------------------------------------

## What I Did  
1. Analyzing the IAM Policy
   - The policy had two `Action` keys: `s3:GetObject` and `s3:ListBucket`. These actions allow listing and retrieving files in the S3 bucket.  

2. Using AWS CLI to Interact with the Bucket
   - Following the AWS CLI guide, I listed the objects in the bucket using the below command which showed two files: `flag1.txt` and `logo.png`.
     ```
     aws s3 ls s3://thebigiamchallenge-storage-9979f4b/files/

   - I retrieved the flag file with:
     ```
     aws s3 cp s3://thebigiamchallenge-storage-9979f4b/files/flag1.txt -

3. Checking the Flag 
   - I pasted my flag in the `Insert flag` text box, completing the challenge.

------------------------------------------------------------------------------------------------------------------------------------------------

## Challenges Faced
- I wasn’t sure what a "flag" was or what I needed to find, but I learned that .txt files often contain flags.
- I didn’t fully understand IAM policies or their significance at first, but reading the documentation helped clarify the permissions.
- I wasn’t sure where to find the flag, but analyzing the IAM policy and listing S3 bucket contents led me to the right files.
- I was unfamiliar with AWS CLI commands, but by following guides and experimenting, I was able to successfully retrieve the flag.

---------------------------------------------------------------------------------------------------------------------------------------------------

## Lessons Learned  
- Actions like `s3:GetObject` and `s3:ListBucket` can expose sensitive data if not restricted.  
- The CLI is a powerful tool for interacting with AWS resources, especially when investigating bucket contents.  
- Always review IAM policies to prevent unauthorized access and secure S3 buckets with proper permissions.
