# CHAPTER 2 | 10K Foot Overview

Thinks you will need to know to pass the exam:

## [aws global infrastructure](https://aws.amazon.com/about-aws/global-infrastructure/)

* Think of an Availability Zone as a Data Center.
An Az is one or more data centres, each with redundant power, networking and connectivity.

### region

* A region is a geographical area. Each region consists of 2 or more AZ

        Tip: US-East (N Virginia) it's the oldest region, where new services come out first. It's also the region that goes down the most (once per year at the time of writing :-)), avoid production workloads there.

* Edge Location are endpoints used for caching by AWS.

## Security, Identity & Compliance

* IAM (Identity Access Managment)

## Compute

* Mostly around EC2 & Lamba

## Storage

* All around S3

## Database

* Around RDS, DynamoDB and Redshift

## Network & Content Delivery

* Route 53 for Amazon DNS servers, VPC's for virtual cloud and CloudFront for CDN's