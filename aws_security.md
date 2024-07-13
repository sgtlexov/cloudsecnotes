## Design Principles

In the cloud, there are a number of principles that can help you strengthen your security. Use the principles described below to help guide your conversation around security and compliance. 

Implement a strong identity foundation
Enable traceability: Implement the principle of least privilege and enforce separation of duties with appropriate authorization for each interaction with your AWS resources.

Enable traceability: Monitor, alert, and audit actions and changes to your environment in real time. Integrate logs and metrics with systems to automatically respond and take action.

Automate security best practices: Automated software-based security mechanisms improve your ability to securely scale more rapidly and cost effectively. Implement controls that are defined and managed as code in version-controlled templates.

Apply security at all layers: Rather than just focusing on protection of a single outer layer, apply a defense-in-depth approach with other security controls.

Protect data in transit and at rest: Classify your data into sensitivity levels and use mechanisms, such as encryption and access control, where appropriate.

Keep people away from data: Reduce or eliminate the need for direct access or manual processing of data. This reduces the risk of loss or modification and human error when handling sensitive data.

Prepare for security events: Prepare for an incident by having an incident management process that aligns to your organizational requirements. Run incident response simulations and use tools with automation to increase your speed for detection, investigation, and recovery.

## Identity and Access Management
The careful management of access credentials is the foundation of how you will secure your resources in the cloud. Every interaction you make with AWS is authenticated.  



https://aws-media.tutorialsdojo.com/secfun_en_m1_3.0.0/assets/hR7SICpTxd6HLoMp_tk8V66fLIg-OeaB6.png

## AWS root user

When you first create an AWS account, you begin with a single sign-in identity that has complete access to all AWS services and resources in the account. This identity is called the AWS root user and is accessed by signing in with the email address and password that were used to create the account. You use this identity to establish less-privileged users and role-based access in the AWS Identity and Access Management (IAM) service. AWS IAM is a centralized mechanism for creating and managing individual users and their permissions with your AWS account. 

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


## Types of AWS Credentials

## Password policies
A password policy is a set of rules that define the type of password an IAM user can set. You should define a password policy for all of your IAM users to enforce strong passwords and regular changing of passwords. Password requirements are similar to those found in most secure online environments.


## Multi-factor authentication
AWS Multi-Factor Authentication (MFA) is an additional layer of security for accessing AWS services. With this authentication method, more than one authentication factor is checked before access is granted, which consists of a user name and password, and the single-use code from the MFA device.

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


## User Access Keys
Users need their own access keys to make programmatic calls to AWS using the AWS CLI, the AWS SDKs, or direct HTTPS calls using the APIs for individual AWS services. Access keys are used to digitally sign API calls made to AWS services. Each access key credential is comprised of an access key ID and a secret key. Each user can have two active access keys, which is useful when you need to rotate the user's access keys or revoke permissions.
https://aws-media.tutorialsdojo.com/secfun_en_m1_3.0.0/assets/tFpGW0KXUIK1HWn0_R-tq4qqC6gdyNjre.png

## Amazon EC2 Key Pairs
To enable SSH or RDP connections to an Amazon Elastic Cloud Compute (EC2) instance, AWS uses a public–key infrastructure to sign the login request. The public and private keys are known as a key pair. To log in to your instance, you must create a key pair, or use an existing key pair, and provide the private key when you connect to the instance. You can choose to have the EC2 key pairs generated by AWS or import your own set of keys.



EC2 key pairs do not provide accountability (as in who is using the keys); therefore, they are not recommended for routine usage. If you require daily access to the instance, AWS recommends that EC2 instances be part of a directory domain (Active Directory or LDAP) in order to enable federated access and provide accountability by tracking which user is logging into which instance.
















## AWS Identity and Access Management
Authentication and authorization

When you configure access to any account, two terms come up frequently: authentication and authorization. Although these terms might seem basic, you must fully understand them to properly configure access management on AWS. 


## Authentication

When you create your AWS account, you use the combination of an email address and a password to verify your identity. If a user types in the correct email address and password, the system assumes the user is allowed to enter and grants them access. This is the process of authentication.

Authentication ensures that the user is who they say they are. User names and passwords are the most common types of authentication. But you might also work with other forms, such as token-based authentication or biometric data, like a fingerprint. Authentication simply answers the question, “Are you who you say you are?”

## Authorization

After you’re authenticated and in your AWS account, you might be curious about what actions you can take. This is where authorization comes in. Authorization is the process of giving users permission to access AWS resources and services. Authorization determines whether a user can perform certain actions, such as read, edit, delete, or create resources. Authorization answers the question, “What actions can you perform?” 

https://explore.skillbuilder.aws/files/a/w/aws_prod1_docebosaas_com/1720890000/6_W6AgtssnL6bKS1FN-TRA/tincan/7b5246b3e4dcf41ee9510fd1863163b18f6b0358/assets/yveoE-Ree5gXh1dz_wuLIgbyGCnHrkih0.png


## What is IAM?
AWS Identity and Access Management (IAM) is an AWS service that helps you manage access to your AWS account and resources. It also provides a centralized view of who and what are allowed inside your AWS account (authentication), and who and what have permissions to use and work with your AWS resources (authorization).

With IAM, you can share access to an AWS account and resources without sharing your set of access keys or password. You can also provide granular access to those working in your account, so people and services only have permissions to the resources that they need. For example, to provide a user of your AWS account with read-only access to a particular AWS service, you can granularly select which actions and which resources in that service that they can access.

## IAM features
To help control access and manage identities in your AWS account, IAM offers many features to ensure 
security.

IAM is global and not specific to any one Region. You can see and use your IAM configurations from any Region in the AWS Management Console.

IAM is integrated with many AWS services by default.

You can grant other identities permission to administer and use resources in your AWS account without having to share your password and key.

IAM supports MFA. You can add MFA to your account and to individual users for extra security.

IAM supports identity federation, which allows users with passwords elsewhere—like your corporate network or internet identity provider—to get temporary access to your AWS account. 


Any AWS customer can use IAM; the service is offered at no additional charge.


## IAM user

An IAM user represents a person or service that interacts with AWS. You define the user in your AWS account. Any activity done by that user is billed to your account. When you create a user, that user can sign in to gain access to the AWS resources inside your account.

You can also add more users to your account as needed. For example, for your cat photo application, you could create individual users in your AWS account that correspond to the people who are working on your application. Each person should have their own login credentials to prevent sharing credentials between users.

IAM user credentials

An IAM user consists of a name and a set of credentials. When you create a user, you can provide them with the following types of access:

Access to the AWS Management Console
Programmatic access to the AWS CLI and AWS API
To access the console, provide the user with a user name and password. For programmatic access, AWS generates a set of access keys that can be used with the AWS CLI and AWS API. IAM user credentials are considered permanent, which means that they stay with the user until there’s a forced rotation by admins.

When you create an IAM user, you can grant permissions directly at the user level. This can seem like a good idea if you have only one or a few users. However, as the number of users increases, keeping up with permissions can become more complicated. For example, if you have 3,000 users in your AWS account, administering access and getting a top-level view of who can perform what actions on which resources can be challenging.

Fortunately, you can group IAM users and attach permissions at the group level.


## IAM groups

An IAM group is a collection of users. All users in the group inherit the permissions assigned to the group. This makes it possible to give permissions to multiple users at once. It’s a more convenient and scalable way of managing permissions for users in your AWS account. This is why using IAM groups is a best practice.

If you have an application that you’re trying to build and you have multiple users in one account working on the application, you might organize the users by job function. For example, you might organize your IAM groups by developers, security, and admins. You could then place all your IAM users into their respective groups.

This provides a way to see who has what permissions in your organization. It also helps you scale when new people join, leave, and change roles in your organization.









Consider the following examples:

A new developer joins your AWS account to help with your application. You create a new user and add them to the developer group, without thinking about which permissions they need.
A developer changes jobs and becomes a security engineer. Instead of editing the user’s permissions directly, you remove them from the old group and add them to the new group that already has the correct level of access.
Keep in mind the following features of groups:

Groups can have many users.
Users can belong to many groups.
Groups cannot belong to groups.
The root user can perform all actions on all resources inside an AWS account by default. This is in contrast to creating new IAM users, new groups, or new roles. To allow an IAM identity to perform specific actions in AWS, such as implement resources, you must grant the IAM user the necessary permissions.

The way you grant permissions in IAM is by using IAM policies.

## IAM policies

To manage access and provide permissions to AWS services and resources, you create IAM policies and attach them to an IAM identity. Whenever an IAM identity makes a request, AWS evaluates the policies associated with them. For example, if you have a developer inside the developers group who makes a request to an AWS service, AWS evaluates any policies attached to the developers group and any policies attached to the developer user to determine if the request should be allowed or denied.

IAM policy examples

Most policies are stored in AWS as JSON documents with several policy elements. 


{
"Version": "2012-10-17",
"Statement": [{
"Effect": "Allow",
"Action": "*",
"Resource": "*"
}]
}

This policy has four major JSON elements: Version, Effect, Action, and Resource.

The Version element defines the version of the policy language. It specifies the language syntax rules that are needed by AWS to process a policy. To use all the available policy features, include "Version": "2012-10-17" before the "Statement" element in your policies.
The Effect element specifies whether the policy will allow or deny access. In this policy, the Effect is "Allow", which means you’re providing access to a particular resource.
The Action element describes the type of action that should be allowed or denied. In the example policy, the action is "*". This is called a wildcard, and it is used to symbolize every action inside your AWS account.
The Resource element specifies the object or objects that the policy statement covers. In the policy example, the resource is the wildcard "*". This represents all resources inside your AWS console.
Putting this information together, you have a policy that allows you to perform all actions on all resources in your AWS account. This is what we refer to as an administrator policy.

The next example shows a more granular IAM policy.

{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Sid": "DenyS3AccessOutsideMyBoundary",
      "Effect": "Deny",
      "Action": [
        "s3:*"
      ],
      "Resource": "*",
      "Condition": {
        "StringNotEquals": {
          "aws:ResourceAccount": [
            "222222222222"
          ]
        }
      }
    }
  ]
}
This policy uses a Deny effect to block access to Amazon S3 actions, unless the Amazon S3 resource that's being accessed is in account 222222222222. This ensures that any Amazon S3 principals are accessing only the resources that are inside of a trusted AWS account.



## IAM roles
All right, so you've learned about IAM users, groups, and policies. Policies can be applied to AWS identities like users and groups to assign permissions. They also, however, can be applied to another AWS identity, IAM roles. An IAM role is an identity that can be assumed by someone or something who needs temporary access to AWS credentials. 
IAM roles are identities in AWS that like an IAM user also have associated AWS credentials used to sign requests. However, IAM users have usernames and passwords as well as static credentials whereas IAM roles do not have any login credentials like a username and password and the credentials used to sign requests are programmatically acquired, temporary in nature, and automatically rotated. A role can be assumed by many different identities and they have many use cases. The important thing to know about roles is that the credentials they provide expire and roles are assumed programmatically. Another identity that can assume an IAM role to gain access to AWS is external identity providers, AWS assigns a role to a federated user when access is requested through an identity provider. We also have AWS services that can make this process easier such as AWS IAM Identity Center. 


## IAM best practices
The root user is an all-powerful and all-knowing identity in your AWS account. If a malicious user were to gain control of root-user credentials, they would be able to access every resource in your account, including personal and billing information. To lock down the root user, you can do the following:

Don’t share the credentials associated with the root user.
Consider deleting the root user access keys.
Activate MFA on the root account.

Follow Least privilege. Least privilege is a standard security principle that advises you to grant only the necessary permissions to do a particular job and nothing more. To implement least privilege for access control, start with the minimum set of permissions in an IAM policy and then grant additional permissions as necessary for a user, group, or role.

IAM is used to secure access to your AWS account and resources. It provides a way to create and manage users, groups, and roles to access resources in a single AWS account. IAM is not used for website authentication and authorization, such as providing users of a website with sign-in and sign-up functionality. IAM also does not support security controls for protecting operating systems and networks.

Maintaining roles is more efficient than maintaining users. When you assume a role, IAM dynamically provides temporary credentials that expire after a defined period of time, between 15 minutes and 36 hours. Users, on the other hand, have long-term credentials in the form of user name and password combinations or a set of access keys.

 

User access keys only expire when you or the account admin rotates the keys. User login credentials expire if you applied a password policy to your account that forces users to rotate their passwords.

consider managing employee identity information through an identity provider (IdP). Using an IdP, whether it's with an AWS service such as AWS IAM Identity Center (successor to AWS Single Sign-On) or a third-party identity provider, provides a single source of truth for all identities in your organization. You no longer have to create separate IAM users in AWS. You can instead use IAM roles to provide permissions to identities that are federated from your IdP. Being federated is a process that allows for the transfer of identity and authentication information across a set of networked systems. 

You might have IAM users, roles, permissions, policies, or credentials that you are no longer using in your account. IAM provides last accessed information to help you identify irrelevant credentials that you no longer need so that you can remove them. This helps you reduce the number of users, roles, permissions, policies, and credentials that you have to monitor.



## AWS Shared Responsibility Model

Security is a shared responsibility between you and AWS. 

AWS is responsible for protecting the global infrastructure that runs all of the services offered in the AWS Cloud. This infrastructure comprises the hardware, software, networking, and facilities that run AWS services.

As an AWS customer, you are responsible for securing your data, operating systems, networks, platforms, and other resources that you create in the AWS Cloud. You are responsible for protecting the confidentiality, integrity, and availability of your data and for meeting any specific business and/or compliance requirements for your workloads.

## DDoS Mitigation
A combination of AWS services may be used to implement a defense in depth strategy when it comes to DDoS attacks. These services are designed with an automatic response to DDoS attacks and can help minimize time to mitigate and reduce impact. AWS Edge locations provide an additional layer of network infrastructure that increases your ability to absorb DDoS attacks and to isolate faults while minimizing availability impact. Edge locations are physical data centers located in key cities, that are different from Availability Zones. As access to certain data increases with time, this data is copied to an edge location near your customer base for better performance and latency. Threats can then be taken care of at these edge locations, away from your web applications, AWS resources, and the original data.



# Compliance and Governance
AWS communicates about its security and control environment to customers by:


Obtaining industry certifications and independent third-party attestations.


Publishing information about AWS security and control practices in whitepapers and website content.


Providing certificates, reports, and other documentation directly to AWS customers under an NDA (as required).


Providing security features and enablers, including compliance playbook and mapping documents for compliance programs.



Customers can't visit AWS data centers to see how they are secured, however, AWS engages with external certifying bodies and independent auditors to provide customers with considerable information regarding the policies, processes, and controls established and operated by AWS.


Running your workloads on AWS does not automatically make the workload compliant. It is your responsibility to ensure that your workload meets all the requirements established in the compliance standard. However, AWS is already certified for its infrastructure, you only have to certify the applications and architectures you create.



Capturing and Collecting Logs

Detective controls are an essential part of governance frameworks and can be used to identify a potential security threat or incident. In AWS, there are a number of approaches to consider when addressing detective controls. AWS CloudTrail is a service that records API calls made on your account. This information helps you track changes made to your AWS resources, troubleshoot operational issues, and ensure compliance with internal policies and regulatory standards.

AWS CloudTrail is enabled by default on your AWS account. You can use the AWS API call history produced by CloudTrail to track changes to AWS resources, including creation, modification, and deletion of AWS resources.

Keeping every CloudTrail log in its immutable form is part of proving your compliance. The best suggestion is to have every log file copied to a different account with a non-penetrable access wall.  For example, if account A is tracking all actions using CloudTrail, all logs are copied to account B.  No user from account A has access to B, and vice-versa.  That way, any event forensics can prove that no one person, even a human with “admin access,” has the ability to cover their own tracks.

Monitoring and Notifications

It's not uncommon for organizations to integrate security alerts into their operations and platforms. The ability to detect change, determines whether a change was appropriate, and then route this information to the correct remediation workflow is essential.

In AWS, routing events and information reflecting potentially unwanted changes into a proper workflow is done using Amazon CloudWatch.  The functionality offered by CloudWatch can be used to monitor resources and logs, send notifications, and trigger automated actions for remediation. Take a moment to review the Amazon CloudWatch architecture below to learn more about this service.

https://aws-media.tutorialsdojo.com/secfun_en_m1_3.0.0/assets/k_mn1Iq9X3QmJ180_Roqy_g34KZ-lDIXq.png

Auditing on AWS

The AWS Management console, along with the AWS CLI, can produce powerful results for auditors across multiple regulatory, standards, and industry authorities. The key services to audit include Amazon S3, Elastic Load Balancing, Amazon CloudWatch, AWS CloudTrail, and Amazon VPC.  View each flashcard below for more information.










https://aws-media.tutorialsdojo.com/secfun_en_m1_3.0.0/assets/r27sGE6PjFpVD2UG_ni96Fiiy3vD7izIn.png


https://explore.skillbuilder.aws/files/a/w/aws_prod1_docebosaas_com/1720890000/6_W6AgtssnL6bKS1FN-TRA/tincan/7b5246b3e4dcf41ee9510fd1863163b18f6b0358/assets/XzQ6ItNPDmtH_jWs_WXZ1hMonELN5HDwI.png

Refrences
Enabling a virtual multi-factor authentication (MFA) device (console): https://docs.aws.amazon.com/IAM/latest/UserGuide/id_credentials_mfa_enable_virtual.html

Multi-Factor Authentication (MFA) for IAM: https://aws.amazon.com/iam/features/mfa/

Tasks that require root user credentials: https://docs.aws.amazon.com/IAM/latest/UserGuide/root-user-tasks.html

What is IAM: https://docs.aws.amazon.com/en_us/IAM/latest/UserGuide/introduction.html

IAM Identities (users, user groups, and roles): https://docs.aws.amazon.com/en_us/IAM/latest/UserGuide/id.html

Policies and permissions in IAM: https://docs.aws.amazon.com/en_us/IAM/latest/UserGuide/access_policies.html

How IAM works: https://docs.aws.amazon.com/en_us/IAM/latest/UserGuide/intro-structure.html

Access management for AWS resources: https://docs.aws.amazon.com/en_us/IAM/latest/UserGuide/access.html

Security best practices in IAM: https://docs.aws.amazon.com/IAM/latest/UserGuide/best-practices.html

Password Policies for IAM Users: https://docs.aws.amazon.com/IAM/latest/UserGuide/id_credentials_passwords_account-policy.html



AWS Best Practices for DDoS Resiliency:
https://aws.amazon.com/compliance/programs/

AWS Compliance Center: https://aws.amazon.com/financial-services/security-compliance/compliance-center/?country-compliance-center-cards.sort-by=item.additionalFields.headline&country-compliance-center-cards.sort-order=asc&awsf.country-compliance-center-master-filter=*all

Compliance Best Practices and Workbooks: https://aws.amazon.com/compliance/resources/

AWS CIS Foundations Benchmark:
https://d1.awsstatic.com/whitepapers/compliance/AWS_CIS_Foundations_Benchmark.pdf

AWS service endpoints: https://docs.aws.amazon.com/general/latest/gr/rande.html#ct_region

Detection: https://docs.aws.amazon.com/wellarchitected/latest/security-pillar/detection.html


Amazon CloudWatch Events
https://docs.aws.amazon.com/eventbridge/latest/userguide/eb-tutorial.html

https://aws.amazon.com/blogs/security/how-to-create-and-manage-users-within-aws-sso/
