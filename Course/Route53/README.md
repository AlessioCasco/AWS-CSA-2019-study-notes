# CHAPTER 5 | Route53

## DNS

_You won't be questioned in the exam about the next sections (up to ALIAS record).
It's just for your knowledge and very good for better understanding the course._

### [What's DNS](https://www.cloudflare.com/learning/dns/what-is-dns/)

The Domain Name Systems (DNS) is the phonebook of the Internet. Humans access information online through domain names, like nytimes.com or espn.com. Web browsers interact through Internet Protocol (IP) addresses. DNS translates domain names to IP addresses so browsers can load Internet resources.

### [IPv4 vs IPv6](https://www.guru99.com/difference-ipv4-vs-ipv6.html)

* IPv4 is a 32-Bit IP Address.
* IPv6 is 128 Bit IP Address and was created to fulfil the need for more Internet addresses.

### [Top Level Domains:](https://en.wikipedia.org/wiki/Top-level_domain)

A top-level domain is one of the domains at the highest level in the hierarchical Domain Name System of the Internet (```.com``` ```.net``` ```.org``` as an example).

In the case of ```.co.uk```, ```.co``` is the second level domain and ```.uk``` is the top level domain

### [SOA Record](https://en.wikipedia.org/wiki/SOA_record)

A Start of Authority record (abbreviated as SOA record) is a type of resource record in the Domain Name System (DNS) containing administrative information about the zone, especially regarding zone transfers.

Example of a SOA record

```bash
$ dig SOA +multiline google.com

[...]
;; ANSWER SECTION:
google.com.        55 IN SOA ns1.google.com. dns-admin.google.com. (
                238640061  ; serial
                900        ; refresh (15 minutes)
                900        ; retry (15 minutes)
                1800       ; expire (30 minutes)
                60         ; minimum (1 minute)
                )
[...]
```

### [NS Record](https://www.cloudflare.com/learning/dns/dns-records/dns-ns-record/)

NS stands for 'name server' and this record indicates which DNS server is authoritative for that domain (which server contains the actual DNS records)

```bash
$ dig NS google.com

[...]

;; ANSWER SECTION:
google.com.        2073    IN    NS    ns4.google.com.
google.com.        2073    IN    NS    ns1.google.com.
google.com.        2073    IN    NS    ns2.google.com.
google.com.        2073    IN    NS    ns3.google.com.

[...]
```

### [A Record](https://www.cloudflare.com/learning/dns/dns-records/dns-a-record/)

The ‘A’ stands for ‘address’ and this is the most fundamental type of DNS record, it indicates the IP address of a given domain

```bash
$ dig A google.com

[...]

;; ANSWER SECTION:
google.com.        62    IN    A    216.58.201.14

[...]
```

### [TTL, Time to Live](https://en.wikipedia.org/wiki/Time_to_live#DNS_records)

When a caching (recursive) nameserver queries the authoritative nameserver for a resource record, it will cache that record for the time (in seconds) specified by the TTL.

### [CNAME Record](https://support.dnsimple.com/articles/cname-record/)

CNAME records can be used to alias one name to another. CNAME stands for Canonical Name.

A common example is when you have both example.com and www.example.com pointing to the same application and hosted by the same server.

```bash
$ dig www.dnsimple.com

[...]

;; ANSWER SECTION:
www.dnsimple.com.    3595    IN    CNAME    dnsimple.com.
dnsimple.com.        55    IN    A    104.245.210.170

[...]
```

CNAME can't be used on the root domain. (This is a contractual limitation imposed by the RFC 1912 and RFC 2181, not a technical one.)

### [ALIAS record](https://support.dnsimple.com/articles/alias-record/)

An ALIAS record is a virtual record type we created to provide CNAME-like behaviour on apex domains.
For example, if your domain is example.com and you want it to point to a hostname like myapp.herokuapp.com, you can’t use a CNAME record, but you can use an ALIAS record. The ALIAS record will automatically resolve your domain to one or more A records at resolution time, and resolvers see your domain simply as if it had A records.

In AWS you have to use ALIAS records to point your root domain to other DNS records such as your ELB.

## DNS IN AWS

### [Routing policies available in AWS](https://docs.aws.amazon.com/Route53/latest/DeveloperGuide/routing-policy.html)

* Simple routing policy: Use for a single resource that performs a given function for your domain. You can have 1 record with multiple addresses.
* Weighted routing policy: Use to route traffic to multiple resources in proportions that you specify. You can send 40% of the traffic on one IP and 60% to another IP.
* Latency routing policy: Use when you have resources in multiple AWS Regions and you want to route traffic to the region that provides the best latency.
* Failover routing policy: Use when you want to configure active-passive failover.
You need to create a health check before.
* Geolocation routing policy: Use when you want to route traffic based on the location of your users.
* Multivalue answer routing policy: Use when you want Route 53 to respond to DNS queries with up to eight healthy records selected at random.
* Geoproximity routing policy: Use when you want to route traffic based on the location of your resources and, optionally, shift traffic from resources in one location to resources in another.