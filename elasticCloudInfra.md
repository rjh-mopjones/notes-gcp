
**Elastic Google Cloud Infrastructure, Scaling and Automation**

**Interconnecting Networks**

_ **Cloud VPN** _

 - Cloud VPN securely connects your on-premises network to your GCP VPC network through an IPsec VPN tunnel
 - Traffic traveling between the two networks is encrypted by one VPN gateway, then decrypted by the other VPN gateway
 - This protects your data as it travels over the public internet, and that’s why Cloud VPN is useful for low-volume data connections
 - As a managed service, Cloud VPN provides an SLA of 99.9% service availability and supports site-to-site VPN, static and dynamic routes, and IKEv1 and IKEv2 ciphers.
 - Cloud VPN doesn't support use cases where client computers need to “dial in” to a VPN using client VPN software
 - Also, dynamic routes are configured with Cloud Router, which we will cover briefly.
 - VPN Topology Example
   - Your VPC network has subnets in us-east1 and us-west1, 
   - with GCP resources in each of those regions.
   - These resources are able to communicate using their internal IP addresses 
   - because routing within a network is automatically configured (assuming that firewall rules allow the communication)
   - Now, in order to connect to your on-premises network and its resources, you need to configure your Cloud VPN gateway, on-premises VPN gateway, and two VPN tunnels. 
   - The Cloud VPN gateway is a regional resource that uses a regional external IP address
   - Your on-premises VPN gateway can be a physical device in your data center or a physical or software-based VPN offering in another cloud provider's network
   -  This VPN gateway also has an external IP address.
   - A VPN tunnel then connects your VPN gateways and serves as the virtual medium through which encrypted traffic is passed
   - In order to create a connection between two VPN gateways, you must establish two VPN tunnels
   - Each tunnel defines the connection from the perspective of its gateway, and traffic can only pass when the pair of tunnels is established.
   - Now, one thing to remember when using Cloud VPN is that the maximum transmission unit, or MTU, for your on-premises VPN gateway cannot be greater than 1460 bytes
   - This is because of the encryption and encapsulation of packets
 - Dynamic Routing with Cloud Router
   - Cloud VPN supports both static and dynamic routes. In order to use dynamic routes, you need to configure Cloud Routers
   - Cloud Router can manage routes for a Cloud VPN tunnel using Border Gateway Protocol, or BGP
   - This routing method allows for routes to be updated and exchanged without changing the tunnel configuration
     - EG, two different regional subnets in a VPC network, namely Test and Prod
     - The on-premises network has 29 subnets, and the two networks are connected through Cloud VPN tunnels
     - Now, how would you handle adding new subnets? 
     - For example, how would you add a new “Staging” subnet in the GCP network and a new on-premises 10.0.30.0/24 subnet to handle growing traffic in your data center?
   - To automatically propagate network configuration changes, the VPN tunnel uses Cloud Router to establish a BGP session between the VPC and the on-premises VPN gateway, 
     - which must support BGP
   - The new subnets are then seamlessly advertised between networks
   - This means that instances in the new subnets can start sending and receiving traffic immediately, as you will explore in the upcoming lab.
   - To set up BGP, an additional IP address has to be assigned to each end of the VPN tunnel
   - These two IP addresses must be link-local IP addresses, belonging to the IP address range 169.254.0.0/16.
   - These addresses are not part of IP address space of either network and are used exclusively for establishing a BGP session

_ **Cloud Interconnect and Peering** _

 - There are different Cloud Interconnect and Peering services available to connect your infrastructure to Google’s network
 - These services can be split into Dedicated versus Shared connections and Layer 2 versus Layer 3 connections
 - The services are Direct Peering, Carrier Peering, Dedicated Interconnect, and Partner Interconnect
 - Dedicated connections provide a direct connection to Google’s network, but shared connections provide a connection to Google’s network through a partner
 - Layer 2 connections use a VLAN that pipes directly into your GCP environment, providing connectivity to internal IP addresses in the RFC 1918 address space
 - Layer 3 connections provide access to G Suite services, YouTube, and Google Cloud APIs using public IP addresses
 - Google also offers its own Virtual Private Network service, called Cloud VPN
   - This service uses the public internet, but traffic is encrypted and provides access to internal IP addresses
   - That’s why Cloud VPN is a useful addition to Direct Peering and Carrier Peering.
 - Dedicated Interconnect provides direct physical connections between your on-premises network and Google’s network.
   - This enables you to transfer large amounts of data between networks, which can be more cost-effective than purchasing additional bandwidth over the public internet
 - In order to use Dedicated Interconnect, you need to provision a cross connect between the Google network and your own router in a common colocation facility, 
 - To exchange routes between the networks, you configure a BGP session over the interconnect between the Cloud Router and the on-premises router.
 - This will allow user traffic from the on-premises network to reach GCP resources on the VPC network, and vice versa.
 - Dedicated Interconnect can be configured to offer a 99.9% or a 99.99% uptime SLA. 
 - In order to use Dedicated Interconnect, your network must physically meet Google’s network in a supported colocation facility
 - Partner Interconnect provides connectivity between your on-premises network and your VPC network through a supported service provider
 - This is useful if your data center is in a physical location that cannot reach a Dedicated Interconnect colocation facility or 
   - if your data needs don't warrant a Dedicated Interconnect.
 - In order to use Partner Interconnect, you work with a supported service provider to connect your VPC and on-premises networks
 - These service providers have existing physical connections to Google's network that they make available for their customers to use
 - After you establish connectivity with a service provider, you can request a Partner Interconnect connection from your service provider
 - Then, you establish a BGP session between your Cloud Router and on-premises router to start passing traffic between your networks via the service provider's network
 - Partner Interconnect can be configured to offer a 99.9% or a 99.99% uptime SLA between Google and the service provider
 - Comparing Interconnect options, All of these options provide internal IP address access between resources in your on-premises network and in your VPC network
   - The IPsec VPN tunnels that Cloud VPN offers have a capacity of 1.5 to 3 Gbps per tunnel and require a VPN device on your on-premises network
     - The 1.5-Gbps capacity applies to traffic that traverses the public internet, and the 3-Gbps capacity applies to traffic that is traversing a direct peering link
     - You can configure multiple tunnels if you want to scale this capacity
   - Dedicated Interconnect has a capacity of 10 Gbps per link and requires you to have a connection in a Google-supported colocation facility.
     - You can have up to 8 links to achieve multiples of 10 Gbps, but 10 Gbps is the minimum capacity. 
     - As of this recording, there is a beta feature that provides 100 Gbps per link with a maximum of 2 links
   - Partner Interconnect has a capacity of 50 Mbps to 10 Gbps per connection, and requirements depend on the service provider
   - My recommendation is to start with VPN tunnels. 
     - When you need enterprise-grade connections to GCP, switch to Dedicated Interconnect or Partner Interconnect,
     - depending on your proximity to a colocation facility and your capacity requirements.
 - Cloud Peering services, which are Direct Peering and Carrier Peering
   - These services are useful when you require access to Google and Google Cloud properties
   - Google allows you to establish a Direct Peering connection between your business network and Google’s
   - With this connection you will be able to exchange internet traffic between your network and Google’s at one of Google’s broad-reaching edge network locations
   - Direct Peering with Google is done by exchanging BGP routes between Google and the peering entity
   - After a Direct Peering connection is in place, you can use it to reach all of Google’s services, including the full suite of Google Cloud Platform products
   - Unlike Dedicated Interconnect, Direct Peering does not have an SLA
   - GCP’s Edge Points of Presence, or PoPs, are where Google's network connects to the rest of the internet via peering
 - If you require access to Google public infrastructure and cannot satisfy Google’s peering requirements, you can connect via a Carrier Peering partner
   - Work directly with your service provider to get the connection you need and to understand the partner’s requirements
   - like Direct Peering, Carrier Peering does not have an SLA.
 - Compairng Peering Options, All of these options provide public IP address access to all of Google’s services
   - Direct Peering has a capacity of 10 Gbps per link and requires you to have a connection in a GCP Edge Point of Presence
   - Carrier Peering’s capacity and requirements vary depending on the service provider that you work with.
 - the 5 connection services
   - Another way to organize these services is by Interconnect services and by Peering services.
   - Interconnect services provide direct access to RFC1918 IP addresses in your VPC, with an SLA
   - Peering services, in contrast, offer access to Google public IP addresses only, without an SLA
   - Ask yourself whether you need to extend your network for G Suite services, YouTube, or Google Cloud APIs
     - If you do, choose one of the Peering services
     - If you can meet Google’s Direct Peering requirements, choose Direct Peering; otherwise, choose Carrier Peering.
   - If you don’t need to extend your network for G Suite services or Google Cloud APIs but want to extend the reach of your network to GCP
     - you want to pick one of the Interconnect services
   -  If you cannot meet Google at one of its colocation facilities
     - choose Cloud VPN or Partner Interconnect
     - This choice will depend on your bandwidth and encryption requirements, along with the purpose of the connection
     - Specifically, if you have modest bandwidth needs, will use the connection for short durations and trials, and require an encrypted channel, choose Cloud VPN
     - otherwise, choose Partner Interconnect
   - If you can meet Google at one of its colocation facilities
     - you might jump to Dedicated Interconnect
   - however, if you cannot provide your own encryption mechanisms for sensitive traffic, feel that a 10-Gbps connection is too big, or want access to multiple clouds
     - you’ll want to consider Cloud VPN or Partner Interconnect instead

_ **Sharing VPC Networks** _
 
 - In the simplest cloud environment, a single project might have one VPC network, spanning many regions, with VM instances hosting very large and complicated applications.
 - However, many organizations commonly deploy multiple, isolated projects with multiple VPC networks and subnets.
 - Shared VPC allows an organization to connect resources from multiple projects to a common VPC network
   - This allows the resources to communicate with each other securely and efficiently using internal IPs from that network
   - EG, there is one network that belongs to the Web Application Server’s project
   - This network is shared with three other projects, namely the Recommendation Service, the Personalization Service, and the Analytics Service
   - Each of those service projects has instances that are in the same network as the Web Application Server and allow for private communication to that server, 
   - using internal IP addresses.
   - The Web Application Server communicates with clients and on-premises using the server’s external IP address
   - The backend services, in contrast, cannot be reached externally because they only communicate using internal IP addresses.
   - When you use shared VPC, you designate a project as a host project and attach one or more other service projects to it.
   - In this case, the Web Application Server’s project is the host project, and the three other projects are the service projects
   - The overall VPC network is called the shared VPC network
 - VPC Network Peering, in contrast, allows private RFC 1918 connectivity across two VPC networks, regardless of whether they belong to the same project or the same organization
   - Now, remember that each VPC network will have firewall rules that define what traffic is allowed or denied between the networks.
   - EG, there are two organizations that represent a consumer and a producer, respectively
   - Each organization has its own organization node, VPC network, VM instances, Network Admin, and Instance Admin
   -  In order for VPC Network Peering to be established successfully, 
   - the Producer Network Admin needs to peer the Producer Network with the Consumer Network, 
   - and the Consumer Network Admin needs to peer the Consumer Network with the Producer Network
   - When both peering connections are created, the VPC Network Peering session becomes Active and routes are exchanged
   - This allows the virtual machine instances to communicate privately using their internal IP addresses. 
   - VPC Network Peering is a decentralized or distributed approach to multi-project networking, 
   - because each VPC network may remain under the control of separate administrator groups and maintains its own global firewall and routing tables
   - Historically, such projects would consider external IP addresses or VPNs to facilitate private communication between VPC networks
   - However, VPC Network Peering does not incur the network latency, security, and cost drawbacks that are present when using external IP addresses or VPNs.
 - Shared VPC vs VPC Peering
   - If you want to configure private communication between VPC networks in different organizations, you have to use VPC Network Peering
   - Shared VPC only works within the same organization
   - if you want to configure private communication between VPC networks in the same project, you have to use VPC Network Peering
   - This doesn’t mean that the networks need to be in the same project, but they can be
   - Shared VPC only works across projects.
   - the biggest difference between the two configurations is the network administration models
   - Shared VPC is a centralized approach to multi-project networking, because security and network policy occurs in a single designated VPC network
   - In contrast, VPC Network Peering is a decentralized approach, 
     - because each VPC network can remain under the control of separate administrator groups and maintains its own global firewall and routing tables.

**Load Balancing Autoscaling**

 - Cloud Load Balancing gives you the ability to distribute load-balanced compute resources in single or multiple regions to meet your high availability requirements, 
   - to put your resources behind a single anycast IP address, and to scale your resources up or down with intelligent autoscaling. 
 - Using Cloud Load Balancing, you can serve content as close as possible to your users on a system that can respond to over 1 million queries per second
 - Cloud Load Balancing is a fully distributed, software-defined, managed service
 - It is not instance or device-based, so you do not need to manage a physical load balancing infrastructure.
 - GCP offers different types of load balancers that can be divided into two categories: global and regional.
   - The global load balancers are the HTTP(S), SSL proxy, and TCP proxy load balancers
     - These load balancers leverage the Google frontends, which are software-defined, distributed systems that sit in Google’s points of presence and are distributed globally.
     - Therefore, you want to use a global load balancer when your users and instances are globally distributed, 
       - your users need access to the same applications and content, and you want to provide access using a single anycast IP address
   - The regional load balancers are the internal and network load balancers, and they distribute traffic to instances that are in a single GCP region
     - The internal load balancer uses Andromeda, which is GCP’s software-defined network virtualization stack, 
       - and the network load balancer uses Maglev, which is a large, distributed software system.
   - There’s also another internal load balancer for HTTP(S) traffic, but it’s in beta as of this recording.
     - This 6th load balancer is a proxy-based, regional Layer 7 load balancer 
       - that enables you to run and scale your services behind a private load balancing IP address that is accessible only in the load balancer's region in your VPC networ

_ **Managed Instance Groups** _
  
 - A managed instance group is a collection of identical VM instances that you control as a single entity, using an instance template
 - You can easily update all the instances in the group by specifying a new template in a rolling update
   - Also, when your applications require additional compute resources, managed instance groups can automatically scale the number of instances in the group. 
 - Managed instance groups can work with load balancing services to distribute network traffic to all of the instances in the group. 
 -  If an instance in the group stops, crashes, or is deleted by an action other than the instance group’s commands, 
   - the managed instance group automatically recreates the instance so it can resume its processing tasks
 - The recreated instance uses the same name and the same instance template as the previous instance
 - Managed instance groups can automatically identify and recreate unhealthy instances in a group to ensure that all the instances are running optimally.
 - Regional managed instance groups are generally recommended over zonal managed instance groups 
   - because they allow you to spread the application load across multiple zones instead of confining your application to a single zone 
   - or you having to manage multiple instance groups across different zones
 - This replication protects against zonal failures and unforeseen scenarios where an entire group of instances in a single zone malfunctions
   - If that happens, your application can continue serving traffic from instances running in another zone of the same region.
 - In order to create a managed instance group, you first need to create an instance template
   - Next, you're going to create a managed instance group of n specified instances
   - The instance group manager then automatically populates the instance group based on the instance template. 
 - You can easily create instance templates using the GCP Console.
 - The instance template dialog looks and works exactly like creating an instance, except that the choices are recorded so that they can be repeated. 
 - When you create an instance group, you define the specific rules for the instance group.
   - First, decide whether the instance group is going to be single or multi-zoned, and where those locations will be.
   - Second, choose the ports that you are going to allow and load balance across.
   - Third, select the instance template that you want to use.
   - Fourth, decide whether you want to autoscale, and under what circumstances.
   - Finally, consider creating a health check to determine which instances are healthy and should receive traffic.
 - Essentially, you're still creating virtual machines, but you're applying more rules to that instance group.
 - managed instance groups offer autoscaling capabilities that allow you to automatically add or remove instances from a managed instance group based on increases or decreases in load
 - Autoscaling helps your applications gracefully handle increases in traffic and reduces cost when the need for resources is lower
 - You just define the autoscaling policy, and the autoscaler performs automatic scaling based on the measured load
 - Applicable autoscaling policies include scaling based on CPU utilization, load balancing capacity, or monitoring metrics, or by a queue-based workload like Cloud Pub/Sub.
   - EG, et’s assume you have 2 instances that are at 100% and 85% CPU utilization
     - If your target CPU utilization is 75%, the autoscaler will add another instance to spread out the CPU load and stay below the 75% target CPU utilization
     - Similarly, if the overall load is much lower than the target, the autoscaler will remove instances as long as that keeps the overall utilization below the target
     - Now, you might ask yourself how do I monitor the utilization of my instance group.
 - When you click on an instance group (or even an individual VM), a graph is presented
   - By default you’ll see the CPU utilization over the past hour, but you can change the time frame and visualize other metrics like disk and network usage
   - These graphs are very useful for monitoring your instances’ utilization and for determining how best to configure your Autoscaling policy to meet changing demand
   - If you monitor the utilization of your VM instances in Stackdriver Monitoring, you can even set up alerts through several notification channels.
 - Another important configuration for a managed instance group and load balancer is a health check.
   - A health check is very similar to an uptime check in Stackdriver. You just define a protocol, port, and health criteria, as shown in this screenshot
   - Based on this configuration, GCP computes a health state for each instance.
   - The health criteria define how often to check whether an instance is healthy (that’s the check interval)
   - how long to wait for a response (that’s the timeout)
   - how many successful attempts are decisive (that’s the healthy threshold)
   - and how many failed attempts are decisive (that’s the unhealthy threshold)
   - In the example on this slide, the health check would have to fail twice over a total of 15 seconds before an instance is considered unhealthy

_ **HTTP(S) Load Balancing** _
  
 - HTTP(S) load balancing, which acts at Layer 7 of the OSI model.  This is the application layer,
   - which deals with the actual content of each message, allowing for routing decisions based on the UR
 - GCP’s HTTP(S) load balancing provides global load balancing for HTTP(S) requests destined for your instances.
 - This means that your applications are available to your customers at a single anycast IP address, which simplifies your DNS setup
 - HTTP(S) load balancing balances HTTP and HTTPS traffic across multiple backend instances and across multiple regions. 
 - HTTP requests are load balanced on port 80 or 8080, and HTTPS requests are load balanced on port 443. 
 - This load balancer supports both IPv4 and IPv6 clients, is scalable, requires no pre-warming, and enables content-based and cross-region load balancing. 
 - You can configure URL maps that route some URLs to one set of instances and route other URLs to other instances.
 - Requests are generally routed to the instance group that is closest to the user.
 - If the closest instance group does not have sufficient capacity, the request is sent to the next closest instance group that does have capacity.
 - You will get to explore most of these benefits in the first lab of the module
 - Architecture of an HTTP(S) load balancer 
   - A global forwarding rule directs incoming requests from the internet to a target HTTP proxy.
   - The target HTTP proxy checks each request against a URL map to determine the appropriate backend service for the request
     - EG, you can send requests for www.example.com/audio to one backend service, which contains instances configured to deliver audio files, 
     - and requests for www.example.com/video to another backend service, which contains instances configured to deliver video files
   - The backend service directs each request to an appropriate backend based on serving capacity, zone, and instance health of its attached backends.
 - The backend services contain a health check, session affinity, a timeout setting, and one or more backends.
 - A health check polls instances attached to the backend service at configured intervals
 - Instances that pass the health check are allowed to receive new requests.  Unhealthy instances are not sent requests until they are healthy again
 - Normally, HTTP(S) load balancing uses a round-robin algorithm to distribute requests among available instances. 
 - This can be overridden with session affinity
   - Session affinity attempts to send all requests from the same client to the same virtual machine instance.
 - Backend services also have a timeout setting, which is set to 30 seconds by default
 - This is the amount of time the backend service will wait on the backend before considering the request a failure
 - This is a fixed timeout, not an idle timeout
 - If you require longer-lived connections, set this value appropriately
 - The backends themselves contain an instance group, a balancing mode and a capacity scaler
   - An instance group contains virtual machine instances
     - The instance group may be a managed instance group with or without autoscaling or an unmanaged instance group.
   - A balancing mode tells the load balancing system how to determine when the backend is at full usage.
     - If all the backends for the backend service in a region are at full usage, new requests are automatically routed to the nearest region that can still handle requests
     - The balancing mode can be based on CPU utilization or requests per second (RPS).
   - A capacity setting is an additional control that interacts with the balancing mode setting.
     - EG,  if you normally want your instances to operate at a maximum of 80% CPU utilization, you would set your balancing mode to 80% CPU utilization and your capacity to 100%
     - If you want to cut instance utilization in half, you could leave the balancing mode at 80% CPU utilization and set capacity to 50%
 - Now, any changes to your backend services are not instantaneous.
   - So, don’t be surprised if it takes several minutes for your changes to propagate throughout the network.
 - HTTP load balancer in action
   - EG, a single global IP address, but users enter the Google Cloud network from two different locations: one in North America and one in EMEA.
     - First, the global forwarding rule directs incoming requests to the target HTTP proxy
     - The proxy checks the URL map to determine the appropriate backend service for the request.
     - In this case, we are serving a guestbook application with only one backend service.
     - The backend service has two backends: one in us-central1-a and one in europe-west1-d.
     - Each of those backends consists of a managed instance group.
     - Now, when a user request comes in, the load balancing service determines the approximate origin of the request from the source IP address.
     - The load balancing service also knows the locations of the instances owned by the backend service, their overall capacity, and their overall current usage
     - Therefore, if the instances closest to the user have available capacity, the request is forwarded to that closest set of instances
     - In our example, traffic from the user in North America would be forwarded to the managed instance group in us-central1-a, 
     - and traffic from the user in EMEA would be forwarded to the managed instance group in europe-west1-d
     - If there are several users in each region, the incoming requests to the given region are distributed evenly across all available backend services and instances in that region.
     - If there are no healthy instances with available capacity in a given region, the load balancer instead sends the request to the next closest region with available capacity. 
     - Therefore, traffic from the EMEA user could be forwarded to the us-central1-a backend 
     - if the europe-west1-d backend does not have capacity or has no healthy instances as determined by the health checker
     - This is referred to as cross-region load balancing.
   - Another example of an HTTP load balancer is a content-based load balancer
     - In this case, there are two separate backend services that handle either web or video traffic. 
     - The traffic is split by the load balancer based on the URL header as specified in the URL map.
     - If a user is navigating to /video, the traffic is sent to the backend video-service, 
     - and if a user is navigating anywhere else, the traffic is sent to the web-service backend. All of that is achieved with a single global IP address.
 - An HTTP(S) load balancer has the same basic structure as an HTTP load balancer, but differs in the following ways:
   - An HTTP(S) load balancer uses a target HTTPS proxy instead of a target HTTP proxy.
   - An HTTP(S) load balancer requires at least one signed SSL certificate installed on the target HTTPS proxy for the load balancer.
   - The client SSL session terminates at the load balancer.
   - HTTP(S) load balancers support the QUIC transport layer protocol.
 - QUIC is a transport layer protocol that allows faster client connection initiation, eliminates head-of-line blocking in multiplexed streams, 
   - and supports connection migration when a client's IP address changes
 - To use HTTPS, you must create at least one SSL certificate that can be used by the target proxy for the load balancer. 
   - You can configure the target proxy with up to ten SSL certificates. 
   - For each SSL certificate, you first create an SSL certificate resource, which contains the SSL certificate information.
   - SSL certificate resources are used only with load balancing proxies such as a target HTTPS proxy or target SSL proxy, which we will discuss later in this module.

_ **SSL Proxy/TCP Proxy Load Balancing** _

 - SSL proxy is a global load balancing service for encrypted, non-HTTP traffic
 - This load balancer terminates user SSL connections at the load balancing layer, then balances the connections across your instances using the SSL or TCP protocols
 - These instances can be in multiple regions, and the load balancer automatically directs traffic to the closest region that has capacity.
 - SSL proxy load balancing supports both IPv4 and IPv6 addresses for client traffic and provides Intelligent routing, Certificate management, Security patching and SSL policies.
   - Intelligent routing means that this load balances can route requests to backend locations where there is capacity.
   - From a certificate management perspective, you only need to update your customer-facing certificate in one place when you need to switch certificates.
     - Also, you can reduce the management overhead for your virtual machine instances by using self-signed certificates on your instances.
   - In addition, if vulnerabilities arise in the SSL or TCP stack, GCP will apply patches at the load balancer automatically in order to keep your instances safe.
 - EG, traffic from users in Iowa and Boston is terminated at the global load balancing layer
   - From there, a separate connection is established to the closest backend instance. 
   - In other words, the user in Boston would reach the us east region, and the user in Iowa would reach the us central region, if there is enough capacity
   - Now, the traffic between the proxy and the backends can use SSL or TCP. I recommend using SSL.
 - TCP proxy is a global load balancing service for unencrypted, non-HTTP traffic
   - This load balancer terminates your customers’ TCP sessions at the load balancing layer, then forwards the traffic to your virtual machine instances using TCP or SSL
   - These instances can be in multiple regions, and the load balancer automatically directs traffic to the closest region that has capacity.
   - TCP proxy load balancing supports both IPv4 and IPv6 addresses for client traffic
   - Similar to the SSL proxy load balancer, the TCP proxy load balancer provides Intelligent routing and Security patching
 - EG, traffic from users in Iowa and Boston is terminated at the global load balancing layer
   - From there, a separate connection is established to the closest backend instance
   - As in the SSL proxy load balancing example, 
   - the user in Boston would reach the us east region, and the user in Iowa would reach the us central region, 
   - if there is enough capacity.
   - Now, the traffic between the proxy and the backends can use SSL or TCP, and I also recommend using SSL here.
 
_ **Network Load Balancing** _
 
 - Network load balancing is a regional, non-proxied load balancing service
 - In other words, all traffic is passed through the load balancer, instead of being proxied, 
   - and traffic can only be balanced between VM instances that are in the same region, unlike a global load balancer
 - This load balancing service uses forwarding rules to balance the load on your systems based on incoming IP protocol data, such as address, port, and protocol type
 - You can use it to load balance UDP traffic and to load balance TCP and SSL traffic on ports that are not supported by the TCP proxy and SSL proxy load balancers
 - The backends of a network load balancer can be a template-based instance group or target pool resource
 - A target pool resource defines a group of instances that receive incoming traffic from forwarding rules.
 - When a forwarding rule directs traffic to a target pool, 
   - the load balancer picks an instance from these target pools based on a hash of the source IP and port and the destination IP and port
 - These target pools can only be used with forwarding rules that handle TCP and UDP traffic
 - Now, each project can have up to 50 target pools, and each target pool can have only one health check.
 - Also, all the instances of a target pool must be in the same region, which is the same limitation as for the network load balancer

_ **Internal Load Balancing** _
 
 - Internal load balancing is a regional, private load balancing service for TCP- and UDP-based traffic
 - In other words, this load balancer enables you to run and scale your services behind a private load balancing IP address 
 - This means that it is only accessible through the internal IP addresses of virtual machine instances that are in the same region
 - Therefore, use internal load balancing to configure an internal load balancing IP address to act as the frontend to your private backend instances
 - Because you don’t need a public IP address for your load-balanced service, your internal client requests stay internal to your VPC network and region.
 - This often results in lowered latency, because all your load-balanced traffic will stay within Google’s network, making your configuration much simpler.
 - GCP internal load balancing is not based on a device or a VM instance. Instead, it is a software-defined, fully distributed load balancing solution
 - In the traditional proxy model of internal load balancing
   - you configure an internal IP address on a load balancing device or instances, and your client instance connects to this IP address
   - Traffic coming to the IP address is terminated at the load balancer, and the load balancer selects a backend to establish a new connection to
   - Essentially, there are two connections: one between the Client and the Load Balancer, and one between the Load Balancer and the Backend
 - GCP internal load balancing distributes client instance requests to the backends using a different approach
   -  It uses lightweight load balancing built on top of Andromeda (Google’s network virtualization stack) 
   - to provide software-defined load balancing that directly delivers the traffic from the client instance to a backend instance
 - Now, internal load balancing enables you to support use cases such as the traditional 3-tier web services.
   - EG, the web tier uses an external HTTP(S) load balancer that provides a single global IP address for users in San Francisco, Iowa, Singapore, and so on
   - The backends of this load balancer are located in the us-central1 and asia-east1 regions because this is a global load balancer.
   - These backends then access an internal load balancer in each region as the application or internal tier
   - The backends of this internal tier are located in us-central1-a, us-central1-b, and asia-east1-b
   - The last tier is the database tier in each of those zones
   - The benefit of this 3-tier approach is that neither the database tier nor the application tier is exposed externally
   - This simplifies security and network pricing.

_ **Choosing a Load Balancer** _

 - One differentiator between the different GCP load balancers is the support for IPv6 clients
 - Only the HTTP(S), SSL proxy, and TCP proxy load balancing services support IPv6 clients
 - IPv6 termination for these load balancers enables you to handle IPv6 requests from your users and proxy them over IPv4 to your backends.
   - For example, in this diagram there is a website www.example.com that is translated by Cloud DNS to both an IPv4 and IPv6 address
   - This allows a desktop user in New York and a mobile user in Iowa to access the load balancer through the IPv4 and IPv6 addresses, respectively
 - But how does the traffic get to the backends and their IPv4 addresses?
   - Well, the load balancer acts as a reverse proxy, terminates the IPv6 client connection, and places the request into an IPv4 connection to a backend
   - On the reverse path, the load balancer receives the IPv4 response from the backend and places it into the IPv6 connection back to the original client
   - In other words, configuring IPv6 termination for your load balancers lets your backend instances appear as IPv6 applications to your IPv6 clients.
 - Now, in order to decide which load balancer best suits your implementation of GCP, consider the following aspects of Cloud Load Balancing:
   - global versus regional load balancing, external versus internal load balancing, and the traffic type
 - if you need to choose an external load balancing service
   - First, choose the type of traffic that your load balancer must handle.
   - If that is HTTP or HTTPS traffic, I recommend using the HTTP(S) load balancing service as a Layer 7 load balancer
   - Otherwise, use the TCP and UDP traffic paths of this flow chart to determine whether the SSL proxy, TCP proxy, or network load balancing service meets your needs.
 - If you need an internal load balancing service
   - you have the internal load balancing service available, and it supports both TCP and UDP traffic
   - As I mentioned at the beginning of this module, there’s actually another internal load balancer for HTTP(S) traffic but it’s in beta as of this recording
   - This 6th load balancer is for HTTP or HTTPS traffic and it’s regional, meaning for IPv4 clients

**Infrastructure Automation**

 - we have covered several of GCP’s services and features, it makes sense to talk about how to automate the deployment of GCP infrastructure.
 - Calling the cloud API from code is a powerful way to generate infrastructure
 - But writing code to create infrastructure also has some challenges
 - One issue is that the maintainability of the infrastructure depends directly on the quality of the software
   - EG, a program could have a dozen locations that call the cloud API to create VMs
   - Fixing a problem with the definition of one VM would require first identifying which of the dozen calls actually created it.
   - Standard software development best practices will apply, and it’s important to note that things could change rapidly, requiring maintenance on your code
 - Clearly another level of organization is needed
 - That's the purpose of Deployment Manager
 - Deployment Manager uses a system of highly structured templates and configuration files to document the infrastructure in an easily readable and understandable format
 - Deployment Manager conceals the actual Cloud API calls, so you don't need to write code and can focus on the definition of the infrastructure

_ **Deployment Manager** _

 - Cloud Shell works best when you are comfortable using a specific service and you want to quickly create resources using the command line. 
   - Deployment Manager takes this one step further
 - Deployment Manager is an infrastructure deployment service that automates the creation and management of GCP resources for you
 - You just specify all the resources needed for your application in a declarative format and deploy your configuration
 - This deployment can be repeated over and over with consistent results, and you can delete a whole deployment with one command or click
 - The benefit of a declarative approach is that it allows you to specify what the configuration should be and let the system figure out the steps to take.
 - nstead of deploying each resource separately, you specify the set of resources which compose the application or service, allowing you to focus on the application. 
 - Unlike Cloud Shell, Deployment Manager will deploy resources in parallel
 - You can even abstract parts of your configuration into individual building blocks or templates that can be used for other configurations
 - Deployment Manager uses the underlying APIs of each GCP service to deploy your resources
 - This enables you to deploy almost everything we have seen so far, 
   - from instances, instance templates, and groups, to VPC networks, firewall rules, VPN tunnels, Cloud Routers, and load balancers
 - EG that shows how Deployment Manager can be used to set up an auto mode network with an HTTP firewall rule.
   - could put this whole deployment into one single configuration; however, it’s useful to parameterize your configuration with templates
   - Specifically, we are going to create one template for the auto mode network and one for the firewall rule
   - Therefore, if we want to create either of these resources somewhere else later on, we can use those templates.
 - EG, the auto mode network template, which we can write in Jinja2 or Python. Now, each resource must contain a name, type, and properties:
   - For the name, I am using an environment variable to get the name from the top-level configuration, which makes this template more flexible
   - For the type, I am defining the API for a VPC network, which is compute.v1.network. 
     - You can find all supported types in the documentation or query them within Cloud Shell, as you will explore in the upcoming lab.
   - By definition, an auto mode network automatically creates a subnetwork in each region. 
     - Therefore, I am setting the autoCreateSubnetworks property to true.
   - The properties section contains the network I want to apply this firewall rule to, the source IP ranges, and the protocols and ports that are allowed. 
     - Except for the source IP ranges, I am defining these properties as template properties. 
     - I will provide the exact properties from the top-level configuration, 
     - which makes this firewall rule extremely flexible. 
     - Essentially, I can use this firewall rule template for any network and any protocol and port combination
   - Next, let’s write the top-level configuration in YAML syntax.
     - I start by importing the templates that I want to use in this configuration, which are autonetwork.jinja and firewall.jinja.
   - Then, I define the auto mode network by giving it the name “mynetwork” and leveraging the autonetwork.jinja template.
   - I could create more auto mode networks in this configuration with other names, or simply reuse this template in other configurations, later on.
   - Now, I define the firewall rule, by giving it a name, leveraging the firewall.jinja template, referencing mynetwork, and defining the IP protocol and port
   - I can easily add other ports, such as 443 for HTTPS or 22 for SSH traffic
   - Using the selfLink reference for the network name ensures that the VPC network is created before the firewall rule
   - This is very important because Deployment Manager creates all the resources in parallel, unless you use references
   - You would get an error without the reference because you cannot create a firewall rule for a non-existing network.
 - Infrastructure as code tools for GCP
   - Now, there are other infrastructure automation tools in addition to Deployment Manager that you can use in GCP
   - You can also use Terraform, Chef, Puppet, Ansible, or Packer
   - All of these tools allow you to treat your infrastructure like software, which helps you decrease costs, reduce risks, and deploy faster by capturing infrastructure as code.
   - You might recognize some of these tools, because they work across many cloud service providers.

_ **GCP Marketplace** _
 
 - GCP Marketplace lets you quickly deploy functional software packages that run on GCP
 - Essentially, GCP Marketplace offers production-grade solutions from third-party vendors who have already created their own deployment configurations based on Deployment Manager.
 - These solutions are billed together with all of your project’s GCP services
 - If you already have a license for a third-party service, you might be able to use a Bring Your Own License solution
 - You can deploy a software package now and scale that deployment later when your applications require additional capacity
 - GCP even updates the images of these software packages to fix critical issues and vulnerabilities, but doesn't update software that you have already deployed
 - You even get direct access to partner support.

**Managed Services**

 - As an alternative to infrastructure automation, you can eliminate the need to create infrastructure by leveraging a managed service
 - Managed services are partial or complete solutions offered as a service
 - They exist on a continuum between platform as a service and software as a service, depending on how much of the internal methods and controls are exposed
 - Using a managed service allows you to outsource a lot of the administrative and maintenance overhead to Google, if your application requirements fit within the service offering

_ **BigQuery** _

 - BigQuery is GCP’s serverless, highly scalable, and cost-effective cloud data warehouse
 - It is a petabyte-scale data warehouse that allows for super-fast queries using the processing power of Google's infrastructure
 - Because there is no infrastructure for you to manage, you can focus on uncovering meaningful insights using familiar SQL without the need for a database administrator
 - You can access BigQuery by using the GCP Console, by using a command-line tool, 
   - or by making calls to the BigQuery REST API using a variety of client libraries such as Java, .NET, or Python
 - There are also several third-party tools that you can use to interact with BigQuery, such as visualizing the data or loading the data.
 - Here is an example of a query on a table with over 100 billion rows
 - This query processes over 4.1 TB but takes less than a minute to execute
 - The same query would take hours, if not days, through a serial execution.

_ **Cloud Dataflow** _

 - Cloud Dataflow is a managed service for executing a wide variety of data processing patterns
 - It’s essentially a fully managed service for transforming and enriching data in stream and batch modes with equal reliability and expressiveness
 - With Cloud Dataflow, a lot of the complexity of infrastructure setup and maintenance is handled for you. 
 - It’s built on Google Cloud infrastructure and autoscales to meet the demands of your data pipelines, allowing it to intelligently scale to millions of queries per second
 - Cloud Dataflow supports fast, simplified pipeline development via expressive SQL, Java, and Python APIs in the Apache Beam SDK, 
 - which provides a rich set of windowing and session analysis primitives as well as an ecosystem of source and sink connectors
 - Cloud Dataflow is also tightly coupled with other GCP services like Stackdriver, 
   - so you can set up priority alerts and notifications to monitor your pipeline and the quality of data coming in and out
 - As I just mentioned, Cloud Dataflow processes stream and batch data
   - This data could come from other GCP services like Cloud Datastore or Cloud Pub/Sub, which is Google’s messaging and publishing service
   - The data could also be ingested from third-party services like Apache Avro and Apache Kafka
 - After you transform the data with Cloud Dataflow, you can analyze it in BigQuery, AI Platform, or even Cloud Bigtable
   - Using Data Studio, you can even build real-time dashboards for IoT devices

_ **Cloud Dataflow** _

 - Cloud Dataprep is an intelligent data service for visually exploring, cleaning, 
   - and preparing structured and unstructured data for analysis, reporting, and machine learning.
 - Because Cloud Dataprep is serverless and works at any scale, there is no infrastructure to deploy or manage
   - Your next ideal data transformation is suggested and predicted with each UI input, so you don’t have to write code
 - With automatic schema, datatype, possible joins, and anomaly detection, you can skip time-consuming data profiling and focus on data analysis
 - Cloud Dataprep is an integrated partner service operated by Trifacta and based on their industry-leading data preparation solution, Trifacta Wrangler.
 - Google works closely with Trifacta to provide a seamless user experience that removes the need for 
   - up-front software installation, separate licensing costs, or ongoing operational overhead
 - Cloud Dataprep is fully managed and scales on demand to meet your growing data preparation needs, so you can stay focused on analysis.
 - As you can see, Cloud Dataprep can be leveraged to prepare raw data from BigQuery, Cloud Storage, 
   - or a file upload before ingesting it onto a transformation pipeline like Cloud Dataflow
 - The refined data can then be exported to BigQuery or Cloud Storage for analysis and machine learning.

_ **Cloud Dataproc** _

 - Cloud Dataproc is a fast, easy-to-use, fully managed cloud service for running Apache Spark and Apache Hadoop clusters in a simpler way
 - You only pay for the resources you use with per-second billing
 - If you leverage preemptible instances in your cluster, you can reduce your costs even further
 - Without using Cloud Dataproc, it can take from five to 30 minutes to create Spark and Hadoop clusters on-premises or through other Infrastructure-as-a-Service providers.
 - Cloud Dataproc clusters are quick to start, scale, and shut down, with each of these operations taking 90 seconds or less, on average
 - This means you can spend less time waiting for clusters and more hands-on time working with your data.
 - Cloud Dataproc has built-in integration with other GCP services, such as BigQuery, Cloud Storage, Cloud Bigtable, Stackdriver Logging, and Stackdriver Monitoring
 - This provides you with a complete data platform rather than just a Spark or Hadoop cluster
 - As a managed service, you can create clusters quickly, manage them easily, and save money by turning clusters off when you don't need them
 - With less time and money spent on administration, you can focus on your jobs and your data. 
 - If you’re already using Spark, Hadoop, Pig, or Hive, you don’t even need to learn new tools or APIs to use Cloud Dataproc
 - This makes it easy to move existing projects into Cloud Dataproc without redevelopment

_ **Cloud Dataflow vs Cloud Dataproc** _

 - Now, Cloud Dataproc and Cloud Dataflow can both be used for data processing, and there’s overlap in their batch and streaming capabilities.
 - So, how do you decide which product is a better fit for your environment?
 - Well, first, ask yourself whether you have dependencies on specific tools or packages in the Apache Hadoop or Spark ecosystem
 - If that’s the case, you’ll obviously want to use Cloud Dataproc.
 - If not, ask yourself whether you prefer a hands-on or DevOps approach to operations, or a hands-off or serverless approach
 - If you opt for the DevOps approach, you want to use Cloud Dataproc; otherwise, use Cloud Dataflow
