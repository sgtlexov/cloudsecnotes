## Overview of AWS

Amazon Web Services offers a broad set of global cloud-based products including compute, storage, databases, analytics, networking, mobile, developer tools, management tools, IoT, security, and enterprise applications: on-demand, available in seconds, with pay-as-you-go pricing. New services can be provisioned quickly, without the upfront fixed expense. This allows enterprises, start-ups, small and medium-sized businesses, developers, and customers in the public sector to access the building blocks they need to respond quickly to changing business requirements,

## AWS Global Infrastructure
Infrastructure, like data centers and networking connectivity, still exists as the foundation of every cloud application. In AWS, this physical infrastructure makes up the AWS Global Infrastructure, in the form of Regions and Availability Zones. Regions are geographic locations worldwide where AWS hosts its data centers. AWS Regions are named after the location where they reside. For example, in the United States, the Region in Northern Virginia is called the Northern Virginia Region, and the Region in Oregon is called the Oregon Region. Each AWS Region is associated with a geographical name and a Region code. For example, us-east-1 is the first Region created in the eastern US area. The geographical name for this Region is N. Virginia. AWS has Regions in Asia Pacific, China, Europe, the Middle East, North America, and South America.

Availability Zones

Inside every Region is a cluster of Availability Zones. An Availability Zone consists of one or more data centers with redundant power, networking, and connectivity. These data centers operate in discrete facilities in undisclosed locations. They are connected using redundant high-speed and low-latency links.

Availability Zones also have code names. Because they are located inside Regions, they can be addressed by appending a letter to the end of the Region code name. Here are examples of Availability Zone codes:

us-east-1a is an Availability Zone in us-east-1 (N. Virginia Region).

## Scope of AWS Services
There are over 200 AWS services available. Some services might not be available in some Regions. Depending on the AWS service that you use, your resources are either deployed at the Availability Zone, Region, or Global level. Edge locations are global locations where content is cached. Amazon CloudFront delivers your content through a worldwide network of edge locations.


Every action that you make in AWS is an API call that is authenticated and authorized.  In AWS, you can make API calls to services and resources through the AWS Management Console, AWS Command Line Interface (AWS CLI), or AWS Software Development Kits.

AWS Management Console
One way to manage cloud resources is through the web-based console, where you log in and choose the desired service. This can be the easiest way to create and manage resources when you first begin working with the cloud. The following is a screenshot that shows the landing page when you first log in to the console. 

AWS CLI
The AWS CLI is a unified tool that you can use to manage AWS services. You can download and configure one tool that you can use to control multiple AWS services from the command line, and automate them with scripts. The AWS CLI is open source, and installers are available for Windows, Linux, and macOS. Consider the scenario where you run many servers on AWS for your application’s frontend. You want to run a report to collect data from all the servers. You need to do this programmatically every day because the server details might change. Instead of manually logging in to the console and then copying and pasting information, you can schedule an AWS CLI script with an API call to pull this data for you.

AWS SDKs

API calls to AWS can also be performed by running code with programming languages. You can do this by using AWS SDKs. SDKs are open source and maintained by AWS for the most popular programming languages, such as C++, Go, Java, JavaScript, .NET, Node.js, PHP, Python, Ruby, Rust, and Swift.

Developers commonly use AWS SDKs to integrate their application source code with AWS services. For example, consider an application with a frontend that runs in Python. Every time the application receives a photo, it uploads the file to a storage service. This action can be achieved in the source code by using the AWS SDK for Python (Boto3).

## Security and the AWS Shared Responsibility Model

When you work with the AWS Cloud, managing security and compliance is a shared responsibility between AWS and you. To depict this shared responsibility, AWS created the shared responsibility model.
https://explore.skillbuilder.aws/files/a/w/aws_prod1_docebosaas_com/1720890000/6_W6AgtssnL6bKS1FN-TRA/tincan/7b5246b3e4dcf41ee9510fd1863163b18f6b0358/assets/G7jsXz1OeUet0P4d_VQj8P7tpf4Xy4mAS.png

## AWS Responsibility
AWS is responsible for security of the cloud. This means that AWS protects and secures the infrastructure that runs the services offered in the AWS Cloud. AWS is responsible for the following:

Protecting and securing AWS Regions, Availability Zones, and data centers, down to the physical security of the buildings
Managing the hardware, software, and networking components that run AWS services, such as the physical servers, host operating systems, virtualization layers, and AWS networking components
The level of responsibility that AWS has depends on the service. AWS classifies services into two categories. The following table provides information about each, including the AWS responsibility.

## Customer responsibility

Customers are responsible for security in the cloud. When using any AWS service, the customer is responsible for properly configuring the service and their applications, in addition to ensuring that their data is secure.

The customers' level of responsibility depends on the AWS service. Some services require the customer to perform all the necessary security configuration and management tasks. Other more abstracted services require customers to only manage the data and control access to their resources. Using the two categories of AWS services, customers can determine their level of responsibility for each AWS service that they use.
A key concept is that customers maintain complete control of their data and are responsible for managing the security related to their content. For example, you are responsible for the following:

- Choosing a Region for AWS resources in accordance with data sovereignty regulations
- Implementing data-protection mechanisms, such as encryption and scheduled backups
- Using access control to limit who can access your data and AWS resour

## Best practices
A well-known best practice for cloud architecture is to use Region-scoped, managed services. Replicate workload across multiple availability zones, at least two. That way, if an Availability Zone fails, your application will have infrastructure up and running in a second Availability Zone to take over the traffic.

If your application is sensitive to latency (the delay between a request for data and the response), choose a Region that is close to your user base. This helps prevent long wait times for your customers.

Due to the varying levels of effort, customers must consider which AWS services they use and review the level of responsibility required to secure each service. They must also review how the AWS shared responsibility model aligns with the security standards in their IT environment in addition to any applicable laws and regulations.





References
AWS Regions and Availability Zones: https://aws.amazon.com/about-aws/global-infrastructure/regions_az/

List of AWS Services Available by Region: https://aws.amazon.com/about-aws/global-infrastructure/regional-product-services/

AWS whitepaper: https://aws.amazon.com/products/
https://docs.aws.amazon.com/pdfs/whitepapers/latest/aws-overview/aws-overview.pdf

What Is the AWS Management Console?https://docs.aws.amazon.com/awsconsolehelpdocs/latest/gsg/what-is.html

AWS Command Line Interface: https://aws.amazon.com/cli/

AWS SDK for Python (Boto3): 
https://aws.amazon.com/sdk-for-python/?pg=developertools

AWS Shared Responsibility Model: https://aws.amazon.com/compliance/shared-responsibility-model/