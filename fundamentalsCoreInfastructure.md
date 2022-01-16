# **GCP ROUGH NOTES**

**CORE INFASTRUCTURE**

**Introduction to Google Cloud Platform**

_ **Introducing Google Cloud Platform** _

- Definition of cloud computing has five fundamental attributes
  - Customers get computing resources on demand and self-service
  - They can access these resources over the network
  - The provider of these resources has a big pool of them, and benefits from economies of scale
  - The resources are elastic
  - The customers only pay for what they reserve, as they go.
- The first wave of cloud computing was colocation, users can rent physical space instead of investing in their own data center
- The second wave is virtualized data centers
  - Virtualised data centres match the building blocks of hosted computing, but with virtual devices
  - This allows dev teams to move faster
- The third wave made by google is a container-based architecture, making a fully automated elastic cloud that consists of a combination of automated services and scalable data.
- GCP is organized into regions and zones
  - Regions are independent geographical areas that consist of zones
  - A zone is a deployment area for GCP resources within a region, a single failure domain – in order to have fault tolerable applications they should be deployed over multiple zones.
  - Regional resources have higher avaliablility than zonal resources.
  - There are multi-region resources that are managed by google, such as google cloud storage, app engine etc.
- Customers have the ability to run applications elsewhere if google becomes no longer the best provider
  - Using open APIS
  - Open source licenses
  - Interoperability at multiple layers of the stack
- Security is designed into Googles infastructure

![](RackMultipart20210217-4-1tzfxjl_html_4d7be70d22851a7e.jpg)

- GCP offers Compute, Storage, Big Data, Machine Learning, Networking, Operations/Tools

![](RackMultipart20210217-4-1tzfxjl_html_b59fe0538a9b2584.png)

- GCP is innovative in pricing because it offers sub-hour billing, sustained-use discounts, Compute Engine cusom machine types
- Some other benefits apart from pricing include commitment to environmental responsibility, commitment to open source technologies and robust infastructure.

_ **Welcome to GCP Fundamentals** _

- GCP offers four main types of service
  - Compute
  - Storage
  - Big Data
  - Machine Learning
- This course concerns the first two

_ **What is cloud Computing?** _

- Has five equally important traits

- On Demand self-service
- Broad network access
- Resource pooling
- Rapid elasticity
- Measured service

_ **How did we get here?** _

- First wave was colocation, it was user-configured managed and maintained.
- Second wave was virtualised, user configured, with provier-managed and maintained.
- Third wave is serverless and fully automated.

_ **Every company is a data company** _

- Google believes that everything will differentiate itself through software technology, this is centred on data
- GCP provides a wide variety of services for getting value from this data.

_ **GCP Computing Architectures** _

- Infastructure as a Service (IaaS)
  - Provide raw compute storage and network, not too disimilar to data centres
  - Pay for what you allocated
- Platform as a Service (Paas)
  - Binds application code to libraries that give infastructure that the application needs, so you can focus on the application logic.
  - Pay for what you use
- Momentum has shifted to managed services, that are automated and you do not need to worry about allocation.

_ **Google Network** _

- Carries up to 40% of network traffic worldwide
- Network interconnects at 90 internet exchanges
- Google responds to requests with edge locations that have the lowest latency available to user.

_ **GCP Regions and Zones** _

- GCP is organised in zones and regions
- Zones is the smallest deployment area for GCP resources
- Zones are grouped into regions, you can choose what regions to deploy.
- A zone is a single failure domain in a region, you can spread your applications across different zones to increase durability.
- You can also deploy over multiple regions

_ **Enviromental Responsibility** _

- Virtual world built on physical infatructure
- Google works to be carbon neutral
- Striving to use completely renewable resources for data centres

_ **Pricing Innovations** _

- Google bills by the second, first to do so
- There are discounts for sustained use, automatically applied to virtual use over 25% of a month
- Pay only for the resources you need.

_ **Open APIs** _

- So you don&#39;t get &#39;locked in&#39; to the cloud, google gives the choice to run your applications elsewhere (if google no longer offers what they need)
- GCP is compatible with some open source APIs
- Google publishes many open source software

_ **Why choose Google Cloud Platform** _

- Global, cost effective, open source friendly and designed for security
- Offers a range of compute services

_ **Multi-layered security approach** _

- Both the server boards and the networking equipment are custom designed by google
- Google designs custom chips as well
- Server machines use cryptographic signatures
- Google designs and builds its own data centres which have multiple layers of physical protections
- Pc traffic in transit between data centers is automatically encrypted
- Google log in challenges users based on metadata
- Google enables hardware encryption at REST
- Internet communication is registered with a service called the google front end which checks incoming network connections – also good at preventing DDOS
- Google conducts simulated attacks and uses ML to increase security

**Getting Started with Google Cloud Platform**

_ **Getting Started with Google Cloud Platform** _

- Cloud Security requires collaboration, Google is responsible for managing its infastructure security, but you are responsible for securing your data. Google helps with the best practices and products
  - Because of scale google can deliver a higher level of security at the layers of infastructure, such as the encryption of hard disks and the integrity of the network
  - Upper layers remain the customers responsibilty, but there are tools like IAM to help customers implement policies at these layers
- Resource hierarchy levels define trust boundaries, you can group resources according to ogranisation structure, the levels of the hierarchy provide trust boundaries and resource isolation.
  - From the bottom up, all resources used in GCP are organised into projects, these projects can be organised into folders and folders can be nested, folders and projects can then be organised under an organisation node
  - Policies can be defined at projects, folder and org nodes and policies are inherited downwards in the hierarchy, with some exceptions

![](RackMultipart20210217-4-1tzfxjl_html_86e10c568235856d.png)

- All GCP services you use are associated with a project, you use services that can track resource and quota usage, enable billing, manage permissions and credentials, and enable services and APIs.
  - Projects are the basis for enabling and using GCP services Each project is a separate compartment and each resource belongs to exactly one.
  - Projects can have different owners/users and are billed/managed separately.
  - The cloud resource manager provides methods that can be used to manage projects, it can be accessed through the RPC or REST API
- Each GCP project has a name and id that you assign, the id is a permanent unchangeable identifier which needs to be unique across GCP. GCP also assigns a project number that is unique, only the name of the project can be changed.

- Folders in GCP offer flexible management, they can contain projects, or other folders and are used to assign policies.
  - Resources in a folder inherit IAM policies assigned to the folder
  - You can use folders to group projects under an organisation or hierarchy, for example by representing multiple departments with different sets of GCP resources.
  - Folders also allow teams to delegate admin rights so that they can work independently.
  - To use folders you nede an organisation node at the top of the hierarchy, this acts as the root node for GCP resources, and is used to apply policies centrally.
- Organisation nodes can offer special roles, for example by assigning an organisation policy administrator so that only people with a certain privilege can change policies.
  - You get an organisation node if your company is also a G Suite customer, GCP projects will then automatically belong to the organisation node – if not you can use google cloud identity to create an organisation.

![](RackMultipart20210217-4-1tzfxjl_html_a267936fe9c5ad9d.png)

- Resources inherit the policies of their parent resource – One important rule to keep in mind is that the policies implemented at a higher level cannot take away access granted at a lower level
- Google Cloud Identity and Access Management lets admins authorise who can take action on specific resources, it has a &quot;who&quot; part a &quot;can do what&quot; part and an &quot;on which resource&quot; part.
  - The &quot;who&quot; can be a google account, a google group, a service account or an entire G suite or cloud identity domain.
  - The &quot; can do what&quot; part is defined by an IAM role. An IAM role is a collection of permissions, most of the time to do any meaningful operations you need more than 1 permission – so the permissions are grouped together in a role to make them easier to manage.
  - The &quot;on which resource&quot; when you give a user, group or service account a role on a specific element of the resource hierarchy, the resulting policy applies to the element you chose as well as the elements below it in the hierarchy.
- There are three types of roles in cloud IAM
  - Primitive roles are broad, you apply them to a GCP project and they affect all resoureces in that project. Examples are the Owner, Editor and Viewer roles. Owners can change permissions and set up billing for a project – there is also a billing admin role which controls the billing but not the resources of the project.
  - Predefined Roles are more finer-grained role which apply to a particular GCP service or project. For example, ComputeEngine has an instanceAdmin role that can change, start, stop and read virtual machines.
  - Custom Roles are even more finer grained, and can be used to adhere to a &quot;least privilege model&quot; which roles are defined with the minimum amount of permissions someone needs to do their jobs.
- Service Accounts can be defined so that permission and access to a certain resource is only avaliable to a service, for example an application running in a virtual machine that needs tos tore data in google cloud storage.
  - Service accounts need to be managed too, and work just like granting roles or any other GCP resource.
- Cloud Identity lets you manage users and groups using the google admin console whilst not having to pay or receive G Suite&#39;s collaboration products – its avaliable in a premium edition for capabilities for mobile device management
- Google Cloud Directory Sync can be used by administrators to log in and manage GCP resources with the same usernames and passwords they already use
  - This tool synchronizes users and groups from the existing active directory or LDAP system with the users and groups in your cloud identity domain
  - The synchronisation is one way only, with no information in the LDAP being modified.
- There are four ways to interact with GCP:
  - Cloud Platform Console
  - Cloud shell and Cloud SDK
  - Cloud Console Mobile App
  - REST-based API
- The GCP console is a centralised console for all project data, it has developer tools, access to product APIs and the ability to manage and create projects
  - GCP provides git version control to support collaboartive development of any application or service there is also a source editor that can be used to browser, view edit and commit changes within the console
  - The GCP shell provides command line access to cloud resources, you can easily manage projects and resources without having to install Google Cloud SDK.
- The Google Cloud SDK is a set of tools that you can use to manage esources and apllications hosted on the GCP. These include the gcloud tool, which provides the main command line interfce for GCP prodcuts and services – all are located under the bin directory
  - The SDK is available as a docker image and via the cloud shell
  - The cloud shell provides a temporary compute engine virtual machine with a debian based OS
  - It has many features like persistent disk storage, language support command line access to cloud instances and web prievew functionality.
- REST API offers programmatic access to products and services, it uses JSON as the interchange format and Oauth 2.0 for authentication and authorisation. Its enables through the GCP console
  - The GCP console includes a tool called the APIs explorer with can help you learn about the api interactively, showing what apis and what versions are avaliable
  - Google also provides client libraries to interface with the API
  - There are two Client Libraries, Cloud Client libraries are the latest and the recommended as they adopt the native styles and idioms of each language.
  - There is also the Google API Client Library for services and features that aren&#39;t supported by the cloud client libraries.
  - The Google API Client Library is designed for generality and completeness.
- Cloud Console Mobile App allows users to manage virtual machines and database instances, manage apps in the google app engine, manage billing and visualise projects with a customisable dashboard.
  - The app allows you to start, stop and ssh into compute engine instances, and see logs from each instance.
  - You can stop and start cloud SQL instances, and adminster applications deployed on the google app engine, by viewing errors, rolling back deployments and changing traffic splitting.
  - You can also get billing information and set up cusomisable graphs showing key metrics , as well as alerts and incident management
- Cloud marketplace gives quick access to solutions, it lets you quickly deploy functiuonal software packages that run on GCP, some are offered by google while some are offered by third party vendors.
  - Many software packages are free, the only costs are normal usage fees.
  - GCP updates the images for these software packages to fix critical issues and
  - vulnerabilities, but doesn&#39;t update already deployed software.

_ **Introduction** _

- Projects are the main way you organise the resoucres you use in GCP
- They usually have a common business objective
- The principle of least priviledge is important because it is means people are less likely to break things
- There are four ways to interact with GCP, console etc
- In on Premises infastructure, you are responsible for all security, but in GCP google handles many of the lower layers of security – because of its scale google can offer a high level of security .

_ **Google Cloud Platform Resource Hierarchy** _

- All resources used are organised into projects, optionally they may be organised into folders that can be nested
- All projects and folders are organised under an organisation node
- Resource hierarchy defines trust boundaries and resource isolation
- Policies are ineherit downwards in a hierarchy
- Each project is a separate compartment that can have different owners and users
- They have a name and id that you assign and a project number assigned by GCP
- Projects can be organised into folders to represent different departments, teams and environments.
- Resources in a folder inherit IAM policies from the folder, otherwise you would have to duplicate policies which make me tedious and cause errors
- Most companies want to apply policies centrally – which is what the organistation node is for.
- If you are G Suite customer, and you have a domain then you have an organisation domain by automatic
- Otherwise you can use google cloud identity to create an organisation node.
- Once you have an organisation node you can put folders in it
- Policies implemented at a higher level cannot take away access at a lower level

_**Identity and Access Management (IAM)**_

- Lets admins authorise who can take action on specific resources, it has a &quot;who&quot;, &quot;can do what&quot;, &quot;on which resource&quot; part.
- Who is defined by a google account, google group, cloud identity domain etc
- Can do what is defined by an IAM role – Primitive roles are broad such as the Owner, Editor, Viewer or Billing Admin. You can also have Predefined roles that are defined by each service. Finally you can make custom roles.

_ **IAM Roles** _

- Compute Engine has cusom roles – for example the eability to delete start and stop VMS
- Custom Roles can be used to set precise permission to adhere to the priciple of least priviledge
- Custom Roles cannot be used at the folder level, only at the project or organisation level
- You can also give permissions to a service account rather than a user for server-to-server interactions – they can be identified with an email address.
- Service accounts need to be managed too and can have user defined permission on it – you can grant diffeent groups of VMs different service permissions.

_ **Interacting With GCP** _

- Four ways to interact with GCP (The console, the SDK, The app and Apis
- GCP Console is a web based admin which lets you view and manage all projects, it also has cloud shell which is a temporary VM with SDK installed
- The SDK is a set of tools that can be uised to manage tools and resources on GCP. Easiest way is to get there using cloud shell
- You can also install the SDK on any other computer – its avaliable as a docker imag
- APIs are available with Oauth authentications and use JSON as an interchange format it can be enabled through the GCP console
- You can turn off and on APIs using the GCP console, many are disabled and subject to rates and quotas.
- Google offers an API explorer and Client libraries in each language for APIs

_ **Cloud Marketplace** _

- Tool for quickly deploying functional software packages on GCP
- Gives quick access to solutions, most software pacakages have no additional charge, but some have usage fees

_ **Cloud Launcher Lab Intro** _

- Deploying a LAMP stack (linux, apache mysql and php)
- We can use this to deploy it into a Compute Engine instance
- In the console, go on cloud launcher then search for LAMP, then click launch on compute engine.
- Accept defaults and click on deploy, when the deployment is finished the console will display information and you can access the website
- You can log into the vm using ssh and go to the dir where the software is installed and you can copy in a test page for php
- You can then see the php test page on the website.

**Virtual Machines and Networks in the Cloud**

_ **Virtual Machines and Networks in the Cloud** _

- Each Virtual Private Cloud network is contained in a GCP project, you can provision cloud platform resources, connect them to each other and isolate them from one another.
  - VPC netowrks connect the google cloud platform resources to each other and to the internet
  - Many users get started with GCP and define their own virtual private cloud inside their GCP project
- Google Cloud VPC networks are global, whilst subnets are regional
  - Google virtual private cloud networks that you define have gloval scope
  - The private networks can have subnets in any GCP region worldwide, and can span zone in a region
  - Subnet size can be dynamically increased by expanding the range of IP addresses allocated to it
- Compute Engine offers managed virtual machines with high cpu and memory and persistent disks, you can also resize disks with no downtime and instance metadeta and startup scripts
  - A VM running on Google cloud has unmatched worldwide network connectivity
  - You can create a VM instance using the GCP console and can run linux or windows server images
  - Compute engine bills by the second, and there are discounts for VMs that run for a substantial fraction of the month
  - If you have a workload that is not priority, you can save money by using a Preemptible VM
  - A Preemptible VM is different that an ordinary Compute engine VM because they can terminate it if the resources are needed elsewhere. This way you can save a lot of money
  - To use this type of VM then make sure that the job is able to be stopped and restarted
  - You can also choose the machine properties of instance, like the number of virtual CPUs and the amount of memory.
- Autoscaling in Compute engine allows for resilient scalable applications, while you can also use big VMs for memory and compute intensive applications
  - Huge VMs are great for workloads like in-memory databases and CPU-intensive analytics
  - Autoscaling is good for load metrics and balancing incoming traffic among the VMs, google VPC supports several kinds of load balancing.
- The topology of your VPC network is controlled by you, you can use the route table and firewall to contol traffic in the network – and the shared VPC can share this subnet with other GCP projects
  - VPCs have routing tables that are used to forward traffic from one instance to another in the same network, even across subnetworks and between GCP zones. This can be done without an external IP address – you don&#39;t have to manage a router.
  - You don&#39;t have to provision a firewall etiher, VPCs give a global distributed firewall, and firewall rules can be defied easily using metadata tags like &quot;WEB&quot;
  - VPCs belong to GCP projects, you can establish a perring relationship between two VPCs so that they can exchange traffic.
  - However, if you want to still use IAM to control who and what in on project can interact with a VPC in another, its best to configure a Shared VPC
- Global Cloud load balancing can be used to present a single front end to the world, users get a single global IP address and Traffic goes over the Google backbone from the closest point to the user. Backend can then be selected based on load and only healthy backends receive traffic
  - Cloud load balancing is a fully distributed software defined managed service for all traffic, they&#39;re not run in VMs so they don&#39;t need to be managed, you can put them in fron of all traffic
  - With Cloud load balancing, a single anycast IP front-ends all backend instances in regions around the world – providing cross-region load balancing including automatic multi-region failover.
  - No pre-warming is required, scaling reacts to spikes in demand.

![](RackMultipart20210217-4-1tzfxjl_html_777da8ee44c5e0fc.png)

- There are different types of load balacing, lioke Global HTTPs, Global SSL Proxy, Global TCP Proxy, Regional and Regional Internal
  - For web applications, you can use HTTP load balancing.
  - For Secure Sockets Layer traffic, you can use the Global SSL Proxy load balancer
  - If its other TCP traffic that does not use SSL, use the global TCP Proxy Load balancer
  - If you want to load balance traffic on any port, you can load balance across a region with the regional load balancer.
  - You can load balance traffic inside the project you can use the internal load balancer, which accepts traffic on a GCP internal IP address and load balances it across Compute Engine VMs.
- Cloud DNS is highly available and scalable, you can create managed zones, and then add, edit, delete DNS records. You can programmatically manage zones and records using RESTful API or command-line interface
  - GCP offers Cloud DNS to help the world find interanet hostnames and addresses of application you build in GCP.
  - Cloud DNS is a managed DNS service running on the same infastructure as google, it has low latency and high availability – it&#39;s a cost effective way to make applications and services available to you users
  - Cloud DNS is programmable, you can publish and manage millioons of DNS zones and records using the GCP console, CLI or API
- Cloud CDN (Content Delivery Network) uses google&#39;s globally distributed edge caches to cache content close to users, you can also use CDN interconnect if another CDN is preferred
  - Google has a global system of edge caches, this system can be used to accelerate content delivery in the application using google cloud CDN

![](RackMultipart20210217-4-1tzfxjl_html_df4add2992619d6c.png)

- GCP offers many interconnect options, such as VPNs, Direct Peering, Dedicated Interconnect, Carrier Peering, Partner Interconnect
  - To make VPN connections over the internet dynamic, customers can use a GCP feature called cloud router which lets other networks and your google VPC exchange route information over the VPN using the Border Gateway Protocol
  - Some customers don&#39;t want to use the internet due to security concers, in which case they can use Direct Peering, meaning putting a router in the same publci dataceter as a google point of presence and exchanging traffic.
  - Dedicated Interconnect is convered by a google service level agreement, unlike direct peering. They are for customer who want the highest uptimes of interconnection, and can also be backed up by a VPN for greater reliabilitry
  - Partner interconnect provides connectivity between on presmises network and your VPC network through a supported service provider. This is useful if your data center is in a physical location that can&#39;t reach a dedicated interconnect colocation facility. Depending on your availablity needs you can configure partner interconnect to support mission critical services or applications that can tolerate downtime. These connections also are covered by Google&#39;s Service Level Agreement.

_ **Introduction** _

- We will learn of google compute engine works with a focus on virtual networking
- VMs have the power of an operating system

_**Virtual Private Cloud (VPC) Network**_

- You can define your own or choose the default
- VPC networks connect GCP resource to each other and to the internet
- You can segment networks, use firewalls and use static routing
- VPC have global scope, they can have subnets in any region and can span regions/zones
- You can dynamically increase size of a subnet by increasing the range of Ips

_ **Compute Engine** _

- Compute engine lets you create and run VMs, with no up front investments.
- VMs can be created using GCP interfaces
- You can define your own VM to suit your needs
- You can also choose storage for your VMs, and a boot image
- You can define your own startup scripts gor GCP VMs
- Once VMs are running you can take snapshots of disks and backups
- You can save money with Premtible VMs, giving Compute Engine permission to terminate if their resources are needed elsewhere, but your job needs to be not priority, and needs to be able to be stopped and started
- You can scale up or scale out, scaling up by having big vms, or scaling out by distributing across lots of vms
- Autoscaling can help with scaling out by using load balancing

_ **Important VPC Capabilities** _

- VPCs have routing tables to forward traffic in the same network, without requiring an external ip address
- You don&#39;t have to provision your own routing, or your own firewall but you can control them and define your own rules
- VPCs belong to GCP proejcts, if the VPCs need to talk to each other you can establish a peering relationship – you can also use a shared VPC to implement IAM
- VMs can autoscale using cloud load balancing, they don&#39;t run in VMs you have to balance so don&#39;t have to be self configured, you can just put them in front of traffic you want to balance.
- A single IP can then front end all instances across the world.
- You can have multi-region failover
- Reacts quickly to changing conditions, such as spikes in demand.
- Load Balancing for a web application can use Global HTTPs load balancing, You can also use SSL and other TCP proxy load balancers
- For Balancing on any port number you can use load balance across a GCP region
- You can also load balance internally.
- DNS translates host names to addresses
- GCP offers cloud dns for hostnames that you build in GCP, it&#39;s a manged DNS service with low latency and high availablity
- Cloud DNS is also programmable through the GCP console
- Google has a global system of edge caches, which can be utilised using Cloud CDN (Content Delivery Network)
- You can also use other CDNs
- Lots of customers want to interconnect other networks to google VPCs
- Customer can use a VPN, this can be made dynamic using cloud router which lets your other networks and google gcp exchange route information over the VPN using the border gateway protocol
- If customer do not want to use the internet, they can use Peering
- Peering means putting a router in the same data centre as a point of presence, and exchanging traffic.
- Customers who aren&#39;t already in a point of presence can contract with partners to use carrier peering
- A downside of peering is that it isn&#39;t covered by a google service level agreement
- Customers who want highest uptime should use dedicated interconnect, where customers get one or more direct private connections to google

_**Getting Started with Compute Engine (Lab Intro)**_

- Create two VMs using compute engine and connect between them using different protocols
- First create a VM using the GCP console
- Modify its firewall to allow HTTP access
- You can also do it via cloud shell
- You can put the second VM in the same region but a different zone
- You can set your default zones for new virtal machine
- Use the gcloud command to create a new virtual machine
- Ssh into vm2 and ping vm1
- Now log into vm1
- Install a webserver on VM1
- Edit the default homepage to include a custom message
- Use curl to get webpage
- Myvm2 can also see the webserver


**Storage in The Cloud**

_ **Storage in the Cloud** _

- Google Cloud Platform has many storage options that satisy nearly every use case, mainly Google Cloud Storage, Google Cloud SQL, Google Cloud Spanner, Cloud Datastore and Google Cloud Bigtable
- Cloud Storage is binary large-object storage that is High performance, Has Simple administration that doesn't require capacity management. it has data encryption at reast and in transit
  - offers highly available object storage with no minimum free, you only pay for what you use
  - object stroage is different to file storage because you can store an arbitrary sequence of bytes and address it with a unique key, in the form of a URL
  - Cloud storage always encrypts the data on server side before it is written to disk
  - data traveling between a customers device and google is encrypted by default using HTTPS/TLS
  - Cloud storage is not a file system, although it can be accessed as one via third party tools
  - The storage objects are immuatable, they are not edited in place but instead a new version is created.
  - The primary use of cloud storage is whenever binary large-object storage is needed, like online content, backups and archiving.
  - Offline Media import/export is a third party solution that allows you to load in data by sending physical media t a third party service who does it on you behalf
  - offline import is helpful if your internet is limited
  - Cloud storage transfer service enables you to import large amount of online data into cloud storage quickly and cost-effectively
  - To use the transfer service, you can set up a transfer from a data source to data sink
  - examples of cloud storage are backing up data or moving data from standard storage bucket to a nearline storage bucket to lower costs
- Cloud storage files are organised into buckets, buckets have globally unique names, a storage class, a location, IAM policies, Object versioning and Object lifecycle management
  - When you create a bucket you give it a name, a location and a default storage class.
  - you can control users access to objects and buckets, for most purposes cloud IAM is sufficient, roles are inherited from project to bucket to object
  - If you need finer controler, access control lists can be used, which define who has access to buckets/objects and what that level is
  - each ACL consists of a scope (defining a user or group of users) and a permission (defining what actions can be performed)
  - Cloud storage objects are immutable, and you can turn on object versioning
  - object versioning allows for a history of modifications (overwrites/deletes) you can restore an object or permanently delete an object, without versioning new always overwrites old with no history.
  - Cloud storage offers lifecycle management policies, such as deleted objects older than a certain date, or keeping 3 most recent versions of an object.
- You can choose four different types of classes in cloud storage (Multi-regional, regional, nearline and coldline) multi-regional and regional are high-performance whilst near/coldline are backup/archival storage
  - Regional Storage lets you store you data in a specific GCP region, it's cheaper than mult-regional but offers less reducnancy
  - Multi-Regional storage is more expensive but it is geo-redundant. It is appropriate for storing frequently accessed data like online content. Regional storage is used for performance on computation.
  - Nearline Storage is low-cost durable storage for infequently accessed data. 
  - Coldline Storage is very-low-cost durable storage for archiving, online backup and disaster recovery. it is the best choice for data you plan to access for at most once a year.
  - Multi-regional storage has the highest avaliablility, followed by regional then near/coldline. 
  - All storage classes incur a cost per gigabite of data store a month, nearline and coldline also incurs a fee per gigabyte of data read.
- There are several ways to bring data into Cloud storage, like online transfer, storage transfer service or transfer appliances
  - Many customers simply use gsutil (The cloud storage command from cloud SDK). You can also drag and drop in the GCP console if you use chrome.
  - For larger amount of data there are online storage transfer service and offline transfer appliance.
  - The storage transfer service lets you schedule and manage batch transfers to cloud storage from another provider/cloud storage region/HTTPs enbdpoint
  - The transfer appliance in a rackable, high-capacity storage server that you lease from google cloud, you connect it to you network and load in the data, allowing you to tranfer up to a petabye of data. (in beta)
- Cloud storage works with other GCP services, like BigQuery, App Engine, Compute Engine and Cloud SQL
  - Cloud storage is tightly integrated wit many GCP services
  - You can import and export tables from and to BigQuery, as well as Cloud SQL
  - You can also store App ENgine logs, Cloud Datastore backups, and objects used by App Engine applications (like images)
  - Cloud Stroage can also store instance startup scripts, Compute Engine images and objects used by Compute Engine applications
  - Cloud Storage is often the ingestion point for data being moved into the cloud, and it frquently the long-term stoarge location for data.
- Cloud Bigtable is managed NoSQL, wide-column database service for terabyte applications, Its integrated accessed using HBase API, Native compatibility with big data, hadoop ecosystems
  - it is offered as a fully managed service, so it doens't need to be configured, Google has its own operations team to monitor the service
  - Cloud Bigtable is ideal for application that need very high throughput and scalability for key/value data, where each value is no larger than 10MB.
  - It also excels as a storage engine for batch MapReduce operations, stream processing/analytics and machine-learning applications.
  - You can use Cloud Bigtable to store and query Marketing data, Financial data, IOT data and Time-series Data
- Cloud Bigtable is good because it is replicated storage, data encryption in flight and at rest, has role based ACLs and it drives major google applications
  - Customers frequently choose Bigtable if the data is Big, Fast, and is NoSQL compatible (transactions, strong relational semantics not required)
  - it is especially good if the data is a time series/ has a natural semantic order, the data is BIG, or you run machine learning on the Data
  - Bigtable is designed to handle massive workloadd at consistent low latency and high throughput, so its a great choice for both operational and analytical applications.
- Bigtable Access Patterns include the application API, streaming and batch processing
  - From an application API perspective, data can be read from and written to cloud bigtable through a data service layer like Managed VMs, typically this will serve data to applications/dashboards
  - Data can also be streamed in through a variety of popular stream processing frameworks (like cloud dataflow streaming, spark streaming and storm).
  - If streaming is not an option, data can also be read from and written to cloud bigtable through batch processes like Hadoop, MapReduce, Dataflow, or Spark.
- Cloud SQL is a managed RDBMS, offers MySQL/Postgres as a service, with automatic replication, managed backups, vertical/horizontal scaling and google security.
  - Cloud SQL is an easy-to-use service that delivers fully managed relational databases.
  - Google manages patches, updates, backups and replications of the database.
  - Every instance of Cloud SQL has a network firewall that is configurable
  - CLoudSQL doesn't require any software installation and can easily scale up to 64 processor cores and more than 100GB RAM.
  - Cloud SQL has automatic replication, for scenarioes when replicating from an internal master instance, external master instance, or external MySQL instances.
  - Cloud SQL manages backups, it takes care of securely storing it and makes it easy to restore from a backup. Cloud SQL retains up to 7 backups for each instance.
  - Cloud SQL cutomer data is encrypted when on google's internal networks and when stored in databse tables/temporary files and backups.
- Cloud SQL can be used with other GCP services, like App engine, Compute engine, or external applications and clients.
  - You can use Cloud SQL with app engine using standard drivers like Connector/J for JAva or MySQLdb for Python
  - you can authorise compute engine instances to access cloud SQL instances and configure the cloud SQL instance to be in the same zone as your VM
  - Cloud SQL also supports other application and tools like SQL Workbench, Toad and other external applications using standard MySQL drivers
- Cloud Spanner is a horizontally scalable RDBMS that supports automatic replication, strong global consistency, managed instance with high availability.
  - Cloud Spanner supports strong consistency, including strongly consistent secondary indexes, SQL and managed instances with high availability thourhg synchronous and built-in data replication.
  - Cloud Spanner is especially suited for applications requiring an SQL RDBMS, built in high availability, strong global consistency, database sizes exceeding 2TB
- Cloud Datastore is a horizontally scalable NoSQL DB, is is designed for application backends and is fully managed, using a distributed architecutre for scaling, supports ACID transactions and has built-in redundancy
  - Like BigTable, there is no need for you to provision database instances, Cloud Datastore uses a distributed architecture to automatically manage scaling, queries scale with size of results set.
  - Cloud Datastore runs in google data centres which use redundancy to minimise impact from points of failure
  - The total size of cloud datastore databases can grow to terabyte and more.
- Google Cloud Datastore benefits from schemaless access, local development tools, a daily free quota and access from anywhere through a RESTful interface
  - Atomic transactions, Datastore can execture a set up operations where either all or non occur
  - High Availability of reads and writes, datastore runs in google data centres, which use redundancy.
  - Massive scalability with high performance, Datastore uses a distributed architecture to automatically manage scaling. it uses a mix of indexes and query constraints so the queries scale with size of results set (not data set)
  - Flexible storage and quering of data, maps naturally to object-oriented and scripting languages and is exposed to applications through multiple clients.
  - Balance of strong an eventual consistency, ensure that enity lookups and ancestor queries always receive strongly consistent data. allows you application to deliver a great user experience with large amounts of data/users
  - Encryption at rest, Datastore automatically encrypts all data before it is written to disk and automaticall decrypts when read by an authorised user.
  - Fully managed with no planned downtime, Google handles the administration of the datastore service so you can focus on you application. You application can still use datastore when the service recieves and upgrade.
- Comparing storage options, between Cloud Datastore, Bigtable, Cloud Storage, Cloud SQL, Cloud spanner and BigQuery
  - Considering Cloud Datastore, if you need to store structured objects or if you requries support for transactions and SQL like queries. This store provides terabytes of capacity with a max unit size of 1MB
  - With Cloud Bigtable, if you need to store a large amount of structured objects, it doesn't support SQL queries or multi row transactions. Provides petabytes of capacity with a max unit size of 10cm per cell 100mb per row.
  - With Cloud Storage, if you need to store immuatable blobs larger than 10MB (such as images/movies). This storage serivce provides petabyes of capacity with a max unit size of 5TB per object
  - Consider using Cloud SQL or Cloud Spanner if you need full SQL support for an online transaction processing system
  - CLoud SQL provides up to 10230GB depending on machine type, whilst CLoud Spanner provides petabytes. If you need horizontal scalability, not just replicas, consider using cloud spanner.
  - BigQuery sits on the edge between data storage and data processing, you would want to use it for big data analysis and interactive querying capabilities.
- Considering storage option use cases
  - CLoud Datastore is best for semi-structured application data that is used in App Engine applications
  - Bigtable is best for analytical data with heavy read and write events.
  - Cloud Storage is best for structured and unstructured binary or object data (like images, large media files and backups)
  - Cloud SQL is best for web frameworks and existing applications, like storing user credntials and customer oders.
  - Cloud SPanner is best for large-scale database applications that are larger than 2TB ( for example, for financial trading and ecommerce use cases)

_ **Introduction** _

- every application needs to store data
- different applications and workloads require distance storage
- you can store data on your VMs persistent disk but there are other storage options
- The core storage options are Cloud Storage, CloudSQL, CLoud Spanner, Cloud datastore and google bigtable.

_ **Google Cloud Storage** _

- Object storage is not the same as file storage or block storage, it is an arbitrary bunch of bytes at a unique key/address
- These addresses are stored as URLS, its a fully managed scalable service, you don't need to define a size, it sizes dynamically
- Can be used for backups, distributing large data objects, or web frameworks.
- it isn't a filesystem, each object is a URL.
- You would not use it as the root filesystem of your linux box
- Consists of Buckets with storage objects in them, the storage objects are immutable, you create new versions not edit them in place.
- All objects are encrypted at rest and in transit
- There are services you can use to get large amounts of data into cloud storage
- once in cloud storage, the data can be easily moved to other GCP products
- When you create a bucket, you give it a globally unique name and specify a location and a storage class.
- You can control access to objects and buckets using cloud IAM
- You can also have ACLs with scope and permissions for finer controlled access to items.
- You can turnon object versioning to track the history of modifications to any objects.
- You can define lifecycle management, by deleting old objects or having a max amount of object history.

_ **Cloud Storage Interactions** _

- There are four types of storage classes, regional, multiregional, newline and coldline
- mult/regional are high performance, and new/coldline are for infrequent access and backups
- all are accessed through the cloud API
- Regional allows for data storage in a specific region, it is cheaper for mult-regional but doesn't have redundancy
- Multi-regional allows for geo-redundancy, it is aprorpriate for accessing frequently accessed data.
- Regional is used to store data close to their VMs for data intensive computations
- Nearline storage is a low cost highly durable storage for infrequently accessed data, for maybe once a month.
- coldline storage is a very low cost highly durable storage for infrequently accessed data, for maybe once a year.
- all storage classes have cost per gb of data, nearline and coldline also has an access fee per gigabyte read
- There are several ways to bring data into cloud storage, like online transfer, storage transfer or transfer appliances.
- You can drag and drop in the GCP console
- to upload terabytes of data, you can use online storage transfer service or the offline transfer appliance
-  Storage transfer has scheduled managed batch uploads.
- the transfer appliance is a rackable server leased from google cloud that is connected to the network, loaded with data and then shipped to a datacenter where the data is uploaded to cload storage.
- You can also get data into cloud storage from other GCP applications, like BigQUery, App Engine, Compute ENgine and CLoud SQL

_ **Cloud Bigtable** _

- NoSQL bigdata database service
- not a relational database, no rows with same sets of columns, there is no enforced schema, a much more flexible approach.
- Bigtable is a managed NoSQL wide column database service for terabyte applications, ideal for data that has a single lookup key
- Bigtable is a persistent hashtable, supports high throughput, good for operational and analytical applications
- Offered throught the same api as Hadoop
- Having the same API allows portability of application between the two
- Bigtable is easily scalable, you can increase your machine count and this doesn't incur downtime.
- All data in cloud Bigtable is encrytped at rest and in flight.
- Bigtable is the same database that powers many of google core services
- Can interact with other GCP services and thrid party clients
- Data can be streamed through a variety of popular frameworks
- Can be written and read from using mapreduce, dataflow or spark

_ **Cloud SQL and Cloud Spanner** _
- These services use consistent database schemas
- Keeps data consistent and correct, and can have transactions
- Cloud SQL are fully managed with SQL or Postgres database engines, capable of handling terabytes or storage.
- Benefits of CloudSQL, they have automatic replication, can replicate data between multiple zones with automatic failover
- Has managed backups
- Has vertical scaling (Read and write) and horizontal scaling (read)
- Google security with encrypted data at rest and in transit and firewall.
- Accessible by other GCP services and external services
- Can authorise instances to use cloudsql
- Cloud Spanner offers transactional consistency at a global scale, schemas, sql and automatic synchronous replication
- can provide petabytes of storage
- consider spanner if you have outgrown any other relational database, are sharding database for throughput high performance, need transactional consistency, or just want to consolidate.

_ **Cloud Datastore** _

- Highly scalable nosql database
- main use case is to store structured data from app engine apps
- can also build solutions that span app engine and compute engine with cloud datastore as the integration point
- automatically handles sharding and replication, scales automatically to handle load
- unlike cloud bigtable, it also offers transactions athat effect multiple database rows
- free daily quota to get you started.

_ **Comparing Storage Options** _

- CLoud datastore for unstructured objects or support for transactions and SQ like queries, provides terabytes of capacity
- Cloud bigtable for a large amount of unstructured objects, does not sql queries, or multi row transactions - provides petabytes of capacity
- Cloud storage for immutable blobs larger than 10MB, like moves provides petabytes of capacity with a max unit size of 5tb
- Cloud sql/spanner for full SQL support for online transaction system, sql provides Tbs, spanner provides Pbs
- Cloud spanner is best for horizontal scalability
- BigQuery isn't covered here, its used for bigdata analysis
- Cloud datastore is the best for semi-structured application data that is used in app engine applications
- Big table is best for analytical data, or financial data with heavy read/write events
- Cloud Storage is best for structured/unstructured binary or object data
- Cloud SQL is best for web frameworks or existing application
- Cloud spanner is best for large scale web frameworks


_ **Getting started with cloud storage and cloud SQL** _

- First we create a web server
- create an instance
- name it bloghost, leave it in default zone and keep other defaults
- allow https traffic in
- add a startup script, which will install a webserver
- make a cloud storage bucket using cloud shell
- enter gsutil mb -l US (us multiregion) name of bucket must be globally unique, name it after VM project id because its unique
- copy graphical image from other storage bucket called cloud training
- use gsutil to upload to own cloud storage bucket
- create a cloud sql instance in the same zone as VM instance
- choose Mysql for database engine, name the instance blog-db and define a root password, then place it in the same zone as vm
- click on db name to configure it
- create mysql username and define a password
- configure db so it can be only contacted from vm instance
- capture vm instance public ip address
- return to SQL instance and put into authorization the name and ip
- now db instance is protected from public access
- return to vm and configure to use resources that were set up, log in using SSH
- edit the php homepage, add in page
- fill in db ip and password
- restart web server daemon
- return to GCP console and attempt to view the homepage
- to add image to webpage, firstly naviagte to storage broswer and create public link for image
- clone the hyperlink, return to php homepage and add in html reference to that image
- restart web server, return to php homepage and refresh - it now contains the image.



**Containers in the Cloud**

_ **Containers in the Cloud** _

- We have Infastructure as a service (IaaS) and Platform as a service (PaaS), compute engine is stricty IaaS, but kubernetes is a hybrid of the two
  - another choice for ogranising your compute is to use containers rather than VMs
  - You can use kubernetes engine to manage these containers
  - containers are simple andd interoperable, enabling seamless fine grained scaling
- Virtual machines rely on hypervisor based virtualisation, by having a hypervisor and a guest os between the hardware and the guest OS, containers just use a container runtime on the kernel
  - Container based virtualisation is an alternative to ahrdware virtualisation
  - VMs are isolated from one another as each VM has its own instance of the OS
  - OSs can be slow to boot and resource heavy
  - Containers respond to these problems by using modern OSs built in capabilities to isolate environments from one another
  - Containers take advantage of the ability to give processes the ability to have their own namespaces and give a supervisor process to limit the process' access to resouces
  - Containers start much faster than virtual machines and use fewer resources.
  - Developers configure each container with a minimal set of software libraries to do the job
  - Kubernetes engine uses the docker container runtime
  - a process is a running program, with memory address spaces isolated from one another
- Containers are preferable because they provide consistency across environments, losse copling between app and OS layers, Easy workload migrations and easy agile development and operations.
  - A container provides simple deployment, by packaging the application as sa singularly addressable, registry-stored, one command line deployable component
  - It has rapid availability, by abstracting the OS instead of the whole physical computer, it boots much faster than a VM.
  - Containers all developers to further subdivide compute resources into microservices
  - developers find that the compute power in their laoptop is plentyu enough to run many containers, much more than the amount of VMs they can run
  - Pushing new versions is much easier and testing is cheaper because less resources are used in the cloud.
  - you can also easily store applications and their dependencies without conflicting dependencies.
- Kubernetes is a container cluster orchestration system, which automates deployment, scaling and operations for container clusters
  - google built it and then made it open srouce
  - it is an orchestration layer for containers
  - kubernetes eases application management
  - it has workload portability, you can run it in many environments across bloud providers, and its implementation is open and modular
  - it has rolling updates, you can upgrade applications without downtime
  - it has persistent storage, the details ofhow storage is provided are abstracted from how it is consumed
  - it runs in many environments
  - the kubernetes APi and its implementatio are open source
  - the whole system is modular and replacable
  - you can build apps locally and then lift and shift wthese apps to the cloud when you are ready
  - it is cloud vendor agnostic, not just tied down to GCP.
  - Kubernetes makes applications more elastic, by allowing a cluster to be ran in multiple zones, implementing load balancing and autoscaling
- Kuberenetes Engine manages and runs containers, it is a fully managed system based onb kubernetes which uses compute engine instances, it uses a decalarative syntax to manage applications
 - it is kubernetes as a service
 - kubernetes engine is a scalable managed offering that runs on google infstructure
 - you direct the creation of a cluster and kubenetes engine schedules your containers into the cluster and manges them automatically
 - it decouples operational and developmental concerns, it manages and mantains the cluster by logging, health management and monitoring
 - you can easily update kubernetes versions as they are released
- Kubernetes Engine has complementary services like the google cloud container builder, allowing you to create docker container images from app code, you can also use the google container registry (private image storage)
  - container builder lets you careate docker container iamges from application source code located in Cloud stroage
  - container images created by container builder are automatically stored in container registry, you can deploy the images you create on kbuernetes engine
  - Container registry provides private docker image storage on GCP.
  - although docker provides its own central registry to store images, you may want thes images to be private
  - the registry can accessed through an HTTPS endpoint, so you can pull images from any machine
  - container registry only charges for the cloud storage storage and network egress consumed by your docker images

_ **Introduction** _

- Another choice for organising your apps is using containers and using kubernetes to manage them
- containers are simple and interoperable
- they enable symless fine grained scaling
- Kubernetes is an orchestration layer for containers develpoed and realeased as opne source by google
- kubernetes engine is kubernetes as a service, you can run kubernetes on your own premises and in other clouds too
- kuberenets engine runs on googles infastrutcture.
- there is a spectrum beteween Iaas and Paas, compute engine being Iaas and app engine being Paas
- kubernetes is a hybrid of the two.

_ **Introduction to Containers** _

- Container based virtualisation is an alternative to hardware base virtualisation
- VMs are isolated from each other by having their own operating systems, but this is resource heavy
- containers use OSs ability to isolate processes from one another
- containers start much faster than virtual machines and use a ot less resources
- containers offer consistency, loose coupling, workload migration and agility
- containers are easy to move around, both in life cycle cases and between local and cloud environments
- it allows you to develop continuously, one of the hallmarks of agile development

_ **Kubernetes** _

- Containers needs a manager to scale and manage
- google built kubernetes to do this and it is now open source
- the portability of containers and kubernetes allows it to be used in multiple cloud environments
- a kubernetes pod is a group of containers that are deployed together with guaranteed netweek access, this helps develpoers build modularly
- kubernetes can run in many environments
- kubernetes API is completely open  
- after application is deployed on kubernetes, you can do a rolling update, which incrementally replaces resources and pods with new onces
- a kubernetes cluster is a group of machines where kubernetes can schedule containers
- those machines are called nodes
- clusters can have nodes spread across zones to give better resiliency

_ **Kubernetes Engine** _

- lets you build manage and link kubernetes clusters
- the resources used to build these clusters come from compute engine
- for example, cluster nodes are compute engine virtual machines
- master for each cluster runs in a compute engine virtual machine too.
- kubernetes engine gets to take advantage of compute engine and googles VPC capabilities
- kubernetes is declarative, you give it a description of the cluster environment you want and kubernetes changes the environment to make it happen
- you don't have to issue the underlying compute engine commands or API calls.
- Kubernetes engine is good because it is a managed service, relieving develpoers from operational details
- it has built in logging and monitoring capabilities
- google keeps it refreshed and updated
- GCP offers Google Cloud Container builder, to help create container images, and container registry to help privately store these images
- you can manage both these tools using the google cloud access, and IAM just like any other GCP resource.

_ **Getting Started with Kubernetes Engine** _

- use GCP confirm APIs we need are available
- go to api and services dashboard
- look for kubernetes api and container registry api
- check both are enabled
- activate the cloud shell, define an environment variable with your prefered GCP zone
- launch a kubernetes cluster in that zone
- give it two nodes
- confirm what version the cluster is running
- go back to gcp console to view nodes
- go to vm instances to see them
- you can view the cluster in the kubernetes engine console aswell
- return to cloud shell, run a webserver in the cluster
- confirm the pod is running
- expose the deployment so clients access kubernetes can access
- view the new service
- visit ip address in web broswer
- scale the deployment, using replicas
- look at the new number of pods
- confirm that the external ip address did not change
- refresh the homepage


**Applications in the Cloud**

_ **Applications in the Cloud** _

- Google App Engine is a Paas for building scalable applications, it makes deplymnet, maintainence and scalabiltity easy and is especially suited for scalable web apps and mobile backends
  - App Engine manages the hardware and networking infastructure required to run your code.
  - it provides you with built in services and APIs such as NoSQL datastores, memchache, load balancing, health checks, application logging and user athenticaion APIs
  - App engine will scale your application atuomaticcaly in response to activity, there are no servers for you to provision or maintain
  - Security scanner automatically scans and detects common web app vulnerabilities enabling threat identification and delivering low falsse postivie rates.
  - App engine works with popular dev tools like Eclipse, IntelliJ, Maven, Git, Jenkins, PyCharm.
- The App Engine standard environment allows you to easily deploy your applications, autoscale workloads to meet demands, is economical and has SDKs for dev, testing, deployment.
  -  the enviornment is based on container instances running on google's infastructure,
  - the containers can be preconfigured with one of many available runtimes (Java 7, Python 2.7, Go, PHP)
  - for many applications, the standard environment runtimes and libraries may be all you need.
  - the app engine environment makes it easy to build and deploy an application that runs reliably even under heavy load and with large amounts of data. 
  - the environment has persisten storage with queries, sorting and transactions
  - it has automatic scaling and load balancing
  - it has scheduled tasks for triggering events ant specified times
  - it is integrated with other google cloud services and APIs
  - specific versions of Java, Python, PHP and Go are supported
  - the application must conform to sandbox constraints of not writing to the local file system, requests timing out after 60s and limited thrid party installs
  - Software development kids for app engine are available 
  - each sdk includes all the APIs available to app engine, a simulated secure sandbox environment, and deployment tools to upload to application to the cloud
  - The SDK manages your application locally, and GCP console manages it in production
  - apps run in a secure sandboxed environment, allowing the app engine environment to distribute requrests across multiple servers, and auto scaling servers.
- the app engine can easily be used for web applications.
  - You develpop and test the web application locally
  - You use the SDK to deploy it to App Engine
  - App Engine automatically scales and reliably serves the web app
  - app engine can access a variety of services using dedicated services and APIs
  - Each app engine app runs in a GCP project, app engine automaticall provisions server instances and scales/load balances them.
  - Meanwhile, your application can make calls to a variety of services using dedicated APIs
  - For Example, a NoSQL datastore to make data persistent, caching is using memcache, searching, logging, user login and the ability to launch actions not triggered by user requests (task scheduling)
- The App engine flexible environment allows you to build and deploy containerised apps with a click with no sandbox constraints, can access app engine resources, has standard runtimes and custom runtime support
  - Instead of the sandbox in the standard environment, it lets you specify the container you appliccation runs in
  - your application runs inside docker containers on the google compute engine VMs
  - App engine manages these compute engine machines for you, theyre health checked, and you get to choose what geographical region they run in.
  - microserves, authroisatiojn, SQL and noSQL databases, trafic splitting, logging, versioning, security scanning, memcache and content delivery networks are all supported natively.
  - App Engine flexible environment allows you to customise your runtime and the operating system of your VM using dockerfiles
  - The flexible environment includes native support for multiple runtimes, but developer can customise their runtimes with their own docker image/ dockerfile
  - Because VM instances in the flexible environment and Compute ENgine, you can use SSH to connect to them for debugging purposes
  - You can take advantage of a wide arrayt of CPU and memory configuratins, by specifying how much CPU/memory your app needs
  - The standard environment starts up faster, but you get less access to the infastructure in which your application runs.
  - Flexible environment allows you to ssh into the VMs, and write to local disk for scatch space
  - Flexible environment allows you to install third party software, and it lets you app make calls to the network without going through app engine.
  - Standard environment on the other hand can have its billing drop to zero for a completely idle application-
- You can deploy apps with app engine or kubernetes, kubernetes is a more manged infastructure, and the standard environment is more dynamic, with the flexible environment being between the two
  - App Engine standard environment is for people whjo want the service to take max control of their applicaion's deployment and scaling
  - Kubernetes Engine gives the application owner  the full flexibility of Kubernetes.
  - App engine flexible edition is between the two
  - App Engine environment treats containers as a means to an end. but for kubernetes engine, containers are a fundamental organising principle
- Google Cloud Endpoints helps you create and maintain APIs, through an API consolem you can expose it using a restful interface and control access/validate calls with web tokens/keys
  - APIs abstract a complex changeable implementation to a simple versioned interface
  - you might have to version an API, which is include in software calls.
  - Supporting an API is an important task and GCP provides two API management tools
  - Cloud endpoints provides an API console, hosting, logging, mointoring and other features to help you create, share, maintiain and secure your APIs
  - You can use cloud endpoints with any APIs that support the OPenAPI specification, formerly known as prince. (the swagger spec)
  - It uses the distributed extensibile service proxy to provide low latency and high performance for demanding apis
  - extensibile service proxy is a service proxy based on NGINX, it runs its own docker container for better isolation adn scalability
  - The proxy is containerised and sitributed in the container registry and can be used with app/kubernetes/compute engine or kubernetes itself
  - Cloud endpoints features user athentication through firebase auth, google auth and auth0
  - it features automated deployment, with app engine the proxy is deployed automatically with your application.
  - It has logging and monitoring to monitor traffic, error rates and latency and review logs in cloud logging. You can use cloud trace to dive into the performance
  - You can generate API keys in the GCP console and validate on every API call.
  - it has easy integration, you can get started quickly by using on of google cloud endpooints frameworks or by adding an open api spec to your deployment.
- Apigee Edge helps you secure and monetise APIs, it is a plotform for making APIs available to customers/partners. It contains analytics,  monetisation and a developer portal
  - Apigee focuses on business problems for APIs like rate limiting, quotas and analytics
  - many users of apigee edge are providing a softweare service to other companies, and those features come in handy.
  - because the backend services for apigee edge need not be in GCP, engineers also use it when they want to take a legacy app apart.
  - Instead of replacing a monolithic application in one risky move, they can instead use apigee edge to peel of its services one by one.

  
_ **App Engine** _

- if you don't want to focus on infastructure at all app engine is the one for you
- app engine is a platform as a service. 
- app engine just takes your code and takes care of the rest
- it provides lots of services that web apps need 
- it will scale your application automatically for the amount of traffic it recieves
- it is best suited for application where the load is highly variable 

_ **App Engine Standard Environment** _

- of the two app engine environments, standard is the simpler
- it offers a simpler deployment expierience and fine grained autoscaling
- it also offers free daily usage quota
- low utilisation might be able to run at no charge
- google provicdes sdks for deployment testing and development
- app engine has a runtime provided by google, you can choose between java python php and go
- standard environment forces restrictions in your code by making it run in a sandbox
- sandbox has contraints of no writing to local files, all requests time out at 60s and limits on third party software
- you develop the app, run it locally using sdk to do so, you then use the sdk to deploy it
- each app engine runs in a GCP project, it automatically scales and load balances them

_ **App Engine Flexible Environment** _

- instead of the sandbox it slets you specify the container your application runs in.
- your app runs inside containers hosted on GCP vms, it manages the compute engine machines for you - you get to choose their geographical region
- use standard runtimes and can access app engine services
- standard starts up faster, but you get less access to the infastructure 
- flexible environment lets you ssh, use local disk, use third party software
- between app engine standard and kubernetes engine
- in app engine environments, containers are a means to an end but in the kubernetes engine containers are the main organising principle


_ **Cloud Endpoints and Apigee Edge** _

- APIs provide a clean versioned interface that abstracts away complex, not needed implmentations
- to make api changes cleanly, apis are versioned
- programs that consume the api can specify the version in their calls
- GCP supply two API management toosl
- Cloud endpoints implements capabilites to make sure the API is only consumed by developers you trust, to log and analyse it
- cloud endpoints uses an easy-to-deploy proxy in front of the software service
- it has an API console to wrap up the capabilities in an easy to use interface
- cloud endpoints supports applications running in GCPs compute platforms
- Apigee is a platform for developing and managing API proxies 
- it is orientated towards business problems like rate limiting, analytics and monetisation
- the backend service may not need to be in GCP, engineers use it when they are taking apart a legacy application


_ **Getting Started with App Engine** _

- open cloud shell
- clone the source code for a simple app engine application from github
- go to the source code, examine app.yaml (which specifies the configuration)
- run the application locally in cloudshell
- use the preview capability to preview it
- deploy the app, choosing the zone
- go to app engine dashboard to see your app
- disable the app using the app engine console settings

**Developing, Deploying and Monitoring in the Cloud**

_ **Developing, Deploying and Monitoring in the Cloud** _

- Cloud Source Repositories are fully featured Git repositories hosted on GCP, they support collaborative development of cloud apps and include integration with stackdriver debugger
  - They provide git version control to support collaborative develpoment of any application or service, including those that run on App Engine of Compute Engine
  - If you are using the stackdriver debugger, you can use Cloud Source Repositories and related tools to view debugging info alongside your code at runtime
  - They also provide a source viewer that you can use to browse and view repo files from within the GCP console
  - Using these you can have any number of private Git repos which allows you to organise the code associated with your cloud project in whatever way works best for you.
  - Google cloud diagnostics tools like the debugger and error reporting can use the code from your git repos to let you track down issues to specific errors without disrupting users
  - If you have already got code in a Git repo, you can bring that into your cloud project and use it just like any other repo, including browsing and diagnostics
- Cloud Functions, create single-purpose functions that respond to events without a server or runtime, it is written in javascript, executed in nodejs on gcp
  - it is a lightweight event-based asynchronous compute system that allows you to to create small, single purpose functions that respond to cloud based events without runtime
  - You can use these functions to construct applications from bite sized buissines logic.
  - You can also use Cloud functions to connect and extend cloud services
  - You are billed, to the nearest 100 milliseconds, only while your code is running.
  - Cloud functions are written in javascript and execute in a managed nodejs environment on GCP
  - Events from cloud storage and Cloud Pub/Sub can trigger Cloud Functions asynchronously, or you can use HTTP invocation for synchronous execution
  - Cloud events are things that in your cloud environment, like changes to data in a database, files being added to a storage system, or a new vm being created
  - Events occur whether or not you choose to respond to them, Creating a response to an a event is done with a trigger.
  - A trigger is a declaration that you are interested in a certain event or set of events, you create triggers to capture events and act on them
- Development manager is an infastructure managemnt service, using a yaml template to describe the environment, it provides repeat deployments
  - development manager is an infastructure management service that automates the creation and management of your GCP resources for you
  - Setting up your environment in GCP can entail many steps, which is why it is more  efficient to use a template.
  - GCP provides a deployment manager to automate the creation and management of your GCP resources for you
  - To use Deployment Manager, you can create a template file, using either the yaml file or python.
    - The template file describes what you want the components of your environment to look like
    - You can then give the file to the deployment manager , which figures out the actions needed to create your environment
    - If you need to change your environment, you can edit the templatek and then tell your deployment manager to update
- Stackdriver is GCP's tool for monitoring, logging, and diagnostics
  - You cannot run an application without monitoring, it lets you figure out if the changes you made were good or bad
  - It lets you respond with information rather than with paniv when your application is down
  - Stackdriver gives you access to many different kinds of signals from your infastructure platforms.
  - it gives you insight into your applications health, performance, and availability, so if issues occur you can fix them faster
  - StackDriver offers capabilities in six areas
    - monitoring (platform metrics, uptime/health checks, dashboards and alerts)
    - Logging (platform logs, log search and filter, view and export)
    - Trace (Latency reporting and sampling, Per-URL latency and statistics)
    - Error Reporting (Error notifications, error dashboard)
    - Debugger (debug applications)
    - Profiler (Continuous profiling of CPU and memory consumption)
  - Stackdriver Monitoring checks the endpoints of web applications and other internet-accessible services running on your cloud environment.
    - you can configure uptime checks associated with URLs, groups or resources, such as instances and load balancers
    - You can set up alerts on interesting criteria, like when health check results or uptimes fall into levels that need action
    - You can use Monitoring with a lot of popular notification tools.
    - and you can create dashboards to help you visualise the state of your application
  - Stackdriver Loggin lets you view logs from you applications, and filter and search them
    - Logging also lets you define metrics based on log contents that are incorporated into dashboards and alerts
    - You can also export logs to BigQuery, Cloud Storage, and Cloud Pub/Sub
  - Stackdriver Error Reporting tracks and groups the errors in your cloud applications, and it notifies you whenn new errors are detected
  - Stackdriver Trace allows you to sample the latency of app engine applications and report per-URL statistics
  - Stackdriver Debugger offers a less painful way of debugging
    - it connects your applications production data to your source code, so you can inspect its state of your appplication at any code location in production
    - this means you can view the application state without adding logging statements
    - it works best when your applications source code is available, such as in cloud source repositories.
  - Stackdriver Profiler is a statistical, low-overhead profiler that continously gathers CPU usage and memory-allocation information from production applications
    - To profile an application is to look at its execution of a program and observe the patters between functions, how much CPU time and memory is used.
    - Stackdriver Profiler attributes the information to your applications source code, helping you identify the parts of the application using the most resources
    - the stackdriver profiler is in beta stage, and therefore is not covered by SLA or depreciation policies, and may be subject to backward-incompatible changes

_ **Development in the cloud** _
  - Cloud source properties keeps code private to a GCP project
  - cloud source properties allows you to have any number of private git repos, allowing you to organise code
  - it contains a source viewer where you can browse code in the repo
  - cloud functions allows you to run basic code when new things happen
  - they create single purpose functions in javascript and nodejs, you just pay when the functions run
  - cloud functions can trigger on events 
  - you declare triggers and attach javascript functions to these triggers
  - some microservices can be implemented entirely in cloud functions
  - cloud functions can also enhance already existing microservice structures

_ **Infastructure as code** _
  - setting up the environment can be done with templates
  - deployment manager can be used to provide repeateable deployments
  - this can be done in yaml or python
  - deployment manager interprets the template to create and update the environment
  - you can store these templates in cloud source repositories

_ **Monitoring - Proactive instrumentation** _
  - monitoring lets you figure out the changes you make are good or bad
  - stackdriver is the tool for monitoring logging or diagnostics
  - monitoring, logging, trace, error reporting and debugging are the key components
  - monitoring allows you to configure uptime checks and allows you to set alerts
  - monitoring can be used with a lot of popular loggin tools
  - you can also set up dashboards with monitoring
  - logging lets you view logs and filter and search on them
  - you can also export logs to BigQuery, cloud storage 
  - error reporting tracks and groups errors 
  - it notifies you when new errors are created
  - stackdriver trace has latency reporting and sampling
  - you can get per-URL statistics
  - Debugger can be used to inspect application at any code location
  - it works best when the source code is avaliable in repositories

_ **Lab - getting started with deployment manager and stackdriver** _
  - activate cloud shell
  - define env variable with GCP zones
  - create deployment manager template with text editor
  - create template and paste it in
  - deployment requires you to declare zone and project ID
  - use sed to sub in project ID
  - use sed command to sub in preferred zone
  - build deployment from template
  - confirm status using gcloud command
  - look at resulting vm
  - go to compute engine vm instances page
  - click on name to open details
  - make change to template
  - add command to startup script
  - new command installs nginx
  - update component
  - now update is complete, look at details
  - the startup script has changed
  - put some cpu load on vm and monitor it
  - log into vm
  - use artifical command to make a cpu load
  - return to GCP console and setup stackdriver monitoring
  - confirm you want to create an account
  - confirm you wish to monitor GCP project
  - skip AWS setup
  - no need to install stackdriver monitoring agent
  - dont need to get reports by email
  - launch monitoring
  - continue with trial
  - cpu util has increased sharply

**Big Data and Machine Learning in the Cloud**

_ **Big Data and Machine Learning in the Cloud** _

- Google Cloud's Big data services are fully managed and scalable
  - Cloud DataProc provides managed hadoop mapreduce, Spark, Pig and Hive service
  - Cloud Dataflow provides stream and batch processing, unified and simplified piplines
  - BigQuery is an analytics database allowing streaming of data at 100,000 rows per second
  - Cloud pub/sub allows for scalable and flexible enterprise messaging
  - Cloud datalab allows for interactive data exploration
  - Cloud Big data solutions are integrated serverless platforms that provide data insights.
  - Serverless means no compute instances are needed to run the jobs
  - the services are fully managed, you only pay for what you consume
  - the platform is fully integrated with GCP
- Cloud Dataproc is a managed hadoop service, it lets you create cluster in less than 90 seconds and can scale when jobs are running
  - Hadoop is an open source framework for big data, based on the mapreduce model.
  - Mapreduce uses the map funciton that runs in parrallel across a data set and the reduce fuction builds a final result
  - hadoop is usually a catch-all for hadoop itself and related projects like spark, pig, hive
  - Cloud Dataproc is a fast, easy and managed way to run the Hadoop stack
  - it will be built in 90s or less on top of compute engine vms that you control
  - it is easily scalable and you can use the default config for the hadoop software or customise it
- Cloud Dataproc is useful because you can easily migrate on-premises hadoop, quickly analyse data in cloud storage, use Spark and spark ML to run data analysis/ classification algorithms
  - running on premises hadoop jobs require hardware investment, on cloud dataproc you only pay for what you use.
  - you can save money by using preemptible compute engine instances for batch processing, you need to make sure the jobs can be restarted cleanly after termination though
  - once the data is in a cluster, spark and spark sql can do data mining, and use Mlib to discover patterns through machine learning
- Cloud dataflow offers managed data pipelines, processes data using Compute Engine instances, clusters are sixed for you with automated scaling, no instance provision is nrequired, you can write code once and get batch and streaming with a transform based programming model
  - Cloud Dataflow is better than dataproc in instances where you have a datset of unknown size, or when you don't need to manage the cluster size yourself
  - If the data shows up in realtime or if its of unpredictable size or rate then cloud dataflow is a good choice.
  - Cloud dataflow is both a unified programming model and a managed service, and its lets you develop and execute a big range of data processing patterns
    - extract transform and load
    - batch computation
    - continuous computation
  - You use Dataflow to build data pipelines, and the same pipelines work for both batch and streaming data.
  - Dataflow is a unified programming model and a managed service for developing and executing a wide range of data processing patterns including
    - ETL
    - batch computation
    - continuous computation
  - Cloud Dataflow frees you from operational tasks like resource management and performance optimization
- Cloud Dataflow features
  - Resource Management
    - Cloud Dataflow fully automates management of required processing resource. No more spinning up instances by hand
  - On Demand
    - All resources are provided on demand, enabling you to scale to meet your business needs. No need to buy reserved compute instances
  - Intelligent Work Scheduling
    - Automated and optimixed work partitioning which can dynamically rebalance lagging work. No more changin down hot keys or pre processing input data
  - Auto Scaling
    - Horizontal auto scaling of worker resources to meet optimum throughput requirements results in better overall price to performance
  - Unified Programming Model
    - The Dataflow API enables you to express MapReduce like operations, powerful data windowing and fine grained correctness control regardless of data source
  - Open Source
    - Developers wishing to extend the Dataflow programming model caan fork and or submit pull requests on the Java-based Cloud Dataflow SDK. Dataflow pipelines can also run on alternate runtimes like Spark and Flink
  - Monitoring
    - Intergrated into the GCP console Dataflow provides stats such as pipline throughput and lag as well as consolidated worker log inspection
  - Integreated
    - Intergrates with Cloud Storage, Cloud Pub and Sub, Cloud Datastore, Cloud Bigtable and BigQuery for seamless data processing. This can be extended to interact with others sources and sinks like Apache Kafka and HDFS
  - Reliable and Consistent Processing
    - Cloud Dataflow provides built in support for fault tolerant execution that is consistent and correct regardless of data size, cluster size and processing pattern or pipelline complexity.
 - Dataflow Pipeline
  - Each step of the pipeline is elastically scaledm there is no need to launch and manage a cluster.
  - Instead the service provides all resources on demand
  - It has automated and optimised work partitioning built in which can dynamically rebalance lagging work
  - That reduces the need to worry about hot keys 
  - that is situations where disproportionately large chunks of you input get mapped to the same cluster
 - Dataflow Uses, ETL pipelines, Data analysis, Orchestration, Integration
  - People use Dataflow for a variety of use cases, it serves well as a general purpose extract transform and load tool
  - Its use case as a data analysis engine comes in handy in events of
    - Fraud Detection in financial services
    - IOT analytics in manufacturing
    - healthcare
    - logistics
    - clickstream
    - point of scale
    - segmentation analysis in retail
  - Because those pipelines we saw can orchestrate multiple services, even external services
  - It can be used in realtime applications such as personalising gaming user experiences
- BigQuery is a fully managed data warehouse, provides near real time interactive analysis of massive datasets, Query using SQL syntax and no cluster maintenance required
  - If instead of a dynamic pipeline you to do ad hoc SQL queries on a massive datasetlm that is what BQ is for, BigQuery is Googles fully managed petabyte scale low cost analytics data warehouse
  - Big Query is NoOps, there is no infastructure to manage and you dont need a database admin, so you can focus on analysing data to find meaningful insights
  - You can take advantage of our pay as you go model and use familiar SQL.
  - BigQuery is a powerful big data analytics platform used all types of orgs
  - BigQuery features
    - Flexible Data ingestion
      - Load you data from cloud storage or cloud datastore, or stream it into BQ at 100K rows per second to enable real time analysis of your data
    - Global Availability
      - You have the option to store your BQ data in european locations while continuing to benefit from a fully managed service, now with the option of geographic data control, without low level cluster maintenance
    - Security and Permissions
      - You have full control over who has access to the data stored in BQ.
      - If you share datasets, doing so will not impact your cost or performance, those you share with pay for their own queries
    - Cost Controls
      - BQ provides cost control mechanisms that enable you to cap your daily costs at an amount that you choose
    - Highly Available
      - Transparent data replications in multiple geographies means that your data is available and durable even in the case of extreme failure modes
    - Super Fast Performance
      - Run super fast SQL queries against multiple terabytes of data in seconds, using the processing power of Google infastructure
    - Fully Integrated
      - in addition to SQL queries you can easily read and write data in BQ via Cloud Dataflow, Spark and Hadoop
    - Connect with Google Products
      - You can automatically export your data from Google Analytics Premium into BG and analyxe datasets stored in the google cloud storage, google drive and google sheets
  - BigQuery can make, Create, Replace, Update and Delete changes to Databases subject to some limitations
  - BigQuery runs on Googles high performance infastructure
    - Compute and Storage are separated with a terabit network in between
    - You only pay for storage and processing used
    - automatic discount for long term data storage
    - Its easy to get data into BigQuery, you can load from Cloud Storage or Cloud Datastore, or stream it into BigQuery at up to 100K rows per second
    - BigQuery is used by all types of organisations, smaller orgs like BQs free monthly quotas, bigger orgs like its seamless scale and its avaliable 99pc service level agreement
    - Long term storage pricing is an automatic discount for data residing in BQ for extended periods of time
    - When the age of your data reaches 90 days in BigQuery google will automatically drop the price of storage from $0.02 per GB per month down to $0.01 per GB per month
- Cloud Pub and Sub is scalable, reliable messaging
  - It Supports many to many asynchronous messaging, application components make push/pull subscriptions to topics
  - It Includes support for offline consumers 
  - based on proven Google technologies
  - Integrates with Cloud Dataflow for data processing pipelines
  - It allows you to send and receive messages between independent applications.
  - you can leverage the flexibility to decouple systems and components hosted on GCP or elsewhere
  - By building on the same tech Google uses, Cloud Pub/Sub is designed to provide 'at least once' delivery at low latency with on demand scalability to 1M messages per second
  - Cloud Pub/Sub features
    - Highly Scalable
      - Any customer can send up to 100k messages per second, by default and millions per second and beyond upon request
    - Push and Pull Delivery
      - Subscribers have flexible delivery options, whether they are accessible from the internet or behind a firewall
    - Encryption
      - Encryption of all message data on the wire and at rest provides data security and protection
    - Replicated Storage
      - Designed to provide 'at least once' message delivery by storing every message on multiple servers in multiple zones
    - End to End acknowledgement
      - Building reliable applications is easier with explicit application level acknowledgements
    - Fan-Out
      - Publish Messages to a topic once, and multiple subscribers reveive copies to support one-to-many or many-to-many communication patterns
    - REST API
      - Simple, stateless interface using JSON messages with API libraries in many programming languages
   - Why Use Cloud Pub/Sub
    - Building block for data ingestion in DataFlow, IoT, Marketing Analytics
    - Foundation for DataFlow streaming
    - Push Notification for cloud based applications
    - Connect applications across GCP
    - Cloud Pub/Sub builds on the same technology google uses interanlly
    - its an important building block for applications where data arrives at high and unpredictable rates, like IOT systems
    - if youre analysing streaming data, Cloud dataflow is a natural pairing with Pub/Sub.
- Cloud Datalab offers interactive data exploration
  - Interactive tool for large-scale data exploration, transformation, analysis and visualisation
  - Integrated and open source, built on Jupyter
  - For data science, an online lab notebook metaphor is a useful environment, because it feels natural to intersperse data analyses with comments about their results
  - A popular open-source system for hosting those is Project Jupyter, letting you create and maintain web based notebooks containing python code, you can run that interactive and view the results
  - Cloud Datalab lets you use Jupyter notebooks to explore, analyse and visualise data on GCP
  - It runs in a compute engine virtual Machine
  - To get started, you specify the virtual machine type you want and what region is should run in, when it launches it presents an interactive python environment thats ready to use
  - it orchestrates multiple GCP services automatically, so you can focus on exploring your data.
  - You only pay for the resources you use, theres no additional charge for Datalab itself
  - Cloud Datalab features
    - Integrated
      - Cloud Datalab handles authentication and cloud computation out of the box and is integrated with BigQuery, Compute Engine and Cloud Storage.
    - Multi-Language Support
      - Cloud Datalab currently supports Python, Sql and Javascript (For BigQuery user-defined functions)
    - Notebook Format
      - Cloud Datalab combines code, documentation, results and visualisations together in an intuitive notebook format
    - Pay per use Pricing
      - Only pay for the cloud resources you use, the app engine application, BigQuery and any additional resources you decide to use, such as cloud storage
    - Interactive Data Visualisation
      - Use Google charts or matplotlib for easy visualisations 
    - Collaborative
      - Git based source control of notebooks with the option to sync with non-google source doe repositories like githubn and bitbucket
    - Open Source
      - Developers who want to extend cloud datalab can for and/or submit pull requests on the github hosted project
    - Custom Deployment
      - Specify your minimum VM requirements, the network host and more
    - IPython Support
      - Cloud Datalab is based on Jupyter (Formerly Ipython) so you can use a large number of existing packages for stats, machine learning etc. Learn from published notebooks and swap tips with a vibrant ipython community
  - Why use cloud datalab
    - Create and manage code, documentation, results and visualisations in an intuitive notebook format
      - use google charts or matplotlib for easy visualtions
    - Analyse data in BigQuery, Compute Engine, and Cloud Storage using Python, SQL and Javascript
    - Easily deploy models to BigQuery
    - Cloud Datalab is integrated with BigQuery, Compute Engine, and Cloud Storage so accessing your data doesnt run into authentication hassles
    - You can visualise your data with google charts or matplotlib.
    - You can attach a GPU to a cloud datalab instance for faster processing, this is in beta
- Machine Learning APIs enable apps that see, hear and understand
  - Machine learning is one branch of the field of AI
  - Its a way of solving problems without expliciting coding the solution
  - instead human codes build systems that improve themselves over time, through repeated exposure to sample data
  - Major google application use machine learning 
- Cloud Machine Learning Platform
  - Open source tool to build and run neural network models
    - Wide platform support, CPU or GPU, mobile, server or cloud
  - Fully managed machine learning service
    - Familiar notebook-based developer experience
    - optimised for google infastructure, integrates with BigQuery and Cloud Storage
  - Pre-trained machine learning models built by Google
    - Speech, Vision, translate and Natural Language
  - Cloud Machine Learning Platform provides modern machine learning services, with pre-trained models and a platform to generate you own tailored maodels
  - As with other GCP products, theres a range of services that stretches from the highly general to the pre-customised
  - Tensorflow is an open source software library thats exceptionall well suited for machine learning application like neural networks
  - It was development by Google Brain for Googles internal use and then open sourced so the world can benefit
  - GCP is an ideal place for tensorflow because ML models need lots of on demand compute resources and lots of training data.
  - TensorFlow can also take advantage aof tensor processing units, which are hardware devices designed to accelerate machine learning workloads with tensorflow
  - GCP makes them available in the cloud with Compute Engine virtual machines
  - Each Cloud TPU provides up to 180 teraflops of performance and because you pay only for what you use.
  - Suppose you want a more managed service, Google cloud machine learning engine lets you easily build machine learning models that work on any type or size of data
  - Finally, if you just want to add ML capabilites to you application, without having to worry about the details of how they are provided
  - Google Cloud also offers a range of ML APIs suited to specific purposes
  - Why use the Cloud ML platform?
    - It falls into two catagories based on the data, unstructured or structured
    - Based on structure data, you can use ML for
      - for various kinds of classification or regression tasks like
      - customer churn analysts, product diagnostics and forecastiung
      - it can be the heart of a recommendation engine, for content personalistation and cross-sells and up-sells
      - You can use ML to detect anomalies, like fraud detection, sensor diagnostics or log metrics
    - Based on unstructured data, you can use ML for
      - image analystics, such as identifying damaged shipments, identifying styles and flaggin content.
      - you can do text analystics like call center log analysis, language identification, topic classification and sentiment analysis
    - In many of the most innovative applications for ML, several of these applications are combined.
- Cloud Vision API
  - Analyse images with a simple REST API
  - Gain insight from images
  - Detect inappropriate content
  - analyse sentiment
  - extract text
  - Cloud Vision enables developers to understant the content of an image by encapsulating powerful ML models in an easy to use REST API
  - It quickly classifies images into thousands of categories, detects objects in images and finds and reads printed words in images
  - You can build metadata on you image catalog, moderate offensive content or enable new marketing scenarios useing image sentiment analysis
  - analyse images uploaded in the request or integrate with your image storage on Cloud Storage
- Cloud Speech API
  - recognises over 80 languages and variants
  - can return text in real time
  - highly accurate, even in noisy environments
  - access from any device
  - allows developers to convert audio to text
- Cloud Natural Language API
  - Uses machine learning mdoels to reveal structure and meaning of text
  - extract information about items mentioned in text documents, news articles and blog posts
  - analyse text uploaded in request or integrate with cloud storage
  - The cloud natural language API offers a variety of natural language understanding technologies to developers
  - it can do syntax analysis, breaking down sentences supplies by you users into tokesns, identify nouns etc and figure out relations among words
  - It can do entity recognition, parsing text and flag mentions of people, locations etc
  - it can understand overall sentiment expressed in a block of text
  - it can do this in multiple languages
  - Cloud Natural Language API features
    - Syntax Analysis
      - Extract tokens and sentences, identify parts of speech and create dependency parse trees for each sentence
    - entity recognition
      - Identify entities and label by types
    - Sentiment Analysis
      - Understand the overall sentiment expressed in a block of text
    - Multi-Language
      - enables you to easily analyse text in multiple languages including english spanish and japanaese
    - Integrated REST API
      - Access via REST API. Text can be uploaded in the request or integrated with Cloud Storage
- Cloud Translation API
  - Translate arbitrary strings between thousands of language pairs
  - programmatically detect a documents language
  - support for dozens of languages
  - cloud translation API provides a simple programmatic interface for translating a string into any supported language
  - Translation API is highly responsive and dynamic
  - Language detection is also available in cases where the source language is unknown
  - Supports API Client libraries in Python, Java, Ruby, Objective C and more
- Cloud Video Intelligence API
  - Annotate the contents of videos
  - detect scene changes
  - flag inappropriate content
  - support for a variety of video formats
  - Allows developers to use google video analysis technology as part of their apps
  - The REST API enables users to annotate videos stored in Google Cloud Storage with video and frame level contextual info
  - helps you identify keyt entities 
  - You can use it to make video content searchable and discoverable

_ **Google Cloud Big Data Platform** _

- integrated serverless platform, you pay only for resources you consume
- GCP data services work together
- apache hadoop is a open source framework for big data based on the map reduce module
- also encompasses apache spark pig and hive
- dataproc is a fast easy managed way to run all hadoop 
- will be built ontop of compute engine VMs
- you can scale it up or down
- running on prem jobs require capital investment
- dataproc is pay per second
- one minute minimum billing 
- can save money by using preemtible batch processes, needs to be clean break around eighty percent cheaper
- once data is in a cluster you can use spark and ML libraries to do data mining

_ **Dataflow** _

- cloud dataproc is great when you have data of known size and you know when the data will arrive
- cloud dataflow is good when you don't know the data size and it comes in real time
- it is a managed service, it lets you develop and execute a big range of data processing patterns, extract transform and load batch computation
- there is no need to spin up a cluster or size instances, cloud data flow fully automates the management
- cloud data flow frees you from operational tasks like resource management and performance management of what resources are requrired
- each step of the pipeline is elastically scaled, there is no need to launch and manage a cluster, all resources are on demand
- that reduces the need to worry about hotkeys when dispropertionately large chunks of input get mapped to the same cluster

_ **BigQuery** _

- Suppose instead of a dynamic pipeline your data needs to run more in the way of exploring a vast ocean, you can use bigquery
- because theres no infastructure you can focus on analysing data
- you can stream it into bigquery at 100k rows per second
- once its there you can run super fast SQL queries against terabytes of data
-  You can easily write and read data in BigQuery via cloud dataflow hadoop and spar
- BigQuery is used by all types of orgs
- it is available 99.9 percent service level agreement
- it lets you specify the region where your data will be kept
- BigQuery separates storage and computation, you pay for data storage separately from queries
- you only pay for queries whilst they are running
- If you share data it won't effect your cost or performance, people you share with pay for their own queries
- When the age of your data reaches 90 days in BigQuery google automatically drops the price, automatic long storage data discount

_ **Pub/Sub and Datalab** _

- a messaging service when working with events in real time
- Reliable scalable foundation for stream analytics
- pub is short for publishers, sub is short for subscribers
- great for decoupling systems as recieving messages doesn't have to be synchronous
- at least once delivery, change some messages might be delivered more than once
- on demand scalability
- 1 mill messages per second and beyond
- you choose the quota you want
- builds on same tech google uses internally
- important building block for applications where data arrives at high and unpredictable rates
- If you're streaming data in cloud data flow it is a natural pairing with pub sub
- it also works well with applications built on GCPs comput platforms
- you can configure your subscribers to receive messages on a push pull basis
- meaning subscribers can get notified when new messages arrive for them or they can check for new messages at intervals
- it runs on a compute engine VM
- to get started you specify the VM and what region it should run in when it launches
- it presents an interactive python environment
- it orchestres multiple GCP services automatically so you can focus on exploring your data, only paying for resources you use
- no addition charge for datalab itself it is integrated with BigQuery compute engine

_ **Google Cloud Machine Learning Platform** _

- ML is a branch of AI its a way of solving problems without explicitly coding the solution
- you can add innovative capabilities to your own applications
- cloud machine learning platform provides modern ML services with pre-trained models and platform to generate your own tailored models
- Can use tensorflow m an open source software library thats well suited for ML applications
- GCP is an ideal place for tensorflow because machine learning models need lots of on demand compute resources and lots of training data
- can also take advantage of tensor processing units, hardware devices designed to accelerate ML workloads with tensorflow
- GCP makes them available with compute engine VMs
- lets you build ML models that work on any type of data of any size
- GCP also offers a wide range of ML APIs suited to speicifc uses
- Cloud ML platform for use on unstructured or structured data
- ML for image analytics
- ML for language identification and translation

_ **ML APIs** _

- Cloud vision api enables developers to understand the content of an image
  - quickly classifies images into categories
  - detects objects in images and printed words
  - powerful ML models in an easy to use API
- Cloud speech api enables developers to transform audio to text in many languages
- Cloud Natural language api offers natural language understanding technologies
  - syntax analysis
  - breaking into tokens
  - figure out relationships between words
- CLoud translation api provides a simple programmatic interface for translating an arbitrary string
- Cloud Video intelligence API lets you annotate videos in a variety of formats

_ **Getting Started with BigQuery** _

- load into bigquery
- loading data from cloud storage into BQ
- Bigquery in side 
- inside GCP project create new dataset
- add table to dataset
- give URL to CSV file
- destination table name
- tell BQ to automatically detect schema
- Query using BQ web interface
- paste in SQL query
- browse results
- can also run query using BQ command in cloud shell
