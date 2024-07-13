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


Cloud service types
### Infrastructure as a service (IaaS)
Cloud provider is responsible for maintaining the hardware, network connectivity (to the internet), and physical security. Customer is responsible for everything else: operating system installation, configuration, and maintenance; network configuration; database and storage configuration, etc. The customer is bascically renting the hardware in a cloud datacenter but the customer decides what to do with it.

### Platform as a service (PaaS).
The cloud provider maintains the physical infrastructure, physical security, and connection to the internet. They also maintain the operating systems, middleware, development tools, and business intelligence services that make up a cloud solution. The customer don't have to worry about the licensing or patching for operating systems and databases.

This is most suited to a lift and shift migration from an on-premise datacenters to a cloud development.

Why do we need cloud computing?
Prior to the advent of cloud computing, most ccomputing is done in an on-premises datacenter. Which means the customer is responsible for the physical security to the information and data security in their datacenter. 

### Software as a service (SaaS)
With SaaS, the customer is essentially renting or using a fully developed application. For example, Email, financial software, messaging applications, and connectivity software are all common examples of a SaaS implementation.  SaaS is the model that places the most responsibility with the cloud provider and the least responsibility with the user. In a SaaS environment you’re responsible for the data that you put into the system, the devices that you allow to connect to the system, and the users that have access. 

Shared responsiiblity model
The shared responsibility model applies to all the cloud types. 

