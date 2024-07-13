## AWS root user

When you first create an AWS account, you begin with a single sign-in identity that has complete access to all AWS services and resources in the account. This identity is called the AWS root user and is accessed by signing in with the email address and password that were used to create the account. 

AWS root user credentials

The AWS root user has two sets of credentials associated with it. One set of credentials is the email address and password that were used to create the account. This allows you to access the AWS Management Console. The second set of credentials is called access keys, which allow you to make programmatic requests from the AWS Command Line Interface (AWS CLI) or AWS API.

Access keys consist of two parts:

Access key ID: for example, A2lAl5EXAMPLE
Secret access key: for example, wJalrFE/KbEKxE

Similar to a user name and password combination, you need both the access key ID and secret access key to authenticate your requests through the AWS CLI or AWS API. Access keys should be managed with the same security as an email address and password.

AWS root user best practices

The root user has complete access to all AWS services and resources in your account, including your billing and personal information. Therefore, you should securely lock away the credentials associated with the root user and not use the root user for everyday tasks. Visit the links at the end of this lesson to learn more about when to use the AWS root user.

To ensure the safety of the root user, follow these best practices:


Choose a strong password for the root user.


Enable multi-factor authentication (MFA) for the root user.


Never share your root user password or access keys with anyone.


Disable or delete the access keys associated with the root user.


Create an Identity and Access Management (IAM) user for administrative tasks or everyday tasks.

https://explore.skillbuilder.aws/files/a/w/aws_prod1_docebosaas_com/1720890000/6_W6AgtssnL6bKS1FN-TRA/tincan/7b5246b3e4dcf41ee9510fd1863163b18f6b0358/assets/6jTnHGzFpim42ZCZ_YD5J2pBrmA9lGqT-.png