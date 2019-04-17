# Exam Readiness: AWS Certified Solutions Architect – Associate

## The Exam Overview

## Module 1 - Design Resilient Architectures

### RPO and RTO

* RPO Is Recovery Point Objective. How much data is lost if a system fails?
* RTO Is Recovery Time Objective. How long does it take for the system to recover and come back on-line again?

![rpo_rto](https://upload.wikimedia.org/wikipedia/en/6/69/RPO_RTO_example_converted.png)

### Text Axioms 1

* Expect "Single-AZ" will never be a right answer
* Using AWS managed services should always be prefered
* Fault-tolerant and high availability are not the same thing
  * Fault tolerant: Means that the system hides the failure from the users and there is no loss of service
  * High availability: Means that the system will always be up and it can fail-over in the event of failure
* Expect that everything will fail at some point and design accordingly

## Module 2 - Design Performant Architectures

Security:

* [AWS Shield](https://aws.amazon.com/shield/): WS Shield is a managed Distributed Denial of Service (DDoS) protection service
* [AWS WAF](https://aws.amazon.com/waf/): AWS WAF is a web application firewall that helps protect your web applications from common web exploits that could affect application availability, compromise security, or consume excessive resources

### Text Axioms 2

* If data is unstructured, Amazon S3 is generally the storage solution.
* Use caching strategically to improve performance.
* Know when and why to use Auto Scaling.
* Choose the instance and database type that makes the most sense for your workload and performance need.

## Module 3 - Specify Secure Applications and Architectures

### Text Axioms 3

* Look down the root user
* Security groups only allow. Network ACLs allow explicitly deny.
* Prefer IAM roles over access keys

## Module 4 - Design Cost-Optimized Architectures

### Text Axioms 4

* If you know it's going to be on, reserve it.
* Any unused CPU time, is a waste of money.
* Use the most cost-effective data storage service and class.
* Determine the most cost-effective EC2 pricing model and instance type for each workload.

## Module 5 - Define Operationally-excellent Architectures

### Text Axioms 5

* IAM Roles are easier and safer than keys and passwords.
* Monitor metrics across the system.
* Automate responses to metrics where appropriate
* Provide alerts for anomalous conditions