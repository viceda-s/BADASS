# P1 — GNS3 configuration with Docker

Two Docker images, built here and used by every later part, wired into a
two-machine topology in GNS3.

## Required contents of this folder

- [ ] `P1.gns3project` — portable export, **base images included**
- [ ] The host image build context (Dockerfile + entrypoint)
- [ ] The router image build context (Dockerfile + entrypoint + daemon configs)
- [ ] Commented configuration for each piece of equipment

## The images

**Host** — a system of your choice containing at least busybox or an equivalent.
Alpine is a good fit.

**Router** — a system of your choice with:

- [ ] a packet-routing manager (`zebra` / `quagga`, or FRR)
- [ ] **BGPD** active and configured
- [ ] **OSPFD** active and configured
- [ ] an **IS-IS** routing engine service
- [ ] busybox or an equivalent

> **No IP address may be configured by default in either image.** Addressing is
> applied in the topology.

## Naming

Equipment names must carry a group member's login, consistently across the part
— for example `_login-1_host` and `_login-2`.

## Verification

<!--
Record the commands and their output here as the part is built:
  docker build ...
  docker images
  connection to each machine from GNS3
-->

## Notes

<!-- Design decisions, base image choice, anything worth explaining at defence. -->
