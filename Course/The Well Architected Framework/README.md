# CHAPTER 9 | The Well Architected Framework

## Best Practices

### Business Benefits of Cloud

* Almost zero upfront infrastructure investments
* Just-in-time infrastructure
* More efficient resource utilization
* Usage-based costing
* Reduced time to market

### Technical Benefits of the Cloud

* Automation: Scriptable infrastructure
* Auto-scaling
* Proactive Scaling
* More efficient development lifecycle
* Improved Testability
* Disaster Recovery and Business Continuity
* "Overflow" the traffic to the cloud

### Design for failure

* Be a pessimist when designing architectures in the cloud; assume things will fail. In other words, always design, implement and deploy for automated recovery from failure. By being a pessimist.

### Decouple Your Components

* The key is to build components that do not have tight dependencies on each other, so that if one component were to die(fail), sleep(not respond) or remain busy(slow to respond) for some reason, the other components in the system are built so as to continue to work as if no failure is happening.
* In essence, loose coupling isolates the various layers and components of your application so that each component interacts async with the others and treats them as a "black box".

### Implement Elasticity

* The cloud brings a new concept of elasticity in your applications. Elasticity can be implemented in 3 ways:
  1) Proactive Cyclic Scaling: Periodic scaling that occurs at a fixed interval (daily, weekly, monthly, quarterly)
  2) Proactive Event-base Scaling: Scaling just when you are expecting a big surge of traffic requests due to a scheduled business event (new product launch, marketing campaigns)
  3) Auto-scaling based on demand: By using monitoring service, your system can send triggers to take appropriate actions so that it scales up or down based on metrics (utilization of the servers or network i/o)

### Secure your applications

* Only permit what it's needed, nothing else.
* Shut down services you don't use.

## [The Well-Architected Framework](https://aws.amazon.com/architecture/well-architected/)

The Well-Architected Framework has been developed to help cloud architects build secure, high-performing, resilient, and efficient infrastructure for their applications.

Five pillars:

* Operational excellence
* Security
* Reliability
* Performance efficiency
* Cost optimization

### General Design Principles

* Stop guessing your capacity needs.
* Test systems at production scale.
* Automate to make architectural experimentation easier.
* Allow for evolutionary architectures.
* Data-driven architectures.
* Improve through game days.

## [Pillar 1 Security](https://d1.awsstatic.com/whitepapers/architecture/AWS-Security-Pillar.pdf)

### Design Principles

* Apply security at all layers.
* Enable traceability.
* Automate responses to security events.
* Focus on securing your system.
* Automate security best practices.

### AWS Shared Responsability Model

![aws_resp_model](https://d1.awsstatic.com/security-center/Shared_Responsibility_Model_V2.59d1eccec334b366627e9295b304202faf7b899b.jpg)

### Definition

Security in the cloud consists of 4 areas:

#### Data Protections

Before architecting any system, foundational practices that influence security should be in place. For example, data classification provides a way to categorize organizational data based on levels of sensitivity, and encryption protects data
by way of rendering it unintelligible to unauthorized access. These methods are important because they support objectives such as preventing financial loss or complying with regulatory obligations.

In AWS the following practices help to protect your data:

* AWS customers maintain full control over their data
* AWS makes it easier for you to encrypt your data and manage keys, including regular key rotation.
* Detailed logging is available that contains important content, such as file access and changes.
* AWS has designed storage systems for exceptional resiliency.
* Versioning which can be part of a larger data lifecycle-management process.
* AWS never initiates the movement of data between regions.

Questions you should ask yourself:

* How are you encrypting your data at rest?
* How are you encrypting your data in transit (SSL)?

#### Privilege Management

Privilege Management ensures that only authorized and authenticated users are able to access your resources, and only in a manner that is intended. It can include:

* Access Control Lists (ACLs).
* Role Based Access Controls.
* Password Management (such as password rotation policies).

Questions you should ask yourself:

* How are you protecting access to and use the AWS root account credentials?
* How are you defining roles and responsibilities of system users to control human access to the AWS Management Console and APIs?
* How are you limiting automated access (such as from applications, scripts, or 3rd party tools or services) to AWS resources?
* How are you managing keys and credentials?

#### Infrastructure Protection

Outside of Cloud, this is how you protect your data centre. RFID controls, security, lockable cabinets, CCTV etc. Within AWS they handle this so infrastructure protection exists at a VPC level.

Questions you should ask yourself:

* How are you enforcing network and host-level boundary protection?
* How are you enforcing AWS service level protection?
* How are you protecting the integrity of the operating system on your AWS EC2 instances?

#### Detective Controls

You can use detective controls to detect or identify a security breach. AWS Services to achieve this include

* AWS Cloudtrail
* AWS CloudWatch
* AWS Config
* AWS S3
* AWS Glacier

Questions you should ask yourself:

* How are you capturing and analyzing your logs?

### Key AWS Services

* Data Protection:
  * Encrypt both in transit and at rest using - ELB, EBS, S3 and RDS
* Privilege Management:
  * IAM, MFA
* Infrastructure Protection:
  * VPC
* Detective Controls:
  * AWS Cloud Trail, AWS Config, AWS Cloud Watch

## [Pillar 2 Reliability](https://d1.awsstatic.com/whitepapers/architecture/AWS-Reliability-Pillar.pdf)

The reliability pillar encompasses the ability of a system to recover from infrastructure or service disruptions, dynamically acquire computing resources to meet demand, and mitigate disruptions such as misconfigurations or transient network issues.

### Design Principles

* Test recovery procedures.
* Automatically recover from failure (KPI).
* Scale horizontally to increase aggregate system availability.
* Stop guessing capacity.

### Definition

Reliability in the cloud consists of 3 areas:

#### Foundations

Before architecting any system, you need to make sure you have the prerequisite foundations.
With AWS, they handle most of the foundations for you. The cloud is designed to be essentially limitless meaning that AWS handle the networking and compute requirements themselves. However, they do set the [service limits](https://docs.aws.amazon.com/general/latest/gr/aws_service_limits.html) to stop customers from accidentally over-provisioning resources.

Questions you should ask yourself:

* How are you managing AWS service limits for your account?
* How are you planning your network topology on AWS?
* Do you have an escalation path to deal with technical issues?

#### Change Management

You need to be aware of how change affects a system so that you can plan proactively around it. Monitoring allows you to detect any changes to your environment and react.

With AWS, you can use CloudWatch to monitor your environment and services such as autoscaling to automate change in response to your production environment.

Questions you should ask yourself:

* How does your system adapt to changes in demand?
* How are you monitoring AWS resources?
* How are you executing change management?

#### Failure Mangement

With cloud, you should always architect your systems with the assumptions that failure will occur. You should become aware of these failures, how they occurred, how to respond to them and then plan on how to prevent these from happening again.

Questions you should ask yourself:

* How are you backing up your data?
* How does your system withstand component failures?
* How are you planning for recovery?

### Key AWS Services

* Foundations:
  * IAM, VPC
* Change Mangement:
  * AWS CloudTrail
* Failure Management:
  * AWS CloudFormation, AWS RDS multi AZ

## [Pillar 3 Performance Efficiency](https://d1.awsstatic.com/whitepapers/architecture/AWS-Performance-Efficiency-Pillar.pdf)

The performance efficiency pillar focuses on the efficient use of computing resources to meet requirements and how to maintain that efficiency as demand changes and technologies evolve. Keep evolving your platform

### Design Principles

* Democratize advanced technologies.
* Go global in minutes.
* Use server-less architectures.
* Experiment more often.

### Definition

Performance Efficiency in the cloud consists of 4 areas:

#### Compute

When architecting your use of compute, you should take advantage of elasticity mechanisms that can ensure that you have sufficient capacity to sustain performance as demand changes. You should also make sure to chose the right kind of server for your needs.

Questions you should ask yourself:

* How do you select the appropriate instance type for your system?
* How do you ensure that you continue to have the most appropriate instance type as new instance types and features are introduced?
* How do you monitor your instances post-launch to ensure they are performing as expected?
* How do you ensure that the number of your instances match demand?

#### Storage

The optimal storage solution for a particular system varies based on the kind of access method (block, file, or object) you use, patterns of access (random or sequential), throughput required, frequency of access (online, offline, archival), frequency of update (WORM, dynamic), and availability and durability
constraints.

In AWS storage is virtualized, and there are a number of different storage types.
This makes it easier to match your storage methods more closely with your needs, and it also offers storage options that are not easily achievable with on-premises infrastructure.

Questions you should ask yourself:

* How do you select the appropriate storage solution for your system?
* How do you ensure that you continue to have the most appropriate storage solution as new storage solution features are launched?
* How do you monitor your storage solution to ensure it is performing as expected?
* How do you ensure that the capacity and throughput of your storage solutions match demand?

#### Database

The optimal database solution for a particular system can vary based on your requirements for availability, consistency, partition tolerance, latency, durability, scalability, and query capability. Many systems use different database solutions for different subsystems and enable different features to improve performance.

Questions you should ask yourself:

* How do you select the appropriate database solution for your system?
* How do you ensure that you continue to have the most appropriate database solution and features as new database solution and features are launched?
* How do you monitor your databases to ensure performance is as expected?
* How do you ensure the capacity and throughput of your databases match demand?

#### Space-Time trade-off

Using AWS you can use services such as RDS to add read replicas, reducing the load on your database and creating multiple copies of the database. This helps to lower latency.

You can use Direct Connect to provide predictable latency between your HQ and AWS

You can use the global infrastructure to have multiple copies of your environment, in regions that are closest to our customer base. You can also use caching services such as ElastiCache or CloudFront to reduce latency.

Questions you should ask yourself:

* How do you select the appropriate proximity and caching solutions for your system?
* How do you ensure that you continue to have the most appropriate proximity and caching solutions as new solutions are launched?
* How do you monitor your proximity and caching solutions to ensure performance is as expected?
* How do you ensure that the proximity and caching solutions you have matches demand?

### Key AWS Services

* Compute
  * Autoscaling
* Storage
  * EBS, S3, Glacier
* Database
  * RDS, DynamoDB, Redshift
* Space-Time Trade-Off
  * CloudFront, ElasticCache, Direct Connect, RDS Read Replicas etc

## [Pillar 4 Cost Optimization](https://d1.awsstatic.com/whitepapers/architecture/AWS-Cost-Optimization-Pillar.pdf)

Use the Cost Optimization pillar to reduce your costs to a minimum and use those savings for other parts of your business. A cost-optimized system allows you to pay the lowest price possible while still achieving your business objectives.

### Design Principles

* Transparently attribute expenditure.
* Use managed services to reduce the cost of ownership.
* Trade capital expense for operating expense.
* Benefit from economies of scale.
* Stop spending money on data centre operations.

### Definition

Cost optimization in the cloud consists of 4 areas:

#### Matched supply and demand

Try to optimally align supply with demand. Don't overprovision or under-provision, instead of as demand grows, so should your supply of computing resources. Think of things like Autoscaling which scale with demand.

Similarly in a server-less context, use services such as Lambda that only execute when a request comes in.

Services such as CloudWatch can also help you keep track as to what your demand is.

Questions you should ask yourself:

* How do you make sure your capacity matches but does not substantially exceed what you need?
* How are you optimizing your usage of AWS services?

#### Cost-effective resources

Using the correct instance type can be key to cost savings. For example, you might have a reporting process that is running on a t2-Micro and it takes 7 hours to complete. That same process could be run on an m4.2xlarge in a manner of minutes. The result remains the same but the t2.micro is more expensive because it ran for longer.

A well-architected system will use the most cost-efficient resources to reach the end business goal

Questions you should ask yourself:

* Have you selected the appropriate resource types to meet your cost targets?
* Have you selected the appropriate pricing model to meet your cost targets?
* Are there managed services (higher-level services than Amazon EC2, Amazon EBS, and Amazon S3) that you can use improve your ROI (return on investment)?

#### Expenditure Awareness

With cloud, you no longer have to go out and get quotes on physical servers, choose a supplier, have those resources delivered, installed, made available etc. You can provision things within seconds, however, this comes with its own issues.

Many organizations have different teams, each with their own AWS accounts. Being aware of what each team is spending and where is crucial to any well-architected system.

You can use cost allocation tags to track this, billing alerts as well as consolidated billing.

Questions you should ask yourself:

* What access control and procedures do you have in place to govern your AWS costs?
* How are you monitoring usage and spending?
* How do you decommission resources that you no longer need, or stop resources that are temporarily not needed?
* How do you consider data-transfer charges when designing your architecture?

####  Optimizing Over Time

AWS moves FAST. There are hundreds of new services (and potentially 1000 new services this year). A service that you chose yesterday may not be the best service to be using today.

For example, consider MySQL RDS, Aurora was launched at re:invent 2014 and is now out of preview. Aurora may be a better option now for your business because of its performance and redundancy.

You should keep track of the changes made to AWS and constantly re-evaluate your existing architecture. You can do this by subscribing to AWS blog and by using services such as Trusted Advisor.

Questions you should ask yourself:

* How do you manage and/or consider the adoption of new services?

### Key AWS Services

* Matched supply and demand
  * Autoscaling
* Cost-effective resources
  * EC2 (reserved instances), AWS Trusted Advisor
* Expenditure Awareness
  * CloudWatch Alarms, SNS
* Optimizing over time
  * AWS Blog, AWS Trusted Advisor

## [Pillar 5 Operational Excellence](https://d1.awsstatic.com/whitepapers/architecture/AWS-Operational-Excellence-Pillar.pdf)

The Operational Excellence pillar includes operational practices and procedures used to manage production workloads.

This includes how planned changes are executed, as well as responses to unexpected operational events.

Change execution and responses should be automated. All processes and procedures of operational excellence should be documented, tested and regularly reviewed.

### Design Principles

* Perform operations with code.
* Align operations processes to business objectives.
* Make regular, small, incremental changes.
* Test for responses to unexpected events.
* Learn from operational events and failures.
* Keep operations procedures current.

### Definition

There are three best practice areas of Operational Excellence in the cloud:

#### Preparation

Effective preparation is required to drive operational excellence. Operations checklists will ensure that workloads are ready for production operation, and prevent unintentional production promotion without effective preparation.

Workloads should have:

* Runbooks: operations guidance that operations teams can refer to so they can perform normal daily tasks.

* Playbooks: guidance for responding to unexpected operational events. Playbooks should include response plans, as well as escalation paths and stakeholder notifications.

In AWS there are several methods, services and features that can be used to support operational readiness and the ability to prepare for normal day-to-day operations as well as unexpected operational events:

* CloudFormation: can be used to ensure that environments contain all required resources when deployed to production and the configuration of the environment is based on tested best practices, which reduces the opportunity for human error.

* Autoscaling or other automated scaling mechanisms: This will allow workloads to automatically respond when business-related events affect operational needs.

* AWS Config: With the AWS Config rules feature create mechanisms to automatically track and respond to changes in your AWS workloads and environments.

    It is also important to use features like tagging to make sure all resources in a workload can be easily identified when needed during operations and responses.

* Document everything:

    Be sure that documentation doesn't become stale or out of date as procedures change.

    Without application designs, environment configs, resource configs, response plans, and mitigation plans, documentation is not complete.

    If documentation is not updated and tested regularly, it will not be useful when unexpected operational events occur. If workloads are not reviewed before production, operations will be affected when undetected issues occur.

    If resources are not documented, when operational events occur, determining how to respond will be more difficult while the correct resources are identified.

Questions you should ask yourself:

* What best practices for cloud operations are your using?
* How are you doing configuration management for your workload?

#### Operation

Operations should be standardized and manageable on a routine basis. The focus should be on automation, small frequent changes, regular QA testing, and defined mechanisms to track, audit, roll back and review changes. Changes should not be large and infrequent, they should not require scheduled downtime, and they should not require manual execution. A wide range of logs and metrics that are based on key operational indicators for a workload should be collected and reviewed to ensure continuous operations.

In AWS you can set up a continuous integration / continuous deployment (CI/CD) pipeline. Release management processes, whether manual or automated, should be tested and be based on small incremental changes, and tracked versions. You should be able to revert changes that introduce operational issues without causing any operational impact.

Routine operations, as well as responses to unplanned events, should be automated. Manual processes for deployments, release management, changes and rollbacks should be avoided.

Releases should not be large batches that are done infrequently.

Rollbacks are more difficult in large changes, and failing to have a rollback plan or the ability to mitigate failure impacts will prevent continuity of operations.

Align monitoring to business needs, so that the responses are effective at maintaining business continuity. Monitoring that is ad hoc and not centralized, with responses that are manual, will cause more impact to operations during unexpected events.

Questions you should ask yourself:

* How are you evolving your workload while minimizing the impact of change?
* How do you monitor your workload to ensure it is operating as expected?

#### Response

Responses to unexpected operational events should be automated. This is not just for alerting but also for mitigation, remediation, rollback and recovery.

Alerts should be timely and should invoke escalations when responses are not adequate to mitigate the impact of operational events.

QA mechanisms should be in place to automatically roll back failed deployments.

Responses should follow a pre-defined playbook that involves stakeholders, the escalation process and procedures. Escalation paths should be defined and include both functional and hierarchical escalation capabilities. Hierarchical escalation should be automated and escalated priority should result in stakeholder notifications.

Questions you should ask yourself:

* How do respond to unplanned operational events?
* How is escalation managed when responding to unplanned operational events?

### Key AWS Services

* Preparation: AWS Config provides a detailed inventory of your AWS resources and configuration, and continuously records configuration changes. AWS Service Catalog helps to create a standardized set of service offerings that are aligned to best practices. Designing workloads that use automation with services like AutoScaling, AWS SQS are good methods to ensure continuous operations in the event of unexpected operational events.
* Operations: AWS CodeCommit, AWS CodeDeploy and AWS CodePipeline can be used to manage and automate code changes to AWS workloads. Use AWS SDKs or 3rd party libraries to automate operational changes. Use AWS CloudTrail to audit and track changes made to AWS events.
* Responses: Take advantage of all of the AWS CloudWatch service features for effective and automated responses. CloudWatch alarms can be used to set thresholds for alerting and notification, and CloudWatch events can trigger notifications and automated responses.