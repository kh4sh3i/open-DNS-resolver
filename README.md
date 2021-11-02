# open DNS resolver
DNS Open resolvers or open DNS resolver are DNS servers responding to recursive queries for arbitrary domain names from anywhere on the Internet.



### DNS query types
* DNS Recursive query
* DNS Non-recursive query
* DNS Iterative query

DNS Open-resolvers can be abused for DDoS reflection attacks against third parties.


## Verification
```
$ dig +short jetamooz.com @x.x.x.x
```
note : Substitue x.x.x.x with the IP address of the DNS resolver (target).

if you get response then your target is vulnerable.
if you do not set response or get request time out then target is safe!


### online check target
* [zonecheck](https://zonecheck.org/openres.php)
* [openresolver](https://openresolver.com/)


## Solution
* Disable recursion or limit recursion to trusted clients in the DNS server's configuration.

* BIND: [Secure BIND Template](http://www.cymru.com/Documents/secure-bind-template.html)
```
Secure Bind by adding ACLs, and permitting it in named.conf options 

acl "trust" { localhost; 10.100.100.0/24; 2001:ffff:ffff:ffff::/64; };

options {
        ...
        allow-query { trust; };
        allow-query-cache { trust; };
        ...
}


Secure Unbound by adding access-control statements in unbound.conf server block

server:
        access-control: 0.0.0.0/0 refuse
        access-control: 10.100.100.0/24 allow
        access-control:2001:ffff:ffff:ffff::/64 allow
        ...
```
* Microsoft Windows: Disable Recursion on the DNS Server

### references
* [ncsc.gov.ie](https://www.ncsc.gov.ie/emailsfrom/DDoS/DNS/)
* [cloudflare.com/](https://www.cloudflare.com/learning/ddos/dns-amplification-ddos-attack/)
* [bsi.bund.de](https://www.bsi.bund.de/EN/Topics/IT-Crisis-Management/CERT-Bund/CERT-Reports/HOWTOs/DNS-Open-Resolver/DNS-Open-Resolver_node.html)
