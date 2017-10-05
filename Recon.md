# Zero Packet Recon

* ******ASNUM Enumeration******

```zsh
curl -s http://download.maxmind.com/download/geoip/database/asnum/GeoIPASNum2.zip | gunzip | cut -d"," -f3 | sed 's/"//g' | sort -u | grep -i google
```
* ******IPSPACE Enumeration******

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
