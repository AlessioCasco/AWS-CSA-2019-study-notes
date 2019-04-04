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