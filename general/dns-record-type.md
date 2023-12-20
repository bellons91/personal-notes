---
tags: dns
---

# DNS Record types

[[DNS]] record types are used to map domain names to IP addresses and other information. Here are some of the main DNS record types and their descriptions:

## A

Also known as an address record, it maps a domain name to an [[IPv4]] address. This is the most common type of DNS record and is used to point a domain name to an IP address. For example, an A record for the domain name example.com could be example.com. IN A 192.0.2.1.

## AAAA

Also known as an IPv6 address record, it maps a domain name to an [[IPv6]] address. This record is used to point a domain name to an IPv6 address. For example, an AAAA record for the domain name example.com could be example.com. IN AAAA 2001:db8::1.

## ALIAS

An **ALIAS record** is a virtual record type that provides CNAME-like behavior on [[apex domains]]. It maps a domain name to a hostname instead of an IP address. For example, if your domain is example.com and you want it to point to a hostname like myapp.herokuapp.com, you can't use a CNAME record, but you can use an ALIAS record. The ALIAS record will automatically resolve your domain to one or more A records at resolution time, and resolvers see your domain as if it had A records.

## CAA

Also known as a certification authority authorization record, it specifies which [[certificate authorities]] are authorized to issue certificates for a domain name. This record is used to prevent unauthorized certificate issuance and improve security. For example, a CAA record for the domain name example.com could be example.com. IN CAA 0 issue "ca.example.com".

## CNAME

Also known as a canonical name record, it maps an alias name to a true domain name. This record is used to create an alias for a domain name. For example, a CNAME record for the domain name *<www.example.com>* could be *<www.example.com>*. IN CNAME example.com.

## DNSKEY

Also known as a DNS security key record, it stores a public key used to verify [[DNSSEC signatures]]. This record is used to authenticate DNS data and prevent [[DNS spoofing]]. For example, a DNSKEY record for the domain name example.com could be example.com. IN DNSKEY 256 3 8 AwEAAc....

## DS

Also known as a delegation signer record, it stores a hash of a DNSKEY record in the parent zone. This record is used to authenticate child zones and prevent [[DNS cache poisoning]].

## MX

Also known as a mail exchange record, it maps a domain name to a list of mail exchange servers. This record is used to specify the mail server responsible for accepting email messages on behalf of a domain name. For example, an MX record for the domain name example.com could be example.com. IN MX 10 mail.example.com.

## NAPTR

Also known as a naming authority pointer record, it maps a domain name to a regular expression that can be used to transform the domain name into another domain name. This record is used to support advanced services such as ENUM.

## NS

Also known as a name server record, it maps a domain name to a list of name servers. This record is used to delegate a domain name to a set of name servers. For example, an NS record for the domain name example.com could be example.com. IN NS ns1.example.com.

## PTR

Also known as a pointer record, it maps an IP address to a domain name. This record is used to perform a reverse [[DNS lookup]]. For example, a PTR record for the IP address 192.0.2.1 could be 1.2.0.192.in-addr.arpa. IN PTR example.com.

## SOA

Also known as a start of authority record, it contains administrative information about a [[DNS zone]]. This record is used to specify the primary name server for a DNS zone and other administrative information. For example, an SOA record for the domain name example.com could be example.com. IN SOA ns1.example.com. admin.example.com. 2019020101 3600 1800 604800 86400.

## SRV

Also known as a service record, it maps a domain name to the hostname and port number of servers for a specific service. This record is used to locate services such as SIP and XMPP1. For example, an SRV record for the domain name _sip._tcp.example.com could be _sip._tcp.example.com. IN SRV 10 60 5060 sipserver.example.com.

## SSHFP

 Also known as a Secure Shell fingerprint record, it maps a domain name to the fingerprint of an [[SSH]] public key. This record is used to authenticate SSH connections.

## TLSA

Also known as a [[tls]] authentication record, it maps a domain name to the certificate or public key of a server. This record is used to authenticate the server’s identity and establish a secure connection. For example, a TLSA record for the domain name _443._tcp.example.com could be _443._tcp.example.com. IN TLSA 3 1 1 abcd....

## TXT

Also known as a text record, it contains text information about a domain name. This record is used to store arbitrary text data in a DNS record. For example, a TXT record for the domain name example.com could be example.com. IN TXT "v=spf1 a mx ip4:192.0.2.0/24 ~all".
