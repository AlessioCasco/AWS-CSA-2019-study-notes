# CHAPTER 3 | IAM Identity Access Management

## [What's IAM](https://aws.amazon.com/iam/)

Allows you to manage users and their level of access to the AWS console.

## IAM Consist of the following

* Users: People, end users.
* Groups: Collection of users.
* Policies: Are basically the Permissions. Are made up of Documents, formatted in JSON.
* Roles: Is a way to allow one part of AWS to another part.

## Features

* Centralised control of your AWS account.
* Shared Access to your AWS account.
* Gives you granular Permission.
* Does Identity Federation (Active directory, Facebook, etc)
* MultiFactor Authentication.
* Provides temporary access for users/devices etc.
* Allows you to set up your own password rotation policy.
* Supports PCI DSS compliance.
* integrated with a lot of AWS services.

## [From Console](https://aws.amazon.com/console/)

IAM users sign-in link:
You can customize the URL used by users to sign-in

## New Users and account set up

* IAM is universal, the region is on a global level.
* Root account: Is the user you used to register on AWS, no one should use it to log-in.
* Always enable MFA on your Root account.
* New Users have No permissions once created.
* Access keys ID & Secret are not the same as password.
* You can create and customize your password rotation policies.

## [Billing Alarm](https://docs.aws.amazon.com/AmazonCloudWatch/latest/monitoring/monitor_estimated_charges_with_cloudwatch.html)

You can set a billing alarm to get notified when the amount of spendings for the current month reaches your threshold.
Before doing it you probably have to go on:
```https://console.aws.amazon.com/billing/home?#/preferences```
and enable: Receive Billing Alerts

After that, you can go and use cloudwatch services to set a new Billing Alarm