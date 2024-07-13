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



Best practices
A well-known best practice for cloud architecture is to use Region-scoped, managed services. Replicate workload across multiple availability zones, at least two. That way, if an Availability Zone fails, your application will have infrastructure up and running in a second Availability Zone to take over the traffic.

If your application is sensitive to latency (the delay between a request for data and the response), choose a Region that is close to your user base. This helps prevent long wait times for your customers.










References
AWS Regions and Availability Zones: https://aws.amazon.com/about-aws/global-infrastructure/regions_az/

List of AWS Services Available by Region: https://aws.amazon.com/about-aws/global-infrastructure/regional-product-services/

AWS whitepaper: https://aws.amazon.com/products/
https://docs.aws.amazon.com/pdfs/whitepapers/latest/aws-overview/aws-overview.pdf
