# pihole + unbound using docker-compose
# it also works for synology

## What is this about

- pi-hole is basically a DNS setup for your local network which is blocking unwanted content (malware, ads etc). see https://pi-hole.net
- Unbound is a validating, recursive, caching DNS resolver. see https://www.nlnetlabs.nl/projects/unbound/about/

I wanted to run these on my home network, and for that, I used my Synology NAS and Docker.

To be more precise, I'm using Docker Compose with a docker-compose file generated from this project: https://github.com/markdumay/synology-pihole.

Unfortunately, that project is apparently unmaintained, so I made my own improvements, which I'm documenting here. The project includes a shell script used to generate a docker-compose.yaml file. I think that script is overkill for this task, so I prefer to show you my final file and comment on it to help you make changes for your setup.

## Network settings explained
Before diving into `docker-compose.yaml` file, tel me explain the network settings. 

WIP

## Unbound configuration file
WIP

## Usage
WIP

