# Overview

Over the past three or so year I have slowly built up this homelab setup from mostly free hardware I have acquired from friends. This is the most recent rendition after I purchased two new switches I installed yesterday (May 18th 2025). As is the norm with a homelab setup this is always changing and I have big plans for when my friend decommissions 8 or so of his other servers and gifts them to me.

# Hardware 
## Switches
- Microtik CRS326-24S-2Q+RM (10G switch)
- Microtik CRS354-48P-4S-2Q (1G switch with PoE capabilities)
## Storage
- NetApp JBOD (Don't know too much about it as it was gifted to me by a friend)
- 6 Seagate 7E8 ST8000DM0055 8TB 7.2K SATA HDDs (RAIDZ2 29TB Usable)
- 2 Random 4TB drives (Mirrored)
## Servers

**NOTES**
- The server at the very bottom is not in use, referenced in the server list, or counted when referencing number of servers from the bottom.
- Some RAM configurations are weird and non-standard due to problematic ram sticks

### Poweredge R620 (Bottom Server) - PVE1
- CPU(s) 24 x Intel(R) Xeon(R) CPU E5-2620 v2 @ 2.10GHz (2 Sockets)
- 126GB of RAM
- Some random boot drive
- 2x Intel X520-SR2 Network Card 10Gb PCIe 2.0 x8 SFP+ NICs
- 2x 4 port 1G NICs (Sorry, I don't know the model number)
- Proxmox
### Poweredge R710 (Middle Server) - PVE2
- CPU(s) 24 x Intel(R) Xeon(R) CPU X5650 @ 2.67GHz (2 Sockets)
- 142GB of RAM
- Some random boot drive
- 1x Intel X520-SR2 Network Card 10Gb PCIe 2.0 x8 SFP+ NIC
- 1x 4 port 1G NICs (Sorry, I don't know the model number)
- Proxmox

### Poweredge R710 (Top Server) - PVE3
- CPU(s) 24 x Intel(R) Xeon(R) CPU X5650 @ 2.67GHz (2 Sockets)
- 126GB of RAM
- Some random boot drive
- 1x Intel X520-SR2 Network Card 10Gb PCIe 2.0 x8 SFP+ NIC
- 1x 4 port 1G NICs (Sorry, I don't know the model number)
- Proxmox

# VMs

**NOTES**
- All VMs (Other than truenas and OPNsense) run debian and are configured with a cloud-init template using either local storage or an NFS pool. If a server is using an NFS pool it is denoted with (nfs) next to the VM name
- All VM allocated CPUs or Memory are based on what I have running in them. As I add more to each docker node, for example, I expand the allocations as needed.

## PVE1
- OPNsense
	- 4CPUs
	- 8GB Memory
	- 1x 4 Port 1G NIC Passed through (WAN and 1G LAN connectivity)
	- 1x 10Gb NIC Passed through (Additional LAN connectivity)
- tailscale (nfs)
	- 2 CPUs
	- 2 GB Memory
- dns-1 (nfs)
	- 2 CPUs
	- 2 GB Memory
- docker-node-0 (nfs)
	- 2 CPUs
	- 2 GB Memory
- docker-node-1 (nfs)
	- 8 CPUs
	- 16 GB Memory
## PVE2
- dns-2 (nfs)
	- 2 CPUs
	- 2 GB Memory
- docker-node-2 (nfs)
	- 4 CPUs
	- 16 GB Memory
- docker-node-3 (nfs)
	- 2 CPUs
	- 8 GB Memory
## PVE3
- truenas
	- 4 CPUs
	- 64 GB Memory
	- HBA Card Passed through (JBOD is connected here)
- dns-3 (nfs)
	- 2 CPUs
	- 2 GB Memory
- docker-node-4 (nfs)
	- 2 CPUs
	- 2 GB Memory
- docker-node-5 (nfs)
	- 2 CPUs
	- 2 GB Memory

# Services

## PVE1
- OPNsense
- tailscale (nfs)
	- Tailscale exit node with LAN Access
- dns-1 (nfs)
	- Technitium
- docker-node-0 (nfs)
	- Portainer
	- Caddy
- docker-node-1 (nfs)
	- Authentik
	- Immich
	- Microbin
## PVE2
- dns-2 (nfs)
	- Technitium
- docker-node-2 (nfs)
	- Media stuff (Jellyfin)
- docker-node-3 (nfs)
	- Paperless
## PVE3
- truenas
- dns-3 (nfs)
	- Technitium
- docker-node-4 (nfs)
	- homepage
	- miniflux
- docker-node-5 (nfs)
	- staffup-bot (A discord bot)


# Other

I am still working on diagraming my homelab both physical hardware and applications.

Any comments, questions, or feedback is welcome.
