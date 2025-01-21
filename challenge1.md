# Challenge number
Challenge: 1

## Challenge Statement
An S3 bucket has been configured with a public IAM policy, granting unrestricted access to list and download objects within a specific directory, files/. My task is to identify the security risk associated with this bucket by analyzing its access permissions. Additionally, I need to retrieve a flag stored in one of the accessible objects within the files/ directory. Once I have located and retrieved the flag, I will submit it to complete the challenge.

## IAM Policy
```json
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Effect": "Allow",
            "Principal": "*",
            "Action": "s3:GetObject",
            "Resource": "arn:aws:s3:::thebigiamchallenge-storage-9979f4b/*"
        },
        {
            "Effect": "Allow",
            "Principal": "*",
            "Action": "s3:ListBucket",
            "Resource": "arn:aws:s3:::thebigiamchallenge-storage-9979f4b",
            "Condition": {
                "StringLike": {
                    "s3:prefix": "files/*"
                }
            }
        }
    ]
}
```
### write a short analysis about the IAM policy here
* What do I have access to?
--> I have public access to list objects in the files/ directory and download any object stored in the bucket. This means I can freely explore and retrieve files without any authentication.

* What don't I have access to?
--> I don’t have access to list the entire bucket or interact with objects outside the files/ directory. The policy enforces a prefix condition for listing, ensuring only files within the files/ folder are exposed.

* What do I find interesting?
--> The fact that public access is enabled for listing and downloading files is concerning. It highlights a common misconfiguration where sensitive data could inadvertently be exposed. Despite the directory-specific restriction, it’s clear that this configuration could lead to data breaches.

* What could an attacker do with this access?
--> An attacker could exploit this access to download and analyze the files in the files/ directory, potentially uncovering sensitive information. If the bucket contained confidential data, this misconfiguration could lead to significant reputational and financial damage.

* How could this misconfiguration have been avoided?
--> This misconfiguration could have been avoided by limiting public access and enforcing stricter permissions. For instance, the Principal should not be set to * unless necessary, and access could be restricted using identity-based policies or IP conditions to prevent unauthorized usage.


## Solution
Step 1: List Bucket Contents
--> I used the AWS CLI to list the files under the files/ directory:
  aws s3 ls s3://thebigiamchallenge-storage-9979f4b/files/ --no-sign-request

Step 2: Identify Potential Files
--> From the output, I noted all files listed. Any file with a name like flag.txt or similar stood out as a candidate.

Step 3: Download and Inspect Files
--> I used the following command to download the file I suspected might contain the flag
  aws s3 cp s3://thebigiamchallenge-storage-9979f4b/files/flag.txt ./ --no-sign-request
  After downloading, I opened the file using a text editor and found the flag.

Step 4: Submit the Flag
--> Finally, I submitted the retrieved flag on the challenge platform.

## Reflection
* What was your approach?
--> My approach was to break down the challenge into manageable steps: analyze the policy, list accessible files, identify potential files of interest, and retrieve them to locate the flag.
  
* What was the biggest challenge?
--> The biggest challenge was ensuring I fully understood the scope of the IAM policy to determine what actions I could perform and where my access was limited.
  
* How did you overcome the challenges?
--> I overcame this by carefully reading the IAM policy and testing commands within the boundaries of the permissions granted. Tools like AWS CLI made it straightforward to validate my understanding.
  
* What led to the break through?
--> The breakthrough came when I identified that the s3:prefix condition restricted listing to the files/ directory. This made it clear where I should focus my efforts.
  
* On the blue side, how can the learning be used to properly defend the important assets?
--> This experience reinforces the importance of following the principle of least privilege when configuring IAM policies. Public access should be avoided unless absolutely necessary, and conditions like IP restrictions or authentication requirements should be added to protect sensitive resources. Regular audits of bucket permissions can also help prevent misconfigurations.

