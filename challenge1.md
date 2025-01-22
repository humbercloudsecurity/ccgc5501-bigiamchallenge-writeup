## Challenge number
1
## Challenge Statement
Buckets of Fun
## IAM Policy
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
Close
### Write a short analysis about the IAM policy here

The policy allowed access to s3:GetObject for retrieving objects, but access to s3:ListBucket was denied, meaning I couldn't list the objects in the bucket. The policy grants me the ability to retrieve specific objects from the S3 bucket thebigiamchallenge-storage-9979f4b but prevents me from listing its contents. This setup provides object retrieval access while denying listing, which forces reliance on guessing or obtaining the object key through alternative means.

## Solution
The policy allows me to retrieve specific objects from the S3 bucket thebigiamchallenge-storage-9979f4b, but it prevents me from listing the contents of the bucket. The policy gives us object retrieval access while denying listing. This forces reliance on guessing or obtaining the object key through alternative means. The IAM policy allows the s3:GetObject permission for objects within the bucket but denies the s3:ListBucket permission. This means I cannot list the contents of the bucket but can access objects if I know their names.
To list the details in the /file directory 
# aws s3 ls thebigiamchallenge-storage-9979f4b/files/
Copy the specific file (flag1.txt) and store it in /tmp/flag1.txt
# aws s3 cp s3://thebigiamchallenge-storage-9979f4b/files/flag1.txt /tmp/flag1.txt
And to display the content,
# cat /tmp/flag1.txt

## Reflection
The very first thing I did was go through the IAM policy to understand the permissions and restrictions it imposed. The biggest hurdle I encountered was the inability to list the contents of the S3 bucket. The policy allowed s3:GetObject for retrieving objects but denied s3:ListBucket, which meant I couldn't list the objects in the bucket to discover what was available.
The breakthrough came when I successfully retrieved the object, text1.txt, by guessing its name. This experience highlighted how the restriction on s3:ListBucket ensures that no user can discover objects within the bucket, which is a critical control for protecting sensitive or private data. In scenarios where even knowing the existence of a file could expose sensitive information, this restriction adds an important layer of security.
