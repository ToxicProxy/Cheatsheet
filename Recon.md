# Zero Packet Recon

* ***ASNUM Enumeration***

```zsh
curl -s http://download.maxmind.com/download/geoip/database/asnum/GeoIPASNum2.zip | gunzip | cut -d"," -f3 | sed 's/"//g' | sort -u | grep -i google
```
* ***IPSPACE Enumeration***

```zsh
whois -h whois.radb.net -- '-i origin AS35995' | grep -Eo "([0-9.]+){4}/[0-9]+"
```
# Subdomain Recon

* ***Certificate Transparency Logs***

```zsh
curl https://certspotter.com/api/v0/certs\?domain\=example.com | jq '.[].dns_names[]' | sed 's/\"//g' | sed 's/\*\.//g' | uniq
```
  **~** Rolling the above output over Nmap  
```zsh
curl https://certspotter.com/api/v0/certs\?domain\=example.com | jq '.[].dns_names[]' | sed 's/\"//g' | sed 's/\*\.//g' | uniq | dig +short -f - | uniq | grep ".example.com" | nmap -T5 -Pn -sS -i - -p 80,443,21,22,8008,8080,8081,8443 --open -n -oG -
```
```
#!/bin/bash
#Takes a list of domains and runs the host command on them, sorting them by IP.
cat $1| while read line; do host "$line"; done |grep -E "\b([0-9]{1,3}\.){3}[0-9]{1,3}\b"|sort -n -t " " -k 4
```

**DNS Trails**

```
curl hxxps://app.securitytrails.com/api/whois/list/organization/Uber%20Technologies%2C%20Inc.?page=1 | jq .
```
# Android APK Analysis
https://android.fallible.co/
https://apkscan.nviso.be/
