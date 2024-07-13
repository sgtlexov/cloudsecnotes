## AWS root user

When you first create an AWS account, you begin with a single sign-in identity that has complete access to all AWS services and resources in the account. This identity is called the AWS root user and is accessed by signing in with the email address and password that were used to create the account. 

## AWS root user credentials

The AWS root user has two sets of credentials associated with it. One set of credentials is the email address and password that were used to create the account. This allows you to access the AWS Management Console. The second set of credentials is called access keys, which allow you to make programmatic requests from the AWS Command Line Interface (AWS CLI) or AWS API.

Access keys consist of two parts:

Access key ID: for example, A2lAl5EXAMPLE
Secret access key: for example, wJalrFE/KbEKxE

Similar to a user name and password combination, you need both the access key ID and secret access key to authenticate your requests through the AWS CLI or AWS API. Access keys should be managed with the same security as an email address and password.

## AWS root user best practices

The root user has complete access to all AWS services and resources in your account, including your billing and personal information. Therefore, you should securely lock away the credentials associated with the root user and not use the root user for everyday tasks.

To ensure the safety of the root user, follow these best practices:


Choose a strong password for the root user.


Enable multi-factor authentication (MFA) for the root user.


Never share your root user password or access keys with anyone.


Disable or delete the access keys associated with the root user.


Create an Identity and Access Management (IAM) user for administrative tasks or everyday tasks.


## Multi-factor authentication
MFA requires two or more authentication methods to verify an identity.

- Something you know, such as a user name and password or pin number
- Something you have, such as a one-time passcode from a hardware device or mobile app
- Something you are, such as a fingerprint or face scanning technology

With a combination of this information, systems can provide a layered approach to account access. So even if the first method of authentication, like Bob’s password, is cracked by a malicious actor, the second method of authentication, such as a fingerprint, provides another level of security. This extra layer of security can help protect your most important accounts, which is why you should activate MFA on your AWS root user.

When you create an AWS account and first log in to the account, you use single-factor authentication. Single-factor authentication is the simplest and most common form of authentication. It only requires one authentication method. In this case, you use a user name and password to authenticate as the AWS root user. Other forms of single-factor authentication include a security pin or a security token.

However, sometimes a user’s password is easy to guess. For example, your coworker Bob’s password, IloveCats222, might be easy for someone who knows Bob personally to guess, because it’s a combination of information that is easy to remember and includes certain facts about Bob (Bob loves cats, and his birthday is February 22). If a bad actor guessed or cracked Bob’s password through social engineering, bots, or scripts, Bob might lose control of his account. Unfortunately, this is a common scenario that users of any website often face. This is why using multi-factor authentication (MFA) is important in preventing unwanted account access.

Using MFA adds an additional layer of security because it requires users to use a supported MFA mechanism in addition to their regular sign-in credentials. Activating MFA on the AWS root user account is an AWS best practice.


AWS supports a variety of MFA mechanisms, such as virtual MFA devices, hardware time-based one-time password (TOTP) tokens, and FIDO security keys. Microsoft Authenticator, Google Authenticator

https://explore.skillbuilder.aws/files/a/w/aws_prod1_docebosaas_com/1720890000/6_W6AgtssnL6bKS1FN-TRA/tincan/7b5246b3e4dcf41ee9510fd1863163b18f6b0358/assets/iH60qyuGvWpWH0pz_ae3D9Goxf5poTU_J.png






https://explore.skillbuilder.aws/files/a/w/aws_prod1_docebosaas_com/1720890000/6_W6AgtssnL6bKS1FN-TRA/tincan/7b5246b3e4dcf41ee9510fd1863163b18f6b0358/assets/6jTnHGzFpim42ZCZ_YD5J2pBrmA9lGqT-.png

Refrences
Enabling a virtual multi-factor authentication (MFA) device (console): https://docs.aws.amazon.com/IAM/latest/UserGuide/id_credentials_mfa_enable_virtual.html

Multi-Factor Authentication (MFA) for IAM: https://aws.amazon.com/iam/features/mfa/

Tasks that require root user credentials: https://docs.aws.amazon.com/IAM/latest/UserGuide/root-user-tasks.html