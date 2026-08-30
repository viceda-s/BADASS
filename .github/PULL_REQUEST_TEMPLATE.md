## What

<!-- Briefly describe the change. -->

## Why

<!-- The subject requirement or problem being addressed. -->

## Evidence

<!--
This project is defended on observed behaviour, not on code that looks right.
Paste the actual output or drag in the capture. Pick what applies:

  P1  docker build output, `docker images`, container reachable from GNS3
  P2  `ip -d link show vxlan10`, `bridge fdb show`, ping between hosts, tcpdump of the VXLAN
  P3  `show ip ospf neighbor`, `show bgp l2vpn evpn summary`,
      type-3 routes with no host up, type-2 routes appearing once a host boots
-->

```
```

## Scope

- Part: `P1` / `P2` / `P3` / `docs` / `ci`
- Owner consulted: <!-- @handle, if this touches another member's part -->

## Issue

Closes #<!-- issue-number -->

## Checklist

- [ ] Commit messages follow [Conventional Commits](https://www.conventionalcommits.org/).
- [ ] Branch is up to date with `main`, or conflicts are resolved.
- [ ] Configuration files carry comments explaining the setup of each piece of equipment.
- [ ] Equipment names carry the group login, and folder names match the subject exactly (`P1`, `P2`, `P3`).
- [ ] No IP address is baked into a Docker image.
- [ ] The `.gns3project` export is current if the topology changed.
- [ ] No credentials, keys, VM snapshots, or personal state included.
