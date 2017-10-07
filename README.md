# vpn
IPsec IKEv2 strongSwan

# Example of client config
```
config setup
    charondebug="ike 2, knl 2, cfg 2, net 2, esp 2, dmn 2,  mgr 2"
    uniqueids=no

conn vultr
    keyexchange=ikev2
    ike=aes256-sha384-modp2048!
    esp=aes256-sha384-modp2048!
    dpdaction=clear
    dpddelay=300s
    left={{ local_ip_address }}
    leftid={{ client_id }}
    leftcert={{ cert_file_path }}
    leftsourceip=%config
    rightsubnet=0.0.0.0/0
    right={{ server_ip }}
    rightid={{ server_id }}
    rightsendcert=always
    auto=start
    forceencaps=yes
    fragmentation=yes
```
