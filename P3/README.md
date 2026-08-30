# P3 — Discovering BGP with EVPN

The same VXLAN, with MAC learning moved into the control plane. A small data
centre: leaves acting as VTEPs, a route reflector, and OSPF underneath.

## Required contents of this folder

- [ ] `P3.gns3project` — portable export, **base images included**
- [ ] Commented configuration for each piece of equipment

## Requirements

- [ ] BGP EVPN (RFC 7432), **without MPLS**
- [ ] **VXLAN ID 10**, carried over from P2
- [ ] **OSPF** as the underlay — required, to simplify evaluation
- [ ] One **route reflector**; leaves (VTEPs) configured with dynamic relationships
- [ ] **Type-3** routes present from configuration alone, with no host running
- [ ] **Type-2** routes appearing automatically as hosts come up, with
      **no IP address assigned** to them
- [ ] End-to-end reachability between hosts through the VTEPs

## Topology

<!-- Roles, loopbacks, AS numbers, which leaf peers with the reflector. -->

## Verification

<!--
  vtysh -c "show ip ospf neighbor"
  vtysh -c "show bgp l2vpn evpn summary"
  vtysh -c "show bgp l2vpn evpn"        before and after a host boots
  ping across the overlay, with a capture showing ICMP inside VXLAN 10
-->

## Notes

<!--
Worth writing down for the defence: what a VTEP is, what the VNI identifies,
why a route reflector replaces a full mesh, and what distinguishes a type-2
route from a type-3 route.
-->
