# Evoxt Plans and Pricing Explained: What $2.99 a Month Actually Buys, Which Plan a WordPress Site Needs, and Why Hong Kong Costs the Same but Moves Half the Data

Evoxt's cheapest plan is **$2.99/month**: 1 vCPU, 512 MB RAM, 5 GB disk, 500 GB of transfer. The plan most people actually end up needing is **VM-1 at $5.99**, which takes the RAM to 2 GB, the disk to 20 GB and the transfer to 1 TB. Every plan includes KVM virtualisation, an IPv6 address, a free weekly offsite backup, and the same advertised 3.5 GHz+ CPU frequency.

What Evoxt sells is clock speed. Its homepage sets a 6.0 GHz bar beside 2.4, 2.3 and 2.2 GHz bars attributed to other providers, and the company's own description says it prices 3.5 GHz-and-up hardware like the low-clock competition. Two caveats worth carrying: the comparison chart itself notes the data were collected in 2020 and "might differ in the future," and Evoxt does not publish which CPU model you get.

Below: the full plan list, the traffic penalty that comes with the Asia-optimised regions, what 512 MB can realistically run, and the operational limits that don't appear on the homepage.

> **Quick picks**
> - **One website, one small API, one database:** VM-1 at **$5.99/mo** (1 vCPU, 2 GB, 20 GB, 1 TB).
> - **A script, a probe, a proxy hop:** VM-0.5 at **$2.99/mo** — 512 MB and 5 GB, nothing more.
> - **Users in mainland China or Southeast Asia:** Hong Kong or Osaka at the same price, but VM-1 gets 500 GB instead of 1 TB.
>
> 👉 [See current Evoxt plans and pricing](https://bit.ly/EvoXt)

## The full plan list on the standard network

Standard-network pricing covers the US, Canada, the UK, Germany, the Netherlands, Japan (Tokyo), Malaysia and Australia, plus a handful of other European cities. Prices are monthly, in USD, and identical across those locations.

| Plan | vCPU | RAM | Disk | Transfer/mo | Price |
| --- | --- | --- | --- | --- | --- |
| VM-0.5 | 1 | 512 MB | 5 GB | 500 GB | $2.99/mo · [ Order](https://bit.ly/EvoXt) |
| VM-0.75 | 1 | 1 GB | 10 GB | 750 GB | $4.99/mo · [ Order](https://bit.ly/EvoXt) |
| VM-1 | 1 | 2 GB | 20 GB | 1 TB | $5.99/mo · [ Order](https://bit.ly/EvoXt) |
| VM-1.5 | 2 | 2 GB | 20 GB | 1.5 TB | $6.95/mo · [ Order](https://bit.ly/EvoXt) |
| VM-2 | 2 | 4 GB | 30 GB | 2 TB | $11.99/mo · [ Order](https://bit.ly/EvoXt) |
| VM-3 | 4 | 4 GB | 30 GB | 3 TB | $14.99/mo · [ Order](https://bit.ly/EvoXt) |
| VM-4 | 4 | 8 GB | 60 GB | 4 TB | $23.99/mo · [ Order](https://bit.ly/EvoXt) |
| VM-6 | 8 | 8 GB | 60 GB | 5 TB | $29.99/mo · [ Order](https://bit.ly/EvoXt) |
| VM-8 | 8 | 16 GB | 80 GB | 6 TB | $47.99/mo · [ Order](https://bit.ly/EvoXt) |
| VM-12 | 16 | 16 GB | 80 GB | 8 TB | $60.95/mo · [ Order](https://bit.ly/EvoXt) |
| VM-16 | 16 | 32 GB | 100 GB | 10 TB | $95.99/mo · [ Order](https://bit.ly/EvoXt) |

Every transfer figure is an allowance rather than a billing meter. Exceed it and the port is throttled, not charged: Evoxt's pricing model is "allowance then throttled," with no per-GB overage invoice and no shared transfer pool between servers.

Billing is monthly. There is no hourly option anywhere in the plan list, which matters if what you want is a two-day test — you'll pay for a month regardless.

## Standard vs premium regions: same price, half the transfer

Hong Kong, Osaka and Malaysia Premium sit on a separate network tier. You pay exactly the same monthly price and get roughly half the monthly transfer, sometimes less.

| Plan | Standard transfer | Premium transfer | Price (both) |
| --- | --- | --- | --- |
| VM-0.5 | 500 GB | 250 GB | $2.99 |
| VM-1 | 1 TB | 500 GB | $5.99 |
| VM-2 | 2 TB | 1 TB | $11.99 |
| VM-4 | 4 TB | 2 TB | $23.99 |
| VM-8 | 6 TB | 3 TB | $47.99 |
| VM-16 | 10 TB | 5 TB | $95.99 |

Premium regions don't carry every size, so confirm the plan you want exists in the city you want before you plan around it.

The reason to accept half the data is the path out. Evoxt describes Hong Kong as CN2 routing optimised for China; Osaka connects through BBIX and JPIX with Softbank transit; Malaysia's premium tier peers locally through MyIX. If your users sit in mainland China or Southeast Asia, that is the trade you're making: identical price, half the allowance, better latency. For everyone else, the premium tier is strictly worse value.

👉 [Open the Evoxt order page to see which plans each region offers](https://bit.ly/EvoXt)

## What a $2.99 machine can actually run

512 MB of RAM and 5 GB of disk is a real server, just a small one. In practice that budget covers a single cron-driven script, an uptime probe, a WireGuard or Tailscale exit node, a small DNS resolver, a static page behind nginx, or a monitoring agent. It does not cover WordPress with MySQL, a Docker host running three containers, or anything JVM-based.

Working rules, by workload:

- **One script or probe → VM-0.5 ($2.99).** 500 GB of transfer is far more than a heartbeat needs.
- **One WordPress site or a small API with a database → VM-1 ($5.99).** 2 GB is roughly what MySQL, PHP-FPM and a little page cache add up to. 512 MB will hit the OOM killer under real traffic.
- **Several sites, or one site plus a cache and a background worker → VM-2 ($11.99).**
- **Minecraft or a busy Discord bot → VM-2 for the RAM, VM-3 ($14.99) if the process is CPU-bound.** VM-3 gives you 4 cores but stays at 4 GB, which is the wrong direction for memory-hungry game servers.

Disk is the constraint people forget. The 20 GB on VM-1 holds the OS, the database and the uploads. If you keep logs or local backups for months, size the disk before you size the CPU.

## The cheapest upgrade in the table is 96 cents

VM-1.5 costs $6.95 against VM-1's $5.99. For 96 cents more you get a second vCPU and 500 GB of extra transfer, on the same 2 GB of RAM and 20 GB of disk. That's the largest relative jump in the entire list, and it rarely gets mentioned because the name makes it sound like a rounding error.

If your workload is one PHP site plus a queue worker, VM-1.5 buys you headroom for less than moving up to VM-2's 4 GB later. Where it buys nothing: single-threaded work. A second core does not speed up a WordPress page render or a single database query, and single-threaded work is precisely what the 3.5 GHz+ pitch is aimed at.

## Limits you only find after paying

**Backups are weekly, not continuous.** Evoxt's page and VPSBenchmarks' feature check agree: one backup per VM per week, restorable from the panel yourself. Worst case you lose seven days. That's acceptable for a blog and not acceptable for a store taking orders. Third-party plan listings also reference an optional paid backup tier with daily copies and manual snapshots priced by disk size, so ask support if a tighter recovery point is a requirement.

**Over-allowance traffic is throttled.** No surprise bandwidth bill, but your port slows down until the next cycle.

**No reverse DNS.** VPSBenchmarks lists reverse DNS as unsupported, and policy summaries flag a default outbound mail-port restriction. Plan to send transactional email somewhere else.

**No DDoS scrubbing product.** Evoxt's homepage credits its Layer 3 firewall with "better DDoS protection"; VPSBenchmarks records DDoS protection as not offered. Read that as packet filtering you configure yourself, not mitigation that absorbs an attack.

**The CPU model is hidden.** You get a frequency range, not a SKU. If you need to know whether you're on EPYC or Xeon for licensing or performance-modelling reasons, you won't find out before deploying.

**Provisioning isn't always 2.5 minutes.** Evoxt advertises "ready to connect within 2.5 minutes." Across six independently measured deployments the median was 175 seconds, the average 261 seconds, and the slowest 600 seconds. Usually close to the claim, occasionally ten minutes.

There's also no shelving: you can't park a VM without paying for it, and there's no hourly billing to soften that.

👉 [Check the current Evoxt plan specs and availability before you commit](https://bit.ly/EvoXt)

## How to read the benchmark numbers

VPSBenchmarks buys and tests these plans independently. Its four most recent Evoxt trials:

| Plan | Test date | Score | PW Score |
| --- | --- | --- | --- |
| VM-1 | 25 Feb 2026 | 53 | 80 |
| VM-2 | 19 Aug 2026 | 50 | 72 |
| VM-4 | 30 Nov 2025 | 60 | 69 |
| VM-8 | 24 May 2026 | 62 | 55 |

The interesting part is the spread, not any single row. VM-1 scored 53 in February; VM-2, with twice the cores and twice the RAM, scored 50 in August. Different dates, different hardware pools, different neighbours on the host. A single trial tells you roughly where a provider sits; it does not rank that provider's own plans against each other, and it certainly doesn't confirm a 6.0 GHz marketing figure.

## Who should not buy Evoxt

- **You need hourly or per-second billing.** Every plan is monthly. Nothing here scales down at the end of a spike.
- **You need real DDoS mitigation.** A configurable Layer 3 firewall is not the same product.
- **You need to send mail from the box**, or need PTR records for deliverability.
- **You need a contractual SLA with credits.** Evoxt's site states at least 99.99% uptime; that's a published target, not a documented credit scheme.
- **You need managed support.** These are unmanaged KVM servers with a custom control panel, monitoring graphs, an API and self-service restores.

## On promo codes

Coupon aggregators and affiliate posts circulate recurring-discount codes for VM-1 and above, often advertised as 40% off. None of those codes appear on Evoxt's own site, and the pages carrying them are monetised and months old. If you find one, enter it at checkout and validate before paying: either the total changes or it doesn't. Don't pick a plan on the assumption that a discount will apply, and don't expect a code to stack with anything else.

## Which plan to order

- **One script, one probe, one tunnel endpoint** → VM-0.5, $2.99.
- **One website or a small API with a database** → VM-1, $5.99.
- **The same, plus a worker, or users in China/SEA** → VM-1.5 for the extra core, or VM-1 in Hong Kong/Osaka and accept 500 GB.
- **Multiple sites, a cache layer, Minecraft** → VM-2, $11.99.
- **Anything above VM-4** → only if you can name the process that needs it.

One thing to check before you pay: the region you pick sets your transfer allowance, and the price doesn't change to warn you. VM-1 in Frankfurt gets 1 TB; VM-1 in Hong Kong gets 500 GB for the same $5.99. Choose the city first, then confirm the allowance on that region's plan page.

👉 [Start from the Evoxt plan list and confirm your region's transfer allowance](https://bit.ly/EvoXt)
