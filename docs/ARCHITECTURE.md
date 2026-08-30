# Architecture

How the three parts build on each other, and the vocabulary needed to defend them.

## Progression

| Part | Data plane | Control plane |
|---|---|---|
| P1 | none yet — two containers on a link | static |
| P2 | VXLAN, VNI 10 | none: flood-and-learn, static peers then multicast |
| P3 | VXLAN, VNI 10 | MP-BGP with the EVPN address family, via a route reflector |

The data plane does not change between P2 and P3. What changes is how a VTEP
learns which remote VTEP holds a given MAC address: by flooding and observing in
P2, by being told in P3.

## Terminology

The subject warns that any term it uses may be asked about at defence. Fill each
of these in as the part that introduces it is built.

- **Underlay** —
- **Overlay** —
- **VXLAN / VNI** —
- **VTEP** —
- **Flood-and-learn** —
- **MP-BGP (RFC 4760) / NLRI** —
- **EVPN address family (RFC 7432)** —
- **Route reflector** —
- **Route type 2** —
- **Route type 3** —
- **OSPF's role here** —
- **Why no MPLS** —

## Decisions

<!--
Record choices and their reasons as they are made: base images, addressing
scheme, AS numbering, where the route reflector lives.
-->
