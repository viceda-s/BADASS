# P2 — Discovering a VXLAN

A layer-2 overlay built on the P1 images, first with statically configured
remote peers, then with dynamic multicast.

## Required contents of this folder

- [ ] `P2.gns3project` — portable export, **base images included**
- [ ] Commented configuration for each piece of equipment

## Requirements

- [ ] VXLAN with **ID 10**, interface named `vxlan10`
- [ ] Bridge named `br0`
- [ ] Ethernet interfaces addressed as you see fit
- [ ] **Static mode** working: traffic passes between the two hosts
- [ ] **Dynamic multicast mode** working, using a group (for example `239.1.1.1`)
- [ ] MAC address table observable on both routers

## Addressing plan

<!-- Underlay and overlay addressing, per interface. -->

## Verification

<!--
  ip -d link show vxlan10
  bridge fdb show dev vxlan10
  ping between the two hosts
  tcpdump of the encapsulated traffic (UDP 4789)
-->

## Notes

<!-- Static versus multicast: what changed in the configuration, and why. -->
