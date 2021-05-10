# Highly Available app

Highly available systems are reliable in the sense that they continue operating even when critical components fail. They are also resilient, meaning that they are able to simply handle failure without service disruption or data loss, and seamlessly recover from such failure.

### Diagram 1

![vault](./DIAGRAM.png)

### Diagram 2

![vault](./diagram_available_app.png)

### Diagram 3 (mine):

![vault](./diagram_mon.png)

### Concepts:

__Multi az - app deployed to 2 or more zones:__

Availabilty of our app -> Multi avalaiablaty zones, multi could environment. You can place instances in different AZs.

Each Region has multiple, isolated locations known as Availability Zones. When you launch an instance, you can select an Availability Zone or let us choose one for you. If you distribute your instances across multiple Availability Zones and one instance fails, you can design your application so that an instance in another Availability Zone can handle requests.

Customers who care about the availability and performance of their applications want to deploy these applications across multiple AZs in the same region for fault tolerance and low latency. AZs are connected to each other with fast, private fiber-optic networking, enabling you to easily architect applications that automatically fail-over between AZs without interruption.

This ensures that customers avoid having a critical service dependency on a single data center. AWS can conduct maintenance activities without making any critical service temporarily unavailable to any customer.

__Monitoring - Cloud Watch:__

Amazon CloudWatch is a monitoring and management service that provides data and actionable insights for AWS, hybrid, and on-premises applications and infrastructure resources. With CloudWatch, you can collect and access all your performance and operational data in form of logs and metrics from a single platform. This allows you to overcome the challenge of monitoring individual systems and applications in silos (server, network, database, etc.). CloudWatch enables you to monitor your complete stack (applications, infrastructure, and services) and leverage alarms, logs, and events data to take automated actions and reduce Mean Time to Resolution (MTTR). This frees up important resources and allows you to focus on building applications and business value.

You can use CloudWatch Container Insights to monitor, troubleshoot, and alarm on your containerized applications and microservices.

CloudWatch gives you actionable insights that help you optimize application performance, manage resource utilization, and understand system-wide operational health.

Amazon CloudWatch is basically a metrics repository. An AWS service—such as Amazon EC2—puts metrics into the repository, and you retrieve statistics based on those metrics. If you put your own custom metrics into the repository, you can retrieve statistics on these metrics as well.

You can use metrics to calculate statistics and then present the data graphically in the CloudWatch console.

You can configure alarm actions to stop, start, or terminate an Amazon EC2 instance when certain criteria are met. In addition, you can create alarms that initiate Amazon EC2 Auto Scaling and Amazon Simple Notification Service (Amazon SNS) actions on your behalf.

Monitors instance metrics. Monitoring system for AWS resources. For example, send notifications when load is at 70%.

__Load balancing - app load balancer, network load balancer:__

Balance traffic between the nodes of the architecture. You can launch several EC2 instances and distribute traffic between them.

Elastic Load Balancing automatically distributes incoming application traffic across multiple targets, such as Amazon EC2 instances, containers, IP addresses, Lambda functions, and virtual appliances. It can handle the varying load of your application traffic in a single Availability Zone or across multiple Availability Zones. Elastic Load Balancing offers four types of load balancers that all feature the high availability, automatic scaling, and robust security necessary to make your applications fault tolerant.

If one of these instances is experiencing heavy loads, traffic can be redirected to the others.

Elastic Load Balancing types:

- Application Load Balancer

Routes and load balances at the application layer (HTTP/HTTPS), and supports path-based routing. An Application Load Balancer can route requests to ports on one or more registered targets, such as EC2 instances, in your virtual private cloud (VPC).

- Network Load Balancer

Routes and load balances at the transport layer (TCP/UDP Layer-4), based on address information extracted from the TCP packet header, not from packet content. Network Load Balancers can handle traffic bursts, retain the source IP of the client, and use a fixed IP for the life of the load balancer.

- Gateway Load Balancer

Distributes traffic to a fleet of appliance instances, providing scale, availability, and simplicity for third-party virtual appliances, such as firewalls, intrusion detection and prevention systems, and other appliances. Gateway Load Balancers work with virtual appliances that support the GENEVE protocol. Additional technical integration is required, so make sure that you consult the user guide before choosing a Gateway Load Balancer.

__SNS (alarms 65/70%) Simple Notification Service:__

Amazon Simple Notification Service (Amazon SNS) is a fully managed messaging service for both application-to-application (A2A) and application-to-person (A2P) communication.

Amazon SNS leverages the proven AWS cloud to dynamically scale with your application. Amazon SNS is a fully managed service, taking care of the heavy lifting related to capacity planning, provisioning, monitoring, and patching. The service is designed to handle high-throughput, bursty traffic patterns and enables you to send millions of messages per second.

We want to make it even easier for developers to build highly functional and architecturally complex applications on AWS. It turns out that applications of this type can often benefit from a publish/subscribe messaging paradigm. In such a system, publishers and receivers of messages are decoupled and unaware of each other’s existence. The receivers (also known as subscribers) express interest in certain topics. The senders (publishers) can send a message to a topic. The message will then be immediately delivered or pushed to all of the subscribers to the topic.

Provices notificacions when an order is placed, or an instance is experiencing heavy load.

__Health checks CPU usage etc:__

Communicates with load balancer and auto scaling to manage the traffic flow and instance management. Monitor the status of instances and terminate and replace any deemed unhealthy.

Your Classic Load Balancer periodically sends requests to its registered instances to test their status. These tests are called health checks. The status of the instances that are healthy at the time of the health check is InService. The status of any instances that are unhealthy at the time of the health check is OutOfService. The load balancer performs health checks on all registered instances, whether the instance is in a healthy state or an unhealthy state. 

The load balancer checks the health of the registered instances using either the default health check configuration provided by Elastic Load Balancing or a health check configuration that you configure.

The health status of an Auto Scaling instance is either healthy or unhealthy. All instances in your Auto Scaling group start in the healthy state. Instances are assumed to be healthy unless Amazon EC2 Auto Scaling receives notification that they are unhealthy. This notification can come from one or more of the following sources: Amazon EC2, Elastic Load Balancing (ELB), or a custom health check.

After Amazon EC2 Auto Scaling marks an instance as unhealthy, it is scheduled for replacement. If you do not want instances to be replaced, you can suspend the health check process for any individual Auto Scaling group. 

__Route 53 DNS service:__

AWS service - traffic diversion. With route 53 we can reroute traffic from ireland to london if ireland is down.

A DNS that translates www.website.com to an IP (0.0.0.0/0).

It allows users to access the server through an address rather tan an IP.

Amazon Route 53 is a highly available and scalable cloud Domain Name System (DNS) web service. It is designed to give developers and businesses an extremely reliable and cost effective way to route end users to Internet applications by translating names like www.example.com into the numeric IP addresses like 192.0.2.1 that computers use to connect to each other.

Amazon Route 53 effectively connects user requests to infrastructure running in AWS – such as Amazon EC2 instances, Elastic Load Balancing load balancers, or Amazon S3 buckets – and can also be used to route users to infrastructure outside of AWS. You can use Amazon Route 53 to configure DNS health checks to route traffic to healthy endpoints or to independently monitor the health of your application and its endpoints. Amazon Route 53 Traffic Flow makes it easy for you to manage traffic globally through a variety of routing types.

__Auto-scaling horizontal and vertical scaling:__

Use auto-scaling to detect when loads increase, and then dynamically add more instances. Auto scaling group spins up nodes to meet a given capicity. Works accross multiple AZ.

Auto scaling spins up the instances based on the current demand to optimise performance.

- Vertical Scaling - increasing the size of instance (RAM, CPU, etc.).

- Horizontal Scaling - add more instances (replication).

AWS Auto Scaling monitors your applications and automatically adjusts capacity to maintain steady, predictable performance at the lowest possible cost. Using AWS Auto Scaling, it’s easy to setup application scaling for multiple resources across multiple services in minutes.

To use Elastic Load Balancing with your Auto Scaling group, you attach the load balancer to your Auto Scaling group to register the group with the load balancer. Your load balancer acts as a single point of contact for all incoming web traffic to your Auto Scaling group.

When you use Elastic Load Balancing with your Auto Scaling group, it's not necessary to register individual EC2 instances with the load balancer. Instances that are launched by your Auto Scaling group are automatically registered with the load balancer. Likewise, instances that are terminated by your Auto Scaling group are automatically deregistered from the load balancer.

After attaching a load balancer to your Auto Scaling group, you can configure your Auto Scaling group to use Elastic Load Balancing metrics such as the Application Load Balancer request count per target (or other metrics) to scale the number of instances in the group as the demand on your instances changes.

You can also optionally enable Amazon EC2 Auto Scaling to replace instances in your Auto Scaling group based on health checks provided by Elastic Load Balancing. Otherwise, you can create a CloudWatch alarm that notifies you if the healthy host count of the target group is lower than allowed.

Amazon EC2 Auto Scaling can determine the health status of an instance using one or more of the following:

- Status checks provided by Amazon EC2 to identify hardware and software issues that may impair an instance. 

_Questions:_

1. What is our job role?: Make sure the app is running all the time.

2. How can we find out if something goes bad?: Monitoring (Cloud Watch).

3. How to make application highly available: deploying into multiple AZs, multi-cloud environment (next step) [trending clouds: aws, azure, gcp, etc].

4. Reason why we might use multi cloud is because one of the cloud providers might have a failure.

If we introduce new technology, the cto will ask:

- How much will it cost.
- When will i get my money back/how long will it take.
- What are the benefits.
- Security.
- We can let they know all the details regarding real scenarios, incidents, to see the benefits.

DEFINITELY IS BENEFIT OF THE BUSINESS -> SAVING MONEY.

The three main constraints are:

- Cost.
- Quality.
- Time.

A distributed denial-of-service (DDoS) attack is a malicious attempt to disrupt the normal traffic of a targeted server, service or network by overwhelming the target or its surrounding infrastructure with a flood of Internet traffic -> we need to make sure that everything is safe.

Scaling:

- Scaling up is better for applications in which you don't expect a big spike in usage.

- Scaling out is better for applications with sudden usage spikes.

- Vertical Scaling - increasing the size of instance (RAM, CPU, etc.).

- Horizontal Scaling - add more instances (replication).

WE HAVE TO MAKE SURE THAT THE APP IS RUNNING -> CUSTOMER SATISFACTION.
