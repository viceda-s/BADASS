# Contributing to BADASS

This repository is graded on what an evaluator can observe on a running topology.
The workflow below exists to keep `main` in a state where any of the three parts
can be imported into GNS3 and defended without a scramble.

## Ground rules from the subject

These are not conventions we chose. Breaking one costs the deliverable.

- The mandatory parts live in folders named exactly **`P1`**, **`P2`** and **`P3`**
  at the root of the repository. Case matters.
- Every part contains its **portable GNS3 export** (`P1.gns3project`,
  `P2.gns3project`, `P3.gns3project`), produced with *File > Export portable
  project*, **including the base images**.
- Every part contains the **configuration files of each piece of equipment,
  with comments** explaining the setup.
- Every piece of equipment carries a **group member's login** in its name
  (`_login-1`, `host_login-1`, and so on). Naming must be consistent within a part.
- **No IP address is configured by default in a Docker image.** Addressing is
  applied in the topology, not baked into the build.
- The whole project runs **inside a virtual machine**.

## Branches

`main` is protected. Nothing lands on it directly.

Branch off `main`, one branch per issue:

```
feat/issue-<number>-<short-slug>     new capability
fix/issue-<number>-<short-slug>      something broken
docs/issue-<number>-<short-slug>     documentation only
chore/<short-slug>                   tooling, CI, repository plumbing
```

## Commits

[Conventional Commits](https://www.conventionalcommits.org/), scoped by part:

```
feat(p3): add route reflector configuration for the EVPN control plane
fix(p2): correct multicast group on the vxlan10 interface
docs(p1): comment the router image entrypoint
chore(ci): add the repository guard workflow
```

Write the commit body for the person defending this in three weeks. If you
worked around something non-obvious, say why in the body.

## Evidence

A pull request without evidence cannot be reviewed here. Reading a config is not
the same as watching the control plane converge, and the defence is conducted on
observed behaviour.

Attach the output that proves the change works. What counts depends on the part:

**P1 — images and GNS3**

```bash
docker build -t <image> P1/<dir>
docker images
# plus: the container visible and reachable from the GNS3 topology
```

**P2 — VXLAN**

```bash
ip -d link show vxlan10          # VNI 10, correct local/remote or group
bridge fdb show dev vxlan10      # learned MAC entries
ping <peer>                      # end-to-end through the overlay
tcpdump -i <underlay> udp port 4789
```

**P3 — BGP EVPN**

```bash
vtysh -c "show ip ospf neighbor"          # underlay is up
vtysh -c "show bgp l2vpn evpn summary"    # sessions to the route reflector
vtysh -c "show bgp l2vpn evpn"            # type-3 routes with no host running,
                                          # type-2 routes once a host boots
```

Screenshots are fine for anything only visible in the GNS3 GUI. Drag them into
the pull request body — screenshots are deliberately not committed to the
repository (see `.gitignore`), so the exports stay small.

## Before opening a pull request

- [ ] Rebase or merge `main` into your branch and resolve conflicts.
- [ ] Re-export the `.gns3project` if the topology changed, and confirm the
      export still imports cleanly.
- [ ] Confirm no file exceeds 90 MB. The `Repository guard` workflow enforces
      this because GitHub refuses to accept files above 100 MB.
- [ ] Comment any configuration you added.
- [ ] Check that no credentials, keys, VM snapshots, or personal state slipped in.

## Review

Each part has an owner in [`.github/CODEOWNERS`](.github/CODEOWNERS). A pull
request touching a part requests that owner's review automatically, and the
ruleset on `main` requires it. One approval, all review threads resolved, then
merge.

If you have to change someone else's part, say so in the pull request and name
them. The point is that nobody gets surprised at the defence by configuration
they have never seen.

## Terminology

The subject warns that you may be asked to explain any term it uses. If a pull
request introduces a concept the group has not defined yet — VTEP, VNI, route
reflector, route type 2 versus type 3, the split between underlay and overlay —
document it in `docs/` as part of that pull request, while it is fresh.
