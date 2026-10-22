---
title: Tailscale
tags:
  - tools/networking
---

# Tailscale

```text
- Tailscale joins your devices into one private network called a tailnet.
- It uses WireGuard to encrypt traffic end to end.
- A coordination server shares keys and access rules, not the traffic itself.
- Devices connect directly when they can; DERP relays only forward encrypted packets.
- It is not an anonymity VPN.
```

Tailscale is a **mesh VPN** built on WireGuard. It makes devices in different places behave as if they were on the same private LAN, without port forwarding or a central VPN gateway. The private network you create is called a **tailnet**.

## The problem it solves

Remote access normally has three problems:

1. **Identity** — who is allowed in?
2. **Reachability** — how do two devices find each other through NAT and firewalls?
3. **Encryption** — how do you keep the traffic private?

A traditional VPN solves these by routing everything through one central gateway. That is simple to reason about, but it adds latency, creates a bottleneck, and requires running that gateway.

Tailscale keeps the central part small and moves the traffic off it.

## Analogy: switchboard, then direct line

Think of a phone switchboard. It knows every extension and connects callers. Once connected, the call goes directly between the two phones. Tailscale's coordination server is the switchboard; the WireGuard tunnel is the direct call.

Where the analogy breaks: the switchboard does not listen to the call, and if a direct line is impossible, Tailscale forwards sealed packets through a relay (DERP) instead. The relay cannot open them.

## How it works

Tailscale splits into two planes:

- **Control plane** — the coordination server (`login.tailscale.com`). It authenticates devices through your identity provider, distributes public keys, tells each device where the others are, and pushes access rules. Private keys never leave the devices. The server sees metadata such as which devices exist and when they connect, not the traffic itself.
- **Data plane** — WireGuard tunnels between devices. When possible, devices connect directly peer-to-peer. NAT traversal tries STUN, UPnP, NAT-PMP, and PCP. If a direct path fails, traffic falls back to DERP relays, which forward encrypted packets.

So the control plane is hub-and-spoke, but it carries almost no data. The data plane is a mesh.

## What you get

- **MagicDNS** — human-readable names such as `laptop.tailnet.ts.net` instead of IP addresses.
- **ACLs** — identity-based rules for who can reach which device or service.
- **Exit nodes** — route all your internet traffic through another device, like a traditional VPN.
- **Subnet routers** — expose a whole LAN (for example a home network) without installing Tailscale on every device.
- **Taildrop** — send files directly between your devices.
- **Tailscale SSH** — log in to machines using your Tailscale identity instead of managing SSH keys.
- **Funnel** — expose a service to the public internet over HTTPS.

## What it is not

- **Not an anonymity VPN.** It connects your own devices privately; it does not hide your browsing from websites. An exit node changes your apparent IP, but that is a different use case.
- **Not fully self-hosted by default.** The client is open source, but the coordination server is Tailscale's service. Headscale is a third-party open-source alternative.
- **Not a replacement for a firewall.** It controls access between tailnet members; you still secure the services themselves.
- **Not always direct.** On restrictive networks, traffic may go through a DERP relay. It stays encrypted, but latency can increase.
- **Subnet routes are an encryption boundary.** The subnet router decrypts traffic to deliver it to devices behind it.

## Pricing and getting started

The Personal plan is free for non-commercial use. As of 2026 it allows up to 6 users, unlimited user devices, 50 tagged resources, and 3 ACL groups; check [tailscale.com/pricing](https://tailscale.com/pricing) because plans change.

Typical setup:

```bash
# Linux
curl -fsSL https://tailscale.com/install.sh | sh
sudo tailscale up

# Check the tailnet
tailscale status
tailscale ip -4
```

Install the app on phones and laptops, sign in with the same account, and they join the same tailnet. The admin console is where you enable MagicDNS, write ACLs, and approve routes or exit nodes.

## Background

Tailscale Inc. was founded in 2019 by Avery Pennarun, David Crawshaw, David Carney, and Brad Fitzpatrick, and is based in Toronto. The name comes from the paper "The Tail at Scale". The company raised a $160M Series C in 2025.

## Sources

- [How Tailscale works](https://tailscale.com/blog/how-tailscale-works)
- [What is Tailscale?](https://tailscale.com/docs/concepts/what-is-tailscale)
- [Tailscale pricing](https://tailscale.com/pricing)
- [Tailscale on Wikipedia](https://en.wikipedia.org/wiki/Tailscale)
