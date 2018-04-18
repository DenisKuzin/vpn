# vpn
IPsec IKEv2 strongSwan

# server
1) add ip address of server to inventory file ("vpn/production")
2) ssh-copy-id to that server, so ansible can execute remote commands
3) install ansible on you dev host/laptop
Ubuntu/Debian: apt-get install ansible
macos: brew install ansible
4) clone this repo and run "ansible-playbook --inventory-file production site.yml"

# client
docs and client for android: https://strongswan.org/

# Example of client config
```
config setup
    charondebug="ike 2, knl 2, cfg 2, net 2, esp 2, dmn 2,  mgr 2"
    uniqueids=no

conn vpn
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

# testing
tested on ubuntu 16.04 server/client and ios clients
