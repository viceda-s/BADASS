# Bgp At Doors of Autonomous Systems is Simple (BADASS)

Simulating and configuring networks in **GNS3** with **Docker** images, from a
two-machine topology up to a small data centre running **BGP EVPN over VXLAN**.

The project extends what NetPractice teaches about addressing into the control
plane that actually carries it: OSPF as an underlay, MP-BGP (RFC 4760) with the
EVPN address family (RFC 7432) advertising MAC reachability across VXLAN
(RFC 7348) tunnels — without MPLS.

## Repository map

| Path | Contents |
|---|---|
| [`P1/`](P1/) | GNS3 configuration with Docker — the host image and the routing image |
| [`P2/`](P2/) | Discovering a VXLAN — VNI 10, static then dynamic multicast |
| [`P3/`](P3/) | Discovering BGP with EVPN — route reflector, VTEP leaves, OSPF underlay |
| [`docs/`](docs/) | Architecture notes and the terminology used in the subject |
| [`CONTRIBUTING.md`](CONTRIBUTING.md) | Workflow, commit convention, and the evidence a pull request must carry |

Each part folder holds its portable GNS3 export (`Px.gns3project`, base images
included) and the commented configuration of every piece of equipment in it.

## The three parts

**P1 — GNS3 configuration with Docker.** Two images built by hand: a light host
based on Alpine with busybox, and a router running a packet-routing stack
(FRR/Quagga) with **BGPD**, **OSPFD** and an **IS-IS** engine active. Neither
image carries an IP address by default — addressing belongs to the topology.

**P2 — Discovering a VXLAN.** A layer-2 overlay with **VNI 10**, interface
`vxlan10` enslaved to bridge `br0`, first with static remote peers, then with a
multicast group so peers are discovered dynamically.

**P3 — Discovering BGP with EVPN.** The same VNI, but MAC learning moves to the
control plane. Leaves act as VTEPs with dynamic sessions to a **route
reflector**; OSPF carries the underlay. Type-3 routes appear from configuration
alone, and type-2 routes appear as hosts come up — with no IP address assigned.

## Running the labs

Everything runs inside a virtual machine with GNS3 and Docker installed.

To open a part, import its export in GNS3 via *File > Import portable project*.
The export bundles the base images, so it does not depend on what is already in
the local Docker daemon.

Per-part setup notes, addressing plans, and the verification commands used to
validate each topology live in that part's `README.md`.

## Contributing

`main` is protected: work happens on branches, lands through reviewed pull
requests, and every pull request carries the command output or captures that
prove the topology behaves as claimed. See [`CONTRIBUTING.md`](CONTRIBUTING.md).

## License

[MIT](LICENSE).
