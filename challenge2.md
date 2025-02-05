# Challenge number
2
## Challenge Statement
(Google) Analytics
## IAM Policy
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Effect": "Allow",
            "Principal": "*",
            "Action": [
                "sqs:SendMessage",
                "sqs:ReceiveMessage"
            ],
            "Resource": "arn:aws:sqs:us-east-1:092297851374:wiz-tbic-analytics-sqs-queue-ca7a1b2"
        }
    ]
}

### write a short analysis about the IAM policy here
In this challenge 2, what I understood is the policy allows any principal to send and receive messages from aws sqs queue, wiz-tbic-analytics-sqs-queue-ca7a1b2, in the us-east-1 region. what I found interesting is about the policy is that anyone can send and receive message without restrictions, which has security risk. Attackers can easily retrieve the messages and will get exposure to sensitive data.

## Solution
Detailed steps to the flag
I gtot an  idea about the aws sqs from https://docs.aws.amazon.com/cli/latest/reference/sqs/receive-message.html
From there I found the command to receive messages from an sqs queue
 aws sqs receive-message --queue-url https://sqs.us-east-1.amazonaws.com/80398EXAMPLE/MyQueue --attribute-names All --message-attribute-names All 
I made appropriate changes to the command get the message.
That message contained the url to the flag.


## Reflection
I started with understanding the aws sqs. And I researched how to use the receive message command to interact with the queue and retrieve messages. The challenge was in getting the proper command to retrieve message, I made necessary changes to the command and received the message which contained the url to the flag 
