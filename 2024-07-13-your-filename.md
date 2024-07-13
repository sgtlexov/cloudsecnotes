# Fundamentals to Cloud Computing

## What is cloud computing?
Cloud computing is the on-demsnd delivery of computing resources (virtual machines, storage, databases, and networking), as services over the internet. It eliminates the need for individuals and businesses to self-manage physical resources themselves, and only pay for what they use.

## Why Cloud computing?
Prior to Amazon launching Amazon web services and Elastic Computer cloud in 2006, companies maintain on-premise datacenters. The company  is responsible for maintaining the physical space, ensuring security, and maintaining or replacing the servers through procurement processes that can take months if anything happens. The IT department is responsible for maintaining all the infrastructure and software needed to keep the datacenter up and running. They’re also likely to be responsible for keeping all systems patched and on the correct version. This was not sustainable because they are constrained by physical infrastructure. Suppose a company want to process more data, they will need to buy more servers to do that, which is a very high capital expenditure. But with cloud computing, they don't have to worry about that because it  uses the internet to deliver these services, thereby utilizing a operational expenditure model. That means if a company needs to increase their IT infrastructure rapidly, they don’t have to wait to build a new datacenter - they can use the cloud to rapidly expand their IT footprint.


## Benefits of Cloud Computing
- Faster time to market: Cloud computing supports new innovations by making it easy to test new ideas and design new applications without hardware limitations or slow procurement processes. Developers can spin up new instances or retire them in seconds, allowing them to accelerate development with quick deployments.

- Scalability and flexibility: Companies don’t need to pay for or build the infrastructure needed to support their highest load levels. Likewise, they can quickly scale down if resources aren’t being used. Cloud computing gives your business more flexibility. You can quickly scale resources and storage up to meet business demands without having to invest in physical infrastructure.

- Cost savings: Whatever cloud service model you choose, you only pay for the resources you actually use. This helps you avoid overbuilding and overprovisioning your data center and gives your IT teams back valuable time to focus on more strategic work. 

- Better collaboration: Cloud storage enables you to make data available anywhere you are, anytime you need it. Instead of being tied to a location or specific device, people can access data from anywhere in the world from any device—as long as they have an internet connection.

- Advanced security: Cloud computing can actually strengthen your security posture because of the depth and breadth of security features, automatic maintenance, and centralized management.

- Data loss prevention: Cloud providers offer backup and disaster recovery features. Storing data in the cloud rather than locally can help prevent data loss in the event of an emergency, such as hardware malfunction, malicious threats, or even simple user error.


## Limitations of cloud computing
one of the most common drawbacks of cloud computing is that it relies on an internet connection. Traditional computing uses a hardwired connection to access data on servers or storage devices. With cloud computing, a bad connection could keep you from accessing the information or applications you need. 

Even top cloud service providers can experience downtime due to a natural disaster or slower performance caused by an unforeseen technical issue that might impact connectivity. You could be blocked from accessing cloud services until the problem is resolved. 

Other disadvantages of cloud computing include: 
- risk of vendor lock-in
- less control over underlying cloud infrastructure
- concerns about security risks like data privacy and online threats
- integration complexity with existing systems 
- unforeseen costs and unexpected expenses.



## Types of Cloud Computing  deployment models
The cloud models define the deployment type of cloud resources. The three main cloud models are: private, public, hybrid, and Multi-cloud. 

Private clouds: are built, managed, and owned by a single organization and privately hosted in their own data centers, commonly known as “on-premises” or “on-prem.” They provide greater control, security, and management of data while still enabling internal users to benefit from a shared pool of compute, storage, and network resources. For example, company running workload on VMware in a private cloud environment.

Public cloud: A public cloud is built, controlled, and maintained by a third-party cloud provider. They offer compute, storage, and network resources over the internet, enabling companies to access shared on-demand resources based on their unique requirements and business goals. Public cloud is a multi-tenant environment where data
is spread across the shared public infrastructure. 

Foundation of Cloud Computing
Virtualization is the foundation of cloud computing. Virtualization is the technology that creates a virtual version of physical infrastructure, such as servers, storgae, networks. They use virtual mchines. This technology uses virtual machines to simulate a physical computer. Virtual machines contain their own operating systems like windows or linux, and use only portion of the underlying computer;s power. Virtualization uses hypervisors to manage the relationship between physical and virtual resources. A hypervisor is the abstraction layer that sits between the physical computer and virtal machine. Abstraction is what separates hardware and software. 

Types of hypervisors

- Type one also known as bare metal. It replaces the entire operating system of the underlying computer.Type one hypervisors interact with the operating system’s components directly. Having this direct access makes type one streamlined and secure. On the flip side, type two hypervisors, also known as hosted, use the computer’s existing operating system and runs as an application over the operating system.
Type two hypervisors may be easier to install, but you need to take into consideration the extra overhead and security needs of the underlying operating system. So, hypervisors distribute resources across VMs and keep VMs separate so that each one simulates an individual computer.
And the hypervisor ensures that customer data is isolated from other customers sharing the same server machines. This means that although
different customers share the same infrastructure, they’re unable to access each other’s data.

security
https://cloud.google.com/static/docs/security/infrastructure/design/resources/google_infrastructure_whitepaper_fa.pdf





Hybrid cloud: A hybrid cloud combine public and private cloud models, allowing companies to leverage public cloud services and maintain the security and compliance capabilities commonly found in private cloud architectures.

Multi-cloud:  In a multi-cloud scenario, you use multiple public cloud providers. Maybe you use different features from different cloud providers. Or maybe you started your cloud journey with one provider and are in the process of migrating to a different provider. Regardless, in a multi-cloud environment you deal with two (or more) public cloud providers and manage resources and security in both environments.

### Cloud Service Providers
AWS -2006
GCP - 2008
Azure - 2010
Oracle Cloud
IBM Cloud

Cloud service models
### Infrastructure as a service (IaaS):
(IaaS) offers on-demand access to IT infrastructure services, including compute, storage, networking, and virtualization. It provides the highest level of control over your IT resources and most closely resembles traditional on-premises IT resources.

Cloud provider is responsible for maintaining the hardware, network connectivity (to the internet), and physical security. Customer is responsible for everything else: operating system installation, configuration, and maintenance; network configuration; database and storage configuration, etc. The customer is bascically renting the hardware in a cloud datacenter but the customer decides what to do with it.

### Platform as a service (PaaS): 
(PaaS) offers all the hardware and software resources needed for cloud application development. With PaaS, companies can focus fully on application development without the burden of managing and maintaining the underlying infrastructure.

The cloud provider maintains the physical infrastructure, physical security, and connection to the internet. They also maintain the operating systems, middleware, development tools, and business intelligence services that make up a cloud solution. The customer don't have to worry about the licensing or patching for operating systems and databases.
 

### Software as a service (SaaS)
(SaaS) delivers a full application stack as a service, from underlying infrastructure to maintenance and updates to the app software itself. A SaaS solution is often an end-user application, where both the service and the infrastructure is managed and maintained by the cloud service provider. With SaaS, the customer is essentially renting or using a fully developed application. For example, Email, financial software, messaging applications, and connectivity software are all common examples of a SaaS implementation.  SaaS is the model that places the most responsibility with the cloud provider and the least responsibility with the user. In a SaaS environment you’re responsible for the data that you put into the system, the devices that you allow to connect to the system, and the users that have access. 


### The shared responsibility model
With the shared responsibility model, these responsibilities get shared between the cloud provider and the customer. Physical security, power, cooling, and network connectivity are the responsibility of the cloud provider. The customer is responsible for the data and information stored in the cloud. Devices that are allowed to connect to your cloud (cell phones, computers, and so on)
The accounts and identities of the people, services, and devices within your organization.