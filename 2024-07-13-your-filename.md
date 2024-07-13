## Fundamentals to Cloud Computing

What is cloud computing?
Cloud computing is the delivery of computing services over the internet. Computing services include common IT infrastructure such as virtual machines, storage, databases, and networking. 

Why Cloud computing?
Prior to Amazon launching Amazon web services and Elastic Computer cloud in 2006, companies maintain on-premise datacenters. The company  is responsible for maintaining the physical space, ensuring security, and maintaining or replacing the servers if anything happens. The IT department is responsible for maintaining all the infrastructure and software needed to keep the datacenter up and running. They’re also likely to be responsible for keeping all systems patched and on the correct version. This was not sustainable because they are constrained by physical infrastructure. Suppose a company want to process more data, they will need to buy more servers to do that, which is a very high capital expenditure. But with cloud computing, they don't have to worry about that because it  uses the internet to deliver these services, thereby utilizing a operational expenditure model. That means if a company needs to increase their IT infrastructure rapidly, they don’t have to wait to build a new datacenter - they can use the cloud to rapidly expand their IT footprint.

### The shared responsibility model
With the shared responsibility model, these responsibilities get shared between the cloud provider and the customer. Physical security, power, cooling, and network connectivity are the responsibility of the cloud provider. The customer is responsible for the data and information stored in the cloud. Devices that are allowed to connect to your cloud (cell phones, computers, and so on)
The accounts and identities of the people, services, and devices within your organization.


### Cloud deployment models
The cloud models define the deployment type of cloud resources. The three main cloud models are: private, public, hybrid, and Multi-cloud. 

Private cloud: A private cloud is, in some ways, the natural evolution from a corporate datacenter. It’s a cloud (delivering IT services over the internet) that’s used by a single entity. Private cloud provides much greater control for the company and its IT department. However, it also comes with greater cost and fewer of the benefits of a public cloud deployment. Finally, a private cloud may be hosted from your on site datacenter. It may also be hosted in a dedicated datacenter offsite, potentially even by a third party that has dedicated that datacenter to your company. For example, company running workload on VMware in a private cloud environment.

Public cloud: A public cloud is built, controlled, and maintained by a third-party cloud provider. With a public cloud, anyone that wants to purchase cloud services can access and use resources. The general public availability is a key difference between public and private clouds. Public cloud is a multi-tenant environment where data
is spread across the shared public infrastructure. 

hypervisor
With zero trust in place, customer data is
isolated from other customers sharing the same server machines. This means that although
different customers share the same infrastructure, they’re unable to access each other’s data.

security
https://cloud.google.com/static/docs/security/infrastructure/design/resources/google_infrastructure_whitepaper_fa.pdf





Hybrid cloud: A hybrid cloud is a computing environment that uses both public and private clouds in an inter-connected environment. A hybrid cloud environment can be used to allow a private cloud to surge for increased, temporary demand by deploying public cloud resources. Hybrid cloud can be used to provide an extra layer of security. For example, users can flexibly choose which services to keep in public cloud and which to deploy to their private cloud infrastructure. 

Multi-cloud:  In a multi-cloud scenario, you use multiple public cloud providers. Maybe you use different features from different cloud providers. Or maybe you started your cloud journey with one provider and are in the process of migrating to a different provider. Regardless, in a multi-cloud environment you deal with two (or more) public cloud providers and manage resources and security in both environments.

### Cloud Service Providers
AWS -2006
GCP - 2008
Azure - 2010
Oracle Cloud
IBM Cloud

Cloud service models
### Infrastructure as a service (IaaS):
on-demand access to compute, storage, networking, and virtualization


Cloud provider is responsible for maintaining the hardware, network connectivity (to the internet), and physical security. Customer is responsible for everything else: operating system installation, configuration, and maintenance; network configuration; database and storage configuration, etc. The customer is bascically renting the hardware in a cloud datacenter but the customer decides what to do with it.

### Platform as a service (PaaS): 
hardware and software resources needed for cloud application development

The cloud provider maintains the physical infrastructure, physical security, and connection to the internet. They also maintain the operating systems, middleware, development tools, and business intelligence services that make up a cloud solution. The customer don't have to worry about the licensing or patching for operating systems and databases.

This is most suited to a lift and shift migration from an on-premise datacenters to a cloud development.

Why do we need cloud computing?
Prior to the advent of cloud computing, most ccomputing is done in an on-premises datacenter. Which means the customer is responsible for the physical security to the information and data security in their datacenter. 

### Software as a service (SaaS)
full-application stack as a cloud service, including the maintenance and management from underlying infrastructure to application software


With SaaS, the customer is essentially renting or using a fully developed application. For example, Email, financial software, messaging applications, and connectivity software are all common examples of a SaaS implementation.  SaaS is the model that places the most responsibility with the cloud provider and the least responsibility with the user. In a SaaS environment you’re responsible for the data that you put into the system, the devices that you allow to connect to the system, and the users that have access. 

Benefits of Cloud Computing
- Faster time to market: Cloud computing supports new innovations by making it easy to test new ideas and design new applications without hardware limitations or slow procurement processes. Developers can spin up new instances or retire them in seconds, allowing them to accelerate development with quick deployments.

- Scalability and flexibility: Companies don’t need to pay for or build the infrastructure needed to support their highest load levels. Likewise, they can quickly scale down if resources aren’t being used. Cloud computing gives your business more flexibility. You can quickly scale resources and storage up to meet business demands without having to invest in physical infrastructure.

Cost savings: Whatever cloud service model you choose, you only pay for the resources you actually use. This helps you avoid overbuilding and overprovisioning your data center and gives your IT teams back valuable time to focus on more strategic work. 

Better collaboration: Cloud storage enables you to make data available anywhere you are, anytime you need it. Instead of being tied to a location or specific device, people can access data from anywhere in the world from any device—as long as they have an internet connection.

Advanced security: Cloud computing can actually strengthen your security posture because of the depth and breadth of security features, automatic maintenance, and centralized management.

Data loss prevention: Cloud providers offer backup and disaster recovery features. Storing data in the cloud rather than locally can help prevent data loss in the event of an emergency, such as hardware malfunction, malicious threats, or even simple user error. 
