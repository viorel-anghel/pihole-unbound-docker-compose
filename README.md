# pihole + unbound using docker-compose
# it also works for synology

## What is this about

- pi-hole is basically a DNS server for your local network which is blocking unwanted content (malware, ads etc). see https://pi-hole.net
- Unbound is a validating, recursive, caching DNS resolver. To help increase online privacy, Unbound supports DNS-over-TLS and DNS-over-HTTPS which allows clients to encrypt their communication. see https://www.nlnetlabs.nl/projects/unbound/about/

I wanted to run these on my home network, and for that, I used my Synology NAS and Docker. To be more precise, I'm using Docker Compose with a docker-compose file generated from this project: https://github.com/markdumay/synology-pihole.

Unfortunately, that project is apparently unmaintained, so I made my own improvements, which I'm documenting here. The project includes a shell script used to generate a docker-compose.yaml file. I think that script is overkill for this task, so I prefer to show you my final file and comment on it to help you make changes for your setup.


## Network settings explained

```
  
 +-----------+
 |           |  dns    +---------+
 |  home     | ------> | pi-hole |       +-------------+
 |  network  | ------> |  DNS    | ----> | unbound DNS |
 |  clients  | ------> |         |       +-------------+
 |           | queries +---------+
 +-----------+

```

Before diving into `docker-compose.yaml` file, let me explain the network settings. 

In Docker, `macvlan` is a special network driver that allows you to assign containers their own MAC and IP addresses, directly from the host’s physical network. Essentially, the container becomes visible on the network as a completely separate device—just like another computer.

This line `ip_range: 192.168.0.16/30  # small subnet for containers` in docker-compose is defining a very small sub-network inside my home network which is 192.168.0.0/24. Only two IP addresses can be used in a network defined with `/30` and in our case they will be 

- 192.168.0.18 for the pihole container and 
- 192.168.0.17 for the unbound container.

## Unbound configuration file

The unbound daemon will need a configuration file. In `unbound.conf` the only important thing is the line `access-control: 192.168.0.18 allow` with the IP from the pihole container which will access the unbound DNS server.

You'll need to copy this file at the location defined in docker-compose, see the line `- /root/pihole-unbound/etc-unbound/:/etc/unbound/`.

## Usage

Decide a location where to run the whole thing and copy and edit the docker-compose.yaml there. In my case, I'm using `/root/pihole-unbound/'. Use the `docker compose up -d` command to start the containers.

---
WIP
 

