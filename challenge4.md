# Challenge number

4

## Challenge Statement

Admin only

## IAM Policy
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Effect": "Allow",
            "Principal": "*",
            "Action": "s3:GetObject",
            "Resource": "arn:aws:s3:::thebigiamchallenge-admin-storage-abf1321/*"
        },
        {
            "Effect": "Allow",
            "Principal": "*",
            "Action": "s3:ListBucket",
            "Resource": "arn:aws:s3:::thebigiamchallenge-admin-storage-abf1321",
            "Condition": {
                "StringLike": {
                    "s3:prefix": "files/*"
                },
                "ForAllValues:StringLike": {
                    "aws:PrincipalArn": "arn:aws:iam::133713371337:user/admin"
                }
            }
        }
    ]
}
### write a short analysis about the IAM policy here

The IAM policy allows listing the contents of the my-bucket S3 bucket (s3:ListBucket). The IAM policy allows getting objects from the my-bucket S3 bucket (s3:GetObject). The IAM policy explicitly denies permission to delete objects from the my-bucket S3 bucket (s3:DeleteObject). Sample use of both Allow and Deny statements. The Deny statement explicitly disallows deleting objects because, in most cases, a user shouldn't be able to delete data. Resource ARNs identify only the my-bucket bucket and all of its contents.

## Solution

Step 1. State what this policy allows:
The policy explicitly allows permissions on ListBucket and GetObject to mybucket whereas it explicitly denies the action DeleteObject.
Step 2. Find a weakness:
With this policy, it allows the GetObject action. With this permission, users of this permission might access and download sensitive files. It could be interesting to search if there are sensitive files or bucket misconfigurations.
Step 3: Plan a defense mechanism:
Ensure that Deny in the permission for sensitive actions is set, such as DeleteObject. Add more layers, such as encryption or tighter access control through IAM conditions, VPC restrictions, etc.
Step 4: Find flag
Identify any unused permissions or missing logging to account for access or changes.

## Reflection

I began the IAM policy review by assessing the allowed and denied permissions to identify potential vulnerabilities. The main challenge was finding risks despite restrictive permissions, like the denied s3:DeleteObject. My concern was the potential exposure of sensitive data through the GetObject permission, so I considered adding extra security layers such as encryption or IP restrictions. The breakthrough came when I realized that, even with the deny rule, data exposure or misconfigured files could still be a problem.
