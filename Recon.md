# IP-Space/ASNUM Passive Recon


# Subdomain Recon

* ***Certificate Transparency Logs***

```zsh
curl https://certspotter.com/api/v0/certs\?domain\=example.com | jq '.[].dns_names[]' | sed 's/\"//g' | sed 's/\*\.//g' | uniq
```

```zsh
curl https://certspotter.com/api/v0/certs\?domain\=example.com | jq '.[].dns_names[]' | sed 's/\"//g' | sed 's/\*\.//g' | uniq | dig +short -f - | uniq | grep ".example.com" | nmap -T5 -Pn -sS -i - -p 80,443,21,22,8008,8080,8081,8443 --open -n -oG -
```
