# Information Gathering | Reconnaissance | OSINT
# Passive Reconnaissance
### DNS Records
- dig dev.website.io
- whois 10.10.10.10
- nslookup domain.com
- [Netcraft](https://searchdns.netcraft.com)
- subdomain enum with [dnscan](https://github.com/rbsec/dnscan), [dnsrecon](https://github.com/darkoperator/dnsrecon)
- Zone transfer `dig @nameserver axfr domain.com`

### Tools
- [Shodan](https://www.shodan.io)
- Public S3 buckets/Blobs - []()

# Active Reconnaissance
- whatweb ip
-

### Email
- Check email protections [./spoofcheck.py](https://github.com/BishopFox/spoofcheck) org.com

### Web OSINT
Google dorks [GHDB](https://www.exploit-db.com/google-hacking-database)
