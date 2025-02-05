# Challenge number
3

## Challenge Statement
Enable Push Notifications

## IAM Policy
{
    "Version": "2008-10-17",
    "Id": "Statement1",
    "Statement": [
        {
            "Sid": "Statement1",
            "Effect": "Allow",
            "Principal": {
                "AWS": "*"
            },
            "Action": "SNS:Subscribe",
            "Resource": "arn:aws:sns:us-east-1:092297851374:TBICWizPushNotifications",
            "Condition": {
                "StringLike": {
                    "sns:Endpoint": "*@tbic.wiz.io"
                }
            }
        }
    ]
}

### write a short analysis about the IAM policy here
In this challenge, I reviewed an IAM policy to understand what access it grants and what limitations it imposes. By analyzing the permissions, I understood that the Action field specifies "SNS:Subscribe", meaning I can subscribe an endpoint eg, email, etc to the SNS topic. The Resource field restricts this permission to a specific SNS topic:ARN: arn:aws:sns:us-east-1:092297851374:TBICWizPushNotifications. This means I cannot subscribe to other SNS topics unless additional permissions are granted. I do not have permission to publish messages to this SNS topic. 
This policy provides limited but controlled access to an SNS topic by allowing subscriptions but not message publishing.

## Solution

I read the documentation about the AWS SNS from https://docs.aws.amazon.com/sns/latest/dg/welcome.html and got more information about the same from https://docs.aws.amazon.com/cli/latest/reference/sns/ and from the list of available commands, I chose subscribe, which allows subscribing an endpoint (email) to an SNS topic. I used the following command:
aws sns subscribe \
    --topic-arn arn:aws:sns:us-west-2:123456789012:my-topic \
    --protocol email \
    --notification-endpoint my-email@example.com
I then modified the command to match the specific SNS topic ARN provided in the challenge. The command successfully subscribed an email address to the topic, meaning I would receive notifications sent to it.
To capture the request and retrieve the flag, I usedhttps://requestcatcher.com/  . After making further modifications to my setup, I successfully received the flag.

## Reflection
My approach was to first analyze the IAM policy to understand what actions were permitted and what restrictions were in place. I found that I was only allowed SNS:Subscribe. The biggest challenge was the limited access granted by the policy. Since the policy did not allow SNS:Publish, I couldn't send messages or verify the subscription directly through publishing. The breakthrough came when I successfully subscribed to the SNS topic and started monitoring incoming messages, which helped me capture the required information.
