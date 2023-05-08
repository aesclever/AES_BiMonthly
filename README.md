# AES News Feed

By <a href="https://new.aesclever.com"><span style="color:green">Applied Expert Systems LLC</span></a>

The most recent DNS attack vectors include DNS hijacking, DNS spoofing, DNS cache poisoning, DNS tunneling, and DNS amplification attacks.  As malicious attacks evolved to more sophisticated methods of exploitation, the fundamental issue remains; it's a wack-a-mole reality.  A mole problem requires fortification, detection, locating, and bringing the mole to face justice.

* `DNS hijacking` is a type of cyber attack that redirects a user from a legitimate website to a malicious one. It is done by malicious actors who are looking to steal information or spread malware. The targets of DNS hijacking are typically users who are unaware of the attack and are not using secure protocols to access the web. 

* `DNS spoofing`, also known as DNS cache poisoning, is a type of cyber attack in which an attacker corrupts a Domain Name System (DNS) server’s cache so that it resolves a domain name to the wrong IP address. This can allow the attacker to redirect traffic intended for a legitimate website to a malicious one, such as a phishing website that steals user credentials.
DNS spoofing attacks have been responsible for some major security breaches, such as the 2012 LinkedIn data breach that affected over 150 million users. In this case, attackers used a DNS spoofing attack to redirect users from the legitimate LinkedIn website to a fake one that asked them to enter their LinkedIn username and password.

* `DNS cache poisoning` is a cyber attack technique that involves corrupting the Domain Name System (DNS) cache of a server, allowing malicious actors to redirect users to malicious websites. Recent cases of DNS cache poisoning have made headlines, such as the attack on the City of Johannesburg's website in 2019, which resulted in the city's website being redirected to a phishing page, and the attack on the US Department of Defense in 2020, which resulted in malicious actors gaining access to sensitive information. 

* `DNS tunneling` is a technique used by attackers to bypass security policies and send malicious traffic through DNS servers. This technique has been used in a variety of attacks, including DDoS attacks, malware propagation, and data exfiltration. DNS tunneling can be difficult to detect, as it uses valid DNS requests and responses to encode and decode data. However, there are a few indicators that can be used to detect DNS tunneling activity, such as unusual DNS query types or high volumes of DNS queries. 

* `DNS amplification` attacks are often detected by looking at DNS server logs. These logs will show a large number of requests coming from a small number of sources. This is a tell-tale sign of an amplification attack. 


The all encompassing pattern indicators for these attacks are <sup><strong>unusual DNS query types, high volumnes of DNS queries from the same IP or group of IP addresses</strong></sup>.  

<blink>The solution for detecting malicious actors can be provided by <a href="https://new.aesclever.com/solutions/">Applied Expert Systems LLC</a></blink>
We have a suite of enterprise network monitoring tools.  Sign up for a free trial.  Trial can also be extended upon valid request.

<br />

<iframe id="inlineFrame" title="Free trial form" width="100%" height="300" src="https://new.aesclever.com/free-trial/" >Sign up for Free Trial</iframe>


<br />
<hr>

__Additionally, below are some quick references to network tools to preleminarily determine the state of your network security.__


<br />

## How to Verify DNSSEC Using Dig Command

The `DNSSEC` is an acronym for <a href="https://www.google.com/url?sa=t&rct=j&q=&esrc=s&source=web&cd=&cad=rja&uact=8&ved=2ahUKEwiYuP6SreT-AhW4IDQIHYNMASgQFnoECA4QAQ&url=https%3A%2F%2Fwww.icann.org%2Fresources%2Fpages%2Fdnssec-what-is-it-why-important-2019-03-05-en&usg=AOvVaw33EyAgwgmXo-TledVfkt1m"><span style="color:blue">Domain Name System Security Extensions</span></a>.  
Using the network utility `dig`, we can verify the authentication of DNS data and DNS integrity. 

Requirements: Linux or WSL - Windows Linux Subsystem



<br />

1. **DNSSEC verification commands**: 

`dig +sigchase +trusted-key={key} `<span style="color:green">{YOUR-DOMAIN-NAME}</span> `A | grep -i validation`


_Successful sample_:


<span style="color:grey">markn@LAPTOP-G3V91M69:~$</span> `dig . DNSKEY | grep -Ev '^($|;)' > ./keys`

<span style="color:grey">markn@LAPTOP-G3V91M69:~$</span> `dig +sigchase +trusted-key=./keys www.ca.gov A | grep -i validation`

```javascript
;; WE HAVE MATERIAL, WE NOW DO VALIDATION
;; WE HAVE MATERIAL, WE NOW DO VALIDATION
;; WE HAVE MATERIAL, WE NOW DO VALIDATION
;; Ok this DNSKEY is a Trusted Key, DNSSEC validation is ok: SUCCESS
```

_Failure sample_:

<span style="color:grey">markn@LAPTOP-G3V91M69:~$</span> `dig +sigchase +trusted-key=./keys www.yahoo.com A | grep -i validation`

```javascript
;; RRSIG is missing for continue validation: FAILED
```


<br />

**Altenately, command `dig` used in combination with `+dnssec` option**

<span style="color:grey">markn@LAPTOP-G3V91M69:~$</span> `dig www.ca.gov +dnssec +multi`

```javascript
; <<>> DiG 9.11.3-1ubuntu1.12-Ubuntu <<>> www.ca.gov +dnssec +multi
;; global options: +cmd
;; Got answer:
;; ->>HEADER<<- opcode: QUERY, status: NOERROR, id: 50040
;; flags: qr rd ra; QUERY: 1, ANSWER: 5, AUTHORITY: 0, ADDITIONAL: 1

;; OPT PSEUDOSECTION:
; EDNS: version: 0, flags: do; udp: 512
;; QUESTION SECTION:
;www.ca.gov.            IN A

;; ANSWER SECTION:
www.ca.gov.             103 IN CNAME www.ca.gov.edgekey.net.
www.ca.gov.             103 IN RRSIG CNAME 13 3 300 (
                                20230509000229 20230506220229 34505 ca.gov.
                                xEfCxLyLfH76HX7QF9N6JThbNb6BHlKzVnNjEkhfBHPi
                                Rxrk4//naE6IP4tALZ5es4J4jpBBtubpzQTA8dAn3w== )
www.ca.gov.edgekey.net. 5700 IN CNAME e65017.dscb.akamaiedge.net.
e65017.dscb.akamaiedge.net. 20 IN A 69.192.139.236
e65017.dscb.akamaiedge.net. 20 IN A 69.192.139.212

;; Query time: 18 msec
;; SERVER: 75.75.75.75#53(75.75.75.75)
;; WHEN: Sun May 07 16:05:46 PDT 2023
;; MSG SIZE  rcvd: 246

```

Note: <sub>  <span style="color:grey">All is good if the status says `NOERROR`</span></sub>

<hr>
<br />

2. **Display the DNSSEC chain of trust with dig command**:

`dig DS <span style="color:green">{YOUR-DOMAIN-NAME}</span> +trace`


e.g.

markn@LAPTOP-G3V91M69:~$ `dig DS www.ca.gov +trace`

```javascript
; <<>> DiG 9.11.3-1ubuntu1.12-Ubuntu <<>> DS www.ca.gov +trace
;; global options: +cmd
.                       504000  IN      NS      j.root-servers.net.
.                       504000  IN      NS      k.root-servers.net.
.                       504000  IN      NS      l.root-servers.net.
.                       504000  IN      NS      m.root-servers.net.
.                       504000  IN      NS      a.root-servers.net.
.                       504000  IN      NS      b.root-servers.net.
.                       504000  IN      NS      c.root-servers.net.
.                       504000  IN      NS      d.root-servers.net.
.                       504000  IN      NS      e.root-servers.net.
.                       504000  IN      NS      f.root-servers.net.
.                       504000  IN      NS      g.root-servers.net.
.                       504000  IN      NS      h.root-servers.net.
.                       504000  IN      NS      i.root-servers.net.
.                       504000  IN      RRSIG   NS 8 0 518400 20230520050000 20230507040000 60955 . L8eO+po6sEU//i1/fOWkNtDl5kDiXWJui48Bqgc4DMYBAFAvX0VLmrt8 POlum54jig462w1k4HtjW5FFgAq2YnoZoYGZo3elmzOVWTiCO3cp7grI quTb/HP8kTC8K17krBFMCy941/3qJVWh3Q1rDKbhyhsCkwMVyDGwoIdh z4NPJYiMBWXix0q9w8N9QovK92MBnL/IND0p6A/mveP9yZ9JA0T+Uo53 0EVtgMl7x9WnVhw1NZkmz4MYwpJ2B/2MTUpD/OEZjSXpG5uCyVpgO2nz byhwCj2jJ+2AnHOsvNU5I3w1b/kJd/QJJj4QVObeSzYjX3wNY2hcudyz R80Jdw==
;; Received 1097 bytes from 75.75.75.75#53(75.75.75.75) in 15 ms

gov.                    172800  IN      NS      a.gov-servers.net.
gov.                    172800  IN      NS      b.gov-servers.net.
gov.                    172800  IN      NS      c.gov-servers.net.
gov.                    172800  IN      NS      d.gov-servers.net.
gov.                    86400   IN      DS      7698 8 2 6BC949E638442EAD0BDAF0935763C8D003760384FF15EBBD5CE86BB5 559561F0
gov.                    86400   IN      RRSIG   DS 8 1 86400 20230520170000 20230507160000 60955 . Cn7UhmKhLWFOvTayE3hNuI5QShHs3cBFft+Hwmud4yEWcIS6LNhnjzQg xKVr93FElb1ZYBnIxS7whE71Yv5vgZFA85HSVsvuc9yOEhN7Kq2u+MhK pv8pJYrdk5KYoKk+5v/SyveYf2tffGYwZA0nff+++LR+p+Mu8MJ52TK6 s+9RvZUsSxq2BvooVlQLQlSQaPcJEJCzpg/i3ILM9KblBl8RGe74f/c4 dHG51r6wFSXTJeJEKios8iriWJ+4jxGZpJXOhQ5rcdAoQu45OPazQir4 EH1altl5mUakgiFxQsW40rwfOcAmgp1yc3SGAdnbB1g+blU2AjoGFeJy rQW9cw==
;; Received 629 bytes from 2001:500:2d::d#53(d.root-servers.net) in 16 ms

ca.gov.                 86400   IN      NS      chase.ns.cloudflare.com.
ca.gov.                 86400   IN      NS      asa.ns.cloudflare.com.
ca.gov.                 3600    IN      DS      2371 13 2 27B709BA6CE7E22250EE3210F4030F0D81D3AABA7B70AD2C7546EB0B EBDBB69E
ca.gov.                 3600    IN      RRSIG   DS 8 2 3600 20230513074121 20230506074121 50011 gov. k5hRNbfDuK+MP8CrVSA/GebS83NzgFX25D2G/SWrTvCQuhy2SEzxoSn7 CnO2xSqZvKnVwRGkZLVpKUvnCgo2mTCg38/IHJIKYYR6p/MH/zEO48Id 6lsDTd5g84j3j6JbM9VkZTHP81OlnoLajkbhS2C7gL2zPd7f2Q0h7GCF V0w/QAKm94RysOfZ/Vcib/+AUAdmG9/1WqFe3okvxG93rw==
;; Received 337 bytes from 69.36.153.30#53(c.gov-servers.net) in 21 ms

www.ca.gov.             300     IN      CNAME   www.ca.gov.edgekey.net.
www.ca.gov.             300     IN      RRSIG   CNAME 13 3 300 20230508233634 20230506213634 34505 ca.gov. ncFjjCR9pyThbIx35bhgXgvYYa8895CZiEpjVc2hvt+9/ZLQu5q/tpkT RbAlHu/nLdz1gM6blQo+TyNv7Qc3Iw==
;; Received 177 bytes from 2a06:98c1:50::ac40:20f6#53(asa.ns.cloudflare.com) in 21 ms

```


Note: <sub><span style="color:grey">The `RRSIG RR` specifies a validity interval for the signature and uses the Algorithm, the Signer's Name, and the Key Tag to identify the DNSKEY RR containing the public key that a validator can use to verify the signature.</span></sub>


<br />
<hr>
Copyright&copy; 2023 Applied Expert Systems LLC All Rights Reserved
