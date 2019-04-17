# CHAPTER 7 | VPC

## VPC

### [Wat's a VPC](https://aws.amazon.com/vpc/)

Think of a VPC as a virtual data centre in the cloud.

Amazon Virtual Private Cloud (Amazon VPC) lets you provision a logically isolated section of the AWS Cloud where you can launch AWS resources in a virtual network that you define. You have complete control over your virtual networking environment, including selection of your own IP address range, creation of subnets, and configuration of route tables and network gateways.

### What are the components of Amazon VPC

* A Virtual Private Cloud: A logically isolated virtual network in the AWS cloud. You define a VPC’s IP address space from ranges you select.
* Subnet: A segment of a VPC’s IP address range where you can place groups of isolated resources.
* Internet Gateway: The Amazon VPC side of a connection to the public Internet.
* NAT Gateway: A highly available, managed Network Address Translation (NAT) service for your resources in a private subnet to access the Internet.
* Virtual private gateway: The Amazon VPC side of a VPN connection.
* Peering Connection: A peering connection enables you to route traffic via private IP addresses between two peered VPCs.
* VPC Endpoints: Enables private connectivity to services hosted in AWS, from within your VPC without using an Internet Gateway, VPN, Network Address Translation (NAT) devices, or firewall proxies.
* Egress-only Internet Gateway: A stateful gateway to provide egress only access for **IPv6** traffic from the VPC to the Internet.

![VPC_Diagram](https://docs.aws.amazon.com/vpc/latest/userguide/images/default-vpc-diagram.png)

* You can have multiple VPC in a region (default up to 5).
* You can have 1 internet gateway per VPC.
* 1 Subnet = 1 AZ
* Security groups are Stateful, instead, Network ACLs are stateless.

### Default VPC

* Amazon provides a default VPC to immediately deploy instances.
* All Subnets in default VPC have a route out to the internet.

### VPC Peering

* You can peer one VPC to another VPC using private IP subnets.
* You can peer VPC's with others AWS accounts as well as with other VPC's in the same account.

### How to VPC Peering

* Overlapping CIDR Blocks is not supported: You can't connect two VPC's that have the same CIDR.
* Transitive Peering is not supported:

    You have a VPC peering connection between VPC A and VPC B (pcx-aaaabbbb), and between VPC A and VPC C (pcx-aaaacccc). There is no VPC peering connection between VPC B and VPC C. You cannot route packets directly from VPC B to VPC C through VPC A.

    ![transitive-peering](https://docs.aws.amazon.com/vpc/latest/peering/images/transitive-peering-diagram.png)

### Build Your Own Custome VPC

* [VPC and Subnet Sizing](https://docs.aws.amazon.com/vpc/latest/userguide/VPC_Subnets.html#vpc-subnet-basics) The first four IP addresses and the last IP address in each subnet CIDR block are not available for you to use, and cannot be assigned to an instance.

* For Nat Instances you have to disable the [Source/Destination Checks](https://docs.aws.amazon.com/vpc/latest/userguide/VPC_NAT_Instance.html#EIP_Disable_SrcDestCheck).
* Use [Nat Gateways](https://docs.aws.amazon.com/vpc/latest/userguide/vpc-nat-gateway.html#nat-gateway-basics) instead of Nat Instances

    ![nat-gateway](https://docs.aws.amazon.com/vpc/latest/userguide/images/nat-gateway-diagram.png)

### [Network Access Control Lists vs Security Groups](https://docs.aws.amazon.com/vpc/latest/userguide/VPC_Security.html)

![vpc&NACL](https://docs.aws.amazon.com/vpc/latest/userguide/images/security-diagram.png)

* NACL cannot be deployed in multiple VPCs.
* NACL cannot be attached to multiple subnets, only one at the time.
* Each subnet must be associated with a network ACL, if you don't, default NACL will be used.
* By default when you create one NACL, everything is denied.
* Rules are applied in numerical order (starting from the lowest), so when you should create the first rule having number 100 and add others on incremental of 100
* NACL are **stateless** (opposite of Security Groups)
* Remember to open [ephemaral ports](https://docs.aws.amazon.com/vpc/latest/userguide/vpc-network-acls.html#nacl-ephemeral-ports) on your outbound rules only.
* If you have to block specific IP addresses, use network ACL not Security Groups

### Custom VPC's and ELB's

* Design tip: Remember that ELB needs at least two public AZ's, so when designing your network, remember to create at least two public subnets in two AZ.

### [VPC Flow Logs](https://docs.aws.amazon.com/vpc/latest/userguide/flow-logs.html)

VPC Flow Logs is a feature that enables you to capture information about the IP traffic going to and from network interfaces in your VPC. Flow log data can be published to Amazon CloudWatch Logs and Amazon S3. After you've created a flow log, you can retrieve and view its data in the chosen destination.

### [VPC Enpoints](https://docs.aws.amazon.com/vpc/latest/userguide/vpc-endpoints.html)

A VPC endpoint enables you to privately connect your VPC to supported AWS services and VPC endpoint services powered by PrivateLink without requiring an internet gateway, NAT device, VPN connection, or AWS Direct Connect connection.