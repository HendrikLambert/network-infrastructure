# Network Infrastructure

This project demonstrates a setup with a VyOS router that peers using BGP with two Talos nodes. It uses the Calico CNI and hosts a Traefik container on the VyOS router as an edge loadbalancer.

This setup aims to provide a PoC to eliminate the extra hop, often used in Kubernetes and allows for terminating SSL traffic for services outside of the Kubernetes cluster.

> [!WARNING]
> This router configuration is NOT hardened and currently routes all traffic without firewall rules.

## Prerequisites

```bash
vagrant plugin install vagrant-vyos
vagrant box add vyos/current
```

## Setup

1. Modify the IP addresses in `Vagrantfile` to match your network
2. Start the VyOS router:
   ```bash
   vagrant up
   ```
