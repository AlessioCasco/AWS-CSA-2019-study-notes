# Exam Tips

## Big Data

### Kinesis

* If in the exam you got a question which is talking about **consuming** social media feeds, or a way to **consume** big data into the cloud, chances are they are talking about [Kinesis](https://github.com/AlessioCasco/AWS-CSA-2019-study-notes/tree/master/Applicatio%20Services#kinesis).

### Redshift

* If in the question they use languages like business intelligence, or **applying business** intelligence to big data think about [Redshift](https://github.com/AlessioCasco/AWS-CSA-2019-study-notes/tree/master/Databases#redshift).

### Elastic MapReduce

* If in the questions they refer to big data **processing**, think about [Elastic Mapreduce](https://aws.amazon.com/emr/).

## EC2

### [EBS](https://github.com/AlessioCasco/AWS-CSA-2019-study-notes/blob/master/EC2/README.md#ami-types)

* EBS backed volumes are persistent
* Instance Store backed volumes are not persistent (ephemeral).
* EBS Volumes can be detached and reattached to other EC2 instances.
* Instance store volume cannot be detached and reattached to other instances - they exist only for the life of that instance.
* EBS volumes can be stopped; data will persists.
* Instance store volumes cannot be stopped - if you stop them, data will be lost.
* EBS Backed = Store Data for Long term.
* Instance Store = You should not use it for long-term data storage.

## OpsWorks

* If you got a question that is talking about **chef**, or **recipes** or **cookbooks**, think about [OpsWorks](https://aws.amazon.com/opsworks/)

## SWF Actors

* Workflow Started: An application that can initiate a workflow.
* Decider: Control the flow of activity tasks in a workflow execution.
* Activity Workers: Carry out activity tasks.

## [AWS Organizations](https://aws.amazon.com/organizations/)

Using AWS Organizations, you can manage multiple AWS accounts at once. With organizations, you can create groups of accounts a then apply policies to those groups.

### What organizations allow you to do

* Centrally manage policies across multiple AWS accounts.
* Control access to AWS services. Service Control Policies (SCPs) have priority over policies on the account.
* Automate AWS account creation and management.
* Consolidate billing across multiple AWS accounts.

![organization](https://docs.aws.amazon.com/organizations/latest/userguide/images/BasicOrganization.png)

### Other notes for Organizations

* Consolidating billing allows you to get volume discounts on all your accounts.
* Unused reserved instances for EC2 are applied across the group.
* CloudTrail is on a per account and per region basis but can be aggregated into a single bucket in the paying account.
* You can have 20 linked accounts only.

## Cross-Account Access

Many AWS customers use separate AWS accounts for their development and production resources. This separation allows them to cleanly separate different types of resources and can also provide some security benefits.

Cross-account access makes it easier for you to work productively within a multi-account (or multi-role) AWS environment by making it easy for you to switch roles within the AWS Management Console. You can now sign in to the console using your IAM user name then switch the console to manage another account without having to enter or remember another user name and password

## Tagging & Resource Groups

### What are tags

* Key-Value pairs attached to AWS resources.
* Metadata.
* Tags can sometimes be inherited.
  * Autoscaling, CloudFormation, and Elastic Beanstalk can create other resources.

### What are Resource Groups

Resource groups make it easy to group your resources using the tags that are assigned to them. You can group resources that share one or more tags.

Resource groups contain information such as:

* Region
* Name
* Health Checks

There are two types of resources groups:

* Classic Resource Groups: Classic ones are global
* AWS System Manager: These groups are based on the region.

## [VPC Peering](https://docs.aws.amazon.com/vpc/latest/peering/what-is-vpc-peering.html)

![vpc_peering](https://docs.aws.amazon.com/vpc/latest/peering/images/peering-intro-diagram.png)

VPC Peering is simply a connection between two VPCs that enables you to route traffic between them using private IP addresses. Instances in either VPC can communicate with each other as if they are within the same network, You can create a VPC peering connection between your own VPCs, or with a VPC in another AWS account within a **single reagion**.

AWS uses the existing infrastructure of a VPC to create a VPC peering connection; it's neither a gateway nor a VPN connection and does not rely on separate piece of physical hardware. There is no single point of failure for communication or a bandwidth bottleneck.

VPC Limitations:

* You cannot create a VPC peering connections between VPCs that have matching or overlapping CIDR block.
* You cannot create a VPC peering connection between VPCs in different regions.
* VPC peering does not support transitive peering relationships.

## [Direct Connect](https://aws.amazon.com/directconnect/)

AWS Direct Connect is a cloud service solution that makes it easy to establish a dedicated network connection from your premises to AWS. Using AWS Direct Connect, you can establish private connectivity between AWS and your datacenter, office, or colocation environment.

* Reduces costs when using a large amount of traffic.
* Increase reliability.
* Increase bandwidth.

VPNs connections **are not** direct connect!
Direct connections need a physical cable (Dedicated Line) between your facility up to your AWS Facility.

## [STS](https://docs.aws.amazon.com/STS/latest/APIReference/Welcome.html)

Grants users limited and temporary access to AWS resources. Users can come from three sources:

1) Federation (typically Active Directory)
   * Uses Security Assertion Markup Language ([SAML](https://en.wikipedia.org/wiki/Security_Assertion_Markup_Language))
   * Grants temporary access based off the users Active Directory credentials. This user does not need to be an IAM user.
   * [Single sign-on](https://en.wikipedia.org/wiki/Single_sign-on) allows users to log in to AWS console without the need of IAM credentials.
2) Federation with mobile apps.
   * Use Facebook/Amazon/Google or other [OpenID](https://openid.net/what-is-openid/) providers to log in
3) Cross-Account Access.
   * Let's users from one AWS account access resources in another.

### Key Terms

* Federation: Combining or join a list of users in one domain (such as IAM) with a list of users in another domain (such as Active Directory, Facebook etc)
* Identity Broker: A service that allows you to take identity from point A and join it (federate it) with point B
* Identity Store: Services like Active Directory, Facebook, Google etc
* Identities: A user of a service like Facebook etc.

### Scenario

Typical Authentication Work Flow:

1) Employee enters their username and password
2) The application calls an Identity Broker. The broker captures the username and password.
3) The Identity Broker uses the organization's LDAP directory to validate the employee's identity.
4) The identity Broker calls the new GetFederationToken function using IAM Credentials. The call must include an IAM policy and a duration (1 to 36 hours), along with a policy that specifies the permissions to be granted to the temporary security credentials.
5) The Security Token Service confirms that the policy of the IAM user making the call to GetFederationToken gives permission to create new tokens and then returns four values to the application:

   * Access key
   * secret access key
   * token
   * duration (the token's lifetime)

6) The Identity Broker returns the temporary security credentials to the reporting application.
7) the data storage application uses the temporary security credentials (including the token) to make a request to  Amazon S3.
8) Amazon S3 uses IAM to verify that the credentials allowed the requested operation on the given S3 bucket and key.
9) IAM provides S3 with the go-ahead to perform the requested operation.

#### In the Eaxm

* Scenario 1

1) Develop an Identity Broker to communicate with LDAP and AWS STS.
2) Identity Broker always authenticates with LDAP **first**, then with AWS STS.
3) The application then gets temporary access to AWS resources.

* Scenario 2

1) Develop an Identity Broker to communicate with LDAP and AWS STS.
2) Identity Broker always authenticates with LDAP **first**, gets an IAM Role associated with a user.
3) The application then authenticates with STS and assumes that IAM Role.
4) The application uses that IAM role to interact with S3.

## Active Directory Integration

* Can you authenticate with Active Directory? ==> Yes, using SAML

* How do you authenticate to get the security credentials into Active Directory? ==> You always authenticate with Active Directory first and then you are assigned the temporary security credentials.

## [WorkSpaces](https://aws.amazon.com/workspaces/)

You can use Amazon WorkSpaces to provision either Windows or Linux desktops in just a few minutes and quickly scale to provide thousands of desktops to workers across the globe.

Quick Facts:

* Windows 7, Windows 10, or Amazon Linux 2 desktop experience.
* By default, users can personalize their workspaces. This can be locked down by an administrator.
* By default, you will be given local admin access, so you can install your own applications.
* Workspaces are persistent.
* All data on the D:\ is backed up every 12 hours.
* You do not need an AWS account to login into workspaces.

## [ECS Amazon Elastic Container Service](https://aws.amazon.com/ecs/)

### [What is Docker](https://en.wikipedia.org/wiki/Docker_(software))

![docker_vs_vm](https://i0.wp.com/blog.docker.com/wp-content/uploads/Blog.-Are-containers-..VM-Image-1.png?w=1600&ssl=1)

Docker is used to run software packages called containers. Containers are isolated from each other and bundle their own application, tools, libraries and configuration files; they can communicate with each other through well-defined channels. All containers are run by a single operating system kernel and are thus more lightweight than virtual machines. Containers are created from images that specify their precise contents.

### About ECS

* ECS is a regional service that you can use in one or more AZs across a new or existing, VPC to schedule the placement of containers across your cluster based on your resource needs, isolation policies, and availability requirements.
* ECS eliminates the need for you to operate your own cluster management and config management systems, or to worry about scaling your management infrastructure.
* ECS can also be used to create a consistent deployment and build experience, manage and scale batch and [ETL workloads](https://en.wikipedia.org/wiki/Extract,_transform,_load), and build sophisticated application architectures on a microservice level.

### About Containers

* Containers are a method of operating system virtualization that allows you to run the application and its dependencies in resource-isolated process.
* Containers have everything the software needs to run (libraries, system tools, code, and runtime).
* Containers are created from a read-only template called an image.

### What's a docker Image

* An image is a read-only template with instructions for creating a Docker container. It contains:
  * an ordered collection of root filesystem changes and the corresponding execution parameters for use within a container runtime.
* An image is created form a Dockerfile, a plain text file that specifies the components that are to be included in the container.
* Images are stored in a registry, such as DockerHub or [AWS ECR](https://aws.amazon.com/ecr/)

    _do yourself a favour.....DO NOT USE AWS ECR_

### ECS Task Definitions

A Task Definition is required to run Docker containers in ECS.

* Task Definitions are text files in JSON format that describe one or more containers that form your application.
* Some of the parameters you can specify in a task definition include:
  * Which Docker images to use with the containers in your task
  * How much CPU and memory to use with each container
  * Whether containers are linked together in a task
  * The docker networking mode to use for the containers in your task
  * What (if any) ports from the container are mapped to the host container service
  * Whether the task should continue to run if the container finishes or fails
  * The command the container should run when it is started
  * What (if any) env variables should be passed to the container when it starts.
  * Any data volumes that should be used with containers in the task
  * What (if any) IAM role your tasks should use for permissions

### ECS Services

* An ECS service allows you to run and maintain a specified number (or, the "desired count") of instances of a task definition simultaneously in and ECS cluster
* Think of services like Auto-Scaling groups for ECS
* If a task should fail or stop, the ECS service scheduler launches another instance of your task definition to replace it and maintain the desired count of tasks in the service.

### ECS Clusters

* An ECS cluster is a logical grouping of container instances that you can place tasks on. When you first use the Amazon ECS service, a default cluster is created for you, but you can create multiple clusters in an account to keep your resources separate.
* Concepts:
  * Clusters can contain multiple different container instance types
  * Clusters are region-specific
  * Container instances can only be part of one cluster at a time.
  * You can create IAM policies for your clusters to allow or restrict users' access to specific clusters

### ECS Scheduling

* Service Scheduler:
  * Ensures that the specific number of tasks are constantly running and reschedules tasks when a task fails (for example, if the underlying container instance fails for some reason).
  * Can ensure tasks are registered against and ELB.

* Custom Scheduler:
  * You can create your own schedulers that meet your business needs.
  * Leverage third-party schedulers such as Blox.

* The Amazon ECS schedulers leverage the same cluster state information provided by the ECS API to make appropriate placement decisions.

### ECS Container Agent

ECS Container Agent allows container instances to connect to your cluster. The ECS container agent is included in the ECS optimized AMI, but you can also install it on any EC2 instance that supports ECS specifications. The Amazon ECS container agent is only supported on EC2 instances.

* Pre-installed on special ECS AMIs
* Linux based:
  * Works with AWS Linux, Ubuntu, Redhat, CentOS, etc.
  * Will **not** work with Windows.

### ECS Security

* IAM Roles:
  * EC2 instances use an IAM role to access ECS.
  * ECS tasks use an IAM role to access services and resources.
* Security Groups attach at the instance-level (i.e. the host...not the task or container)
* You can access and configure the OS of the EC2 instances in your ECS cluster

### ECS Limits

* Soft Limits:
  * Clusters per Region (default = 1000)
  * Instances per Cluster (default = 1000)
  * Services per Cluster (default = 500)
* Hard Limits:
  * One Load Balancer per Service
  * 1000 Tasks per Service (the "desired count")
  * Max 10 Containers per Task Defintion
  * Max 10 Tasks per Instance (host)

### Recap

* ECS - Amazon's managed EC2 container service. Allows you to manage Docker containers on a cluster or EC2 instances.
* Containers are a method of operating system virtualization that allows you to run an application and its dependencies in resource-isolate processes.
* Containers are created from a read-only template called Image
* An image is a read-only template with instructions for creating a Docker container.
* Images are stored in a Registry.
* Amazon EC2 Container Registry is a managed AWS docker registry service (Amazon ECR)
* A task definition is required to run Docker containers in Amazon ECS.
* Task Definitions are text files in JSON format that describe one or more containers that form your application.
* Think of a task definition as a cloud formation template but for docker.
* An Amazon ECS service allows you to run and maintain a specified number of instances of a task definition simultaneously in an ECS cluster.
* Think of Services like Auto-Scaling groups for ECS.
* An Amazon ECS cluster is a logical grouping of containers instances that you can place tasks on.
* Clusters can contain multiple different container instances types.
* Clusters are region-specific
* Container instances can only be part of one cluster at the time.
* You can create IAM policies for your clusters to allow or restrict users' access to specific clusters.
* You can schedule ECS in two ways:
  * Service scheduler
  * Custom scheduler
* ECS agent to connect EC2 instances to your ECS cluster. Linux Only
* IAM with ECS to restrict access
* Security groups operate at the instance level, not at the task or container level.