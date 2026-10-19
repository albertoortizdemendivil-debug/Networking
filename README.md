# Networking Labs: Linux Services on Debian 12

Hands-on labs where I build a small segmented network (LAN + DMZ) and deploy the core services on top of it: routing and NAT, DHCP, DNS, FTP, web, mail and a firewall. Each lab has its own guide, a diagram and verification tests, so every step can be reproduced and checked.

I'm an ASIR student (Spain), preparing for Cisco CCNA.

> ✏️ **Fill in:** everything in `<angle brackets>` is something only you can confirm. Delete any line you cannot back up with what is actually in the repo.

## Lab environment

| Item | Detail |
| --- | --- |
| Hypervisor | `<VirtualBox / other, with version>` |
| OS | Debian 12 (all machines) |
| Machines | `<e.g. 1 router/firewall, 1 DMZ server, 1 LAN client>` |
| Networks | LAN `<192.168.x.0/24>`, DMZ `<10.x.x.0/24>`, WAN via NAT |

## Topology

```
                    Internet
                       │
                  [ NAT / WAN ]
                       │
                ┌──────┴──────┐
                │   Router    │  iptables, IP forwarding
                │ (Debian 12) │
                └──┬───────┬──┘
                   │       │
            LAN <net>     DMZ <net>
              clients     DNS / FTP / web / mail
```

*Replace this with the real diagram from lab 01 and keep it consistent with the IPs used in the guides.*

## Labs

| # | Lab | What it covers | Main software |
| --- | --- | --- | --- |
| 01 | [Router, LAN, DMZ and NAT](./01-router-lan-dmz-nat) | `<Routing between three zones, source NAT, IP forwarding>` | `<iptables / nftables>` |
| 02 | [DHCP server](./02-dhcp-server-lan-dmz) | `<Scopes for LAN and DMZ, reservations, relay if used>` | `<isc-dhcp-server / kea>` |
| 03 | [DNS](./03-dns-bind9-dmz-lan) | `<Authoritative zone, reverse zone, forwarders, caching>` | BIND9 |
| 04 | [FTP server](./04-ftp-server-vsftpd) | `<Virtual/local users, chroot, TLS if enabled>` | vsftpd |
| 05 | [HTTP server](./05-http-server-apache) | `<Virtual hosts, HTTPS if enabled>` | Apache |
| 06 | [Mail server](./06-mail-server-postfix-dovecot) | `<SMTP + IMAP, mailboxes, tested with which client>` | Postfix, Dovecot |
| 07 | [Firewall](./07-firewall-iptables) | `<Default-drop policy, rules per zone, logging>` | iptables |

## How each lab is organised

Every folder follows the same structure:

1. **Goal and prerequisites**
2. **Step-by-step configuration**, with the real config files
3. **Verification tests**, with commands and expected output
4. **Troubleshooting**, covering problems I actually hit

## Example of what a lab proves

`<Pick one real test from your repo and paste it here. For example: the dig/nslookup output proving internal resolution works from the LAN, or the failed connection from LAN to DMZ that the firewall should block.>`

```
<command>
<real output>
```

## What I learned

- `<One concrete problem you solved, e.g. "DHCP leases weren't reaching the DMZ until I ...">`
- `<One mistake that taught you something about NAT, DNS or the firewall>`

## Status and next steps

- [x] Labs 01 to 07 documented
- [ ] `<Repeat the labs in Cisco Packet Tracer as part of CCNA prep>`
- [ ] `<Automate one lab with Ansible, only if you actually plan to>`

## Notes

- Guides are written in English; the labs were built in a virtual environment and are not production configurations.
- No real credentials or public IPs are committed; sensitive values appear as placeholders.
