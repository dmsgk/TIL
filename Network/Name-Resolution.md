# Name Resolution

## DNS(Domain Name System)

- A global and highly distributed network service that resolves strings of letters into IP address for you (도메인 이름을 ip주소로 바꿔준다.)

- Domain Name
  - The term we use for something that can be resolved by DNS

## Five primary types of DNS servers

1. Cashing name servers
2. Recursive name servers
3. Root name servers
4. TLD name servers
5. Authoritative name servers

- Cashing and recursive name servers
  - Purpose is to store known domain name lookups for a certain amount of time
- Recursive name servers
  - Perform full DNS resolution requests
- TTL(Time to live)
  - A value, in seconds, that can be configured by the owner of a domain name for how long a name server is allowed to cache an entry before it should discard it and perform a full resolution again
- Anycast
  - A  technique that's used to route traffic to different destinations depending on factors like location, congestion, or link health



## DNS and UDP

- DNS와 UDP의 차이점
  - UDP는 connectionless. 따라서 트래픽이 전반적으로 적게 든다. 
  - DNS 사용시 44패킷이 사용되는 것에 비해 UDP 사용  시  8패킷이 사용된다. 

## Resource Record Types

- A record
  - An A record is used to point a certain domain name at a certain IPv4 IP address
- AAAA - Quad A record
  - Quad A record is very similar to an A record except that it returns in IPv6 address instead of an IPv4 address. 
- CNAME record
  - A CNAME record is used to redirect traffic from one domain to another.
- MX record - mail exchange
  -  this resource record is used in order to deliver e-mail to the correct server.
- TXT record - text
  - be used only for associating some descriptive text with a domain name for human consumption. 

## Anatomy of a Domain Name

> `www.google.com`을 예시로 들어보자.
>
> \- `.com`부분은 TLD이다. 
>
> \- `google`부분은 domain이다. 
>
> \- `www`부분은 subdomain이다.
>
> \- 전체를 FQDN이라고 한다. 

- TLD(Top level domain) 
  - The last part of a domain name
- Domains
  - Used to demarcate where control moves from a TLD name server to an authoritative name server
- Subdomains
- FQDN(Fully qualified domain name)
  - When you combine all of these parts together, you have what's knownn as this

DNS can technically support up to 127 levels of domain in total for a single fully qualified domain name.



## DNS Zones

- DNS Zones are a hierarchical concept, allowing for easier control over multiple levels of a domain
- Zones are configured through what are known as zone files
  - Zone files
    - Simple configuration files that declare all resource records for a particular zone
    - Zone file has to contain SOA 
      - SOA(Start of authority)
        - Declares the zone and the name of the name server that is authoritative for it
      - NS records
        - Indicate other name servers that might also be responsible for this zone
    - Reverse lookup zone files
      - These let DNS resolvers ask for an IP and get the FQDN associated with it returned
    - Pointer resouce record(PTR)
      - Resolves an IP to a name