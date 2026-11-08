# Dedicated VPS Server Explained: What You Actually Get, What It Costs, and When a $79 Bare-Metal Box Beats a Pricier VDS (Full Plan Table)

A dedicated VPS server is a virtual machine whose CPU cores and RAM are reserved for that VM alone on a shared physical host. You get isolation and predictable performance without paying for a whole machine, and the going rate is roughly $50 to $320 a month for 2 to 16 dedicated cores.

Then there's the part the pricing pages rarely put side by side: at the bottom of that range, you can rent the entire physical server instead. SpinServers lists a full Xeon E3-1280 v5 with 4 cores / 8 threads, 32 GB DDR4 ECC, a 1 TB M.2 NVMe drive and 30 TB of monthly transfer for **$79/month**, month to month, no setup fee. Several providers charge more than that for a 32 GB VDS slice carved out of somebody else's host.

So the honest answer to "which dedicated VPS should I buy" often turns into "do you need the hypervisor at all." Below: what "dedicated" really reserves, the four SpinServers configurations with published prices, the sizing rules that decide how many cores you need, and the cases where a VDS is still the correct purchase.

> **Quick pick:** most readers searching for a dedicated VPS land in the 4-core / 16–32 GB bracket. The SpinServers Xeon E3-1280 v5 at $79/month covers that bracket with a whole physical server, 32 GB of ECC RAM, 1 TB NVMe and 30 TB of transfer, billed monthly with no setup fee. Need 256 GB of RAM for a database or build farm? The Growth Package at $149/month is the step up.
>
> 👉 [Check the $79 Xeon E3-1280 v5 configuration and current availability](https://bit.ly/Spinservers)

## The SpinServers plans with published monthly prices

These are the four configurations carrying a public monthly price on SpinServers' Dallas pricing page, as listed at the last public price check in September 2026. Month-to-month terms, no setup fee, full root access.

| Plan | CPU / RAM | Storage & transfer | Price | Order |
| --- | --- | --- | --- | --- |
| Intel Xeon E3-1280 v5 | 4 cores / 8 threads @ 3.7 GHz turbo, 32 GB DDR4 ECC | 1 TB M.2 NVMe, 30 TB on a 10 Gbps port, 1 IPv4 | $79/mo | [Order](https://bit.ly/Spinservers) |
| Starter Package | 32 GB RAM | 1 TB NVMe, 10 TB, 10 Gbps, full root | $99/mo | [Order](https://bit.ly/Spinservers) |
| Growth Package | 256 GB RAM | 2 × 1.6 TB SSD, 20 TB, 10 Gbps | $149/mo | [Order](https://bit.ly/Spinservers) |
| High Performance Package | 768 GB RAM | 8 × 2 TB SSD, 40 TB, 10 Gbps | $679/mo | [Order](https://bit.ly/Spinservers) |

A caveat worth stating plainly: the Starter, Growth and High Performance lines publish RAM, storage, bandwidth and port speed, but not the processor model. If the exact CPU matters to your workload, ask before ordering. The Xeon E3-1280 v5 entry plan is the one config where every spec is spelled out.

The San Jose, California location runs a different inventory built around higher core counts. Prices there are quoted per configuration rather than listed:

| CPU | RAM | Storage | Network |
| --- | --- | --- | --- |
| 12 cores / 24 threads, 2.6 GHz (3.1 turbo) | 64 GB DDR3 ECC | 1 × 240 GB SSD | 2 × 10 Gbps, 30 TB, 1 IPv4 |
| 4 cores / 8 threads, 3.7 GHz (4.0 turbo) | 32 GB DDR4 ECC | 1 × 1 TB M.2 NVMe | 2 × 10 Gbps, 30 TB, 1 IPv4 |
| 16 cores / 32 threads, 1.8 GHz (2.9 turbo) | 64 GB DDR4 ECC | 1 × 1.6 TB SSD | 2 × 10 Gbps, 30 TB |
| 16 cores / 32 threads, 1.8 GHz (2.9 turbo) | 64 GB DDR4 ECC | 1 × 1.6 TB NVMe | 2 × 10 Gbps, 30 TB, 1 IPv4 |
| 24 cores / 48 threads, 1.8 GHz (2.5 turbo) | 64 GB DDR4 ECC | 1 × 1.6 TB SSD | 2 × 10 Gbps, 30 TB |
| 16 cores / 32 threads, 1.8 GHz (2.9 turbo) | 256 GB DDR4 ECC | 2 × 1.6 TB SSD, hardware RAID with cache | 2 × 10 Gbps, 30 TB |
| 32 cores / 64 threads, 2.1 GHz (3.0 turbo) | 512 GB DDR4 ECC | 2 × 3.84 TB SSD, RAID with battery-backed cache | 2 × 10 Gbps, 30 TB, 1 IPv4 |

Both locations advertise instant provisioning, IPMI or iKVM remote management, a DDoS-protected multihomed network, VPC networking with private Layer 2 connectivity, and Linux, Windows or ESXi auto-install. Dedicated IPv4 addresses and an IPv6 /64 block are part of the listings.

## What "dedicated" actually reserves

Three different products get sold under nearly the same words, and the difference decides whether you're buying guaranteed silicon or a promise.

**A shared VPS** is a slice of a physical server with a predetermined resource allocation. AWS describes it as a partitioned segment of a machine where several VPSs share the underlying hardware in a fixed manner. Another tenant hammering the host can still show up as jitter on your side.

**A dedicated VPS (VDS)** puts a floor under your allocation. Contabo, which sells both lines, describes the difference as resource allocation that "minimizes the impact of other servers on the same machine." Your RAM is yours. Your core count is guaranteed.

**A dedicated server** gives you the entire box. All cores, all RAM channels, all drive bays, no virtualization layer between your kernel and the hardware.

Here's the wrinkle that matters when you compare prices. Contabo's VDS page says each plan comes with "100% dedicated RAM, processors" and then, in the same table, lists "12 Virtual Cores AMD EPYC 7282 2.8 GHz." Both statements are accurate under their own definition: you exclusively own 12 logical cores' worth of scheduling on a much larger CPU. You do not own 12 physical cores. That distinction is standard across the VDS category, and it's why a "16 dedicated cores" VDS can cost less than a 16-core bare-metal server. When you compare any two dedicated VPS offers, check whether the spec says cores, vCores, or threads.

SpinServers sells the other end of that spectrum. The Xeon E3-1280 v5 is 4 cores and 8 threads on a machine nobody else is scheduled onto. You give up live migration and hypervisor-level snapshots, and you gain the whole memory bus and every drive.

## Where a VDS still beats bare metal

Buying the physical server isn't automatically the better call. A virtual dedicated server gives you things a bare-metal rental doesn't:

**Resizing without a migration.** AWS notes that VPS instances scale by reallocating resources, while a dedicated server grows by physically adding hardware, which carries cost and can involve downtime. If your capacity needs swing month to month, that flexibility is worth real money.

**Hourly billing and fast teardown.** RamNode prices its dedicated CPU VPS line by the month and the hour, from $0.074/hr on the 8 GB plan up to $0.476/hr on the 64 GB plan. SpinServers bills monthly. For a two-week load test, hourly wins.

**Compliance paperwork that assumes virtualization.** Multi-tenant cloud environments get audited against HIPAA, PCI DSS, SOC 2/3 and GDPR every day. AWS is direct about the tradeoff: a VPS has effective security but may not always meet complex compliance requirements, and some regulations covering highly sensitive data effectively require a dedicated environment.

**Multi-instance density.** A dedicated host lets you run many instances on one physical machine and bill per host rather than per instance. Atlantic.Net structures its dedicated hosts that way, with bring-your-own-license support for SQL Server, Oracle and Exchange, which is how teams with existing per-core licenses avoid paying twice.

If any of those four describe your situation, a VDS or a dedicated host is the right product and the SpinServers plans below are the wrong shape for you.

## How many cores do you actually need?

Published sizing notes from providers are the closest thing to a baseline. RamNode publishes its own for its dedicated CPU VPS line, and the numbers map cleanly onto what most workloads need.

| Workload | Starting point | Comfortable |
| --- | --- | --- |
| Docker / CI builds | 3 cores, 6 GB | 4 cores, 16 GB for frequent builds or 10+ services |
| PHP control panel hosting | 3 cores, 6 GB for 20–50 sites | 4 cores, 16 GB for 100+ client sites |
| Kubernetes | 4 cores, 8 GB minimum for real workloads | 8 cores, 16 GB+ for production with latency-sensitive services |
| Databases | 2 cores, 4 GB under 10 GB of data | 4 cores, 16 GB for 100+ concurrent connections |
| Redis / Valkey / Memcached | 2 cores, 4 GB | 4 cores, 16 GB for high-throughput session stores |
| VPN endpoints | 2 cores, 4 GB for 10–20 clients | 4 cores, 8 GB for 100+ clients or site-to-site meshes |

Treat these as general industry estimates, not vendor commitments, and note they're written for virtual cores. On bare metal, 4 physical cores with 8 threads and 32 GB of RAM clears the "comfortable" column for most of the table, which is exactly why the $79 entry configuration is the one most buyers should start with. If you're running a 256 GB database, jump to the Growth Package.

The workloads people underestimate are build pipelines and control planes. Docker builds and Kubernetes scheduling are CPU-bursty, and a shared host that looks fine at idle will stall during a deploy. That's the specific pain dedicated cores solve.

## The real cost is the renewal price, not the sticker

Promotional pricing in this category is aggressive enough that the first-term price tells you very little.

Contabo's Cloud VDS L is **$92.00/month for the first 24 months** against a list price of **$115.00**. The XXL is **$181.60** against **$227.00**. Run the L for three years and the math looks like this: 24 months at $92.00 is $2,208, then 12 months at $115.00 is $1,380, for $3,588 total. That averages $99.67/month. The advertised $92 was real, but it wasn't the price of the third year.

SpinServers' $79 Xeon configuration is month-to-month at a flat rate. Over the same 36 months that's $2,844, or $79 every month with no cliff. The comparison isn't that one provider is cheaper in every scenario. It's that a promo rate and a list rate are different products, and you should price the term you actually intend to keep.

Before you order anything in this bracket, write down four numbers: the first-term monthly price, the list monthly price, the length of the discount period, and the total cost across your expected lifespan. If a provider won't state the renewal rate before you pay, assume list price.

👉 [See the SpinServers Xeon E3-1280 v5 at its flat monthly rate](https://bit.ly/Spinservers)

## Read the bandwidth clause before the CPU

"Unlimited traffic" in VDS marketing almost always has a shape. Contabo spells out its version: inbound traffic is unlimited and unmetered with no extra charges, outbound is "unlimited" subject to a fair usage policy based on average server workloads, and the provider reserves the right to throttle servers with exceptionally high or disruptive usage. That's a reasonable policy, and it means your ceiling is a port speed plus a judgment call, not a number.

SpinServers meters instead: 30 TB per month on the entry plan, on a 10 Gbps port. Spread evenly across 30 days, 30 TB averages about 93 Mbit/s of continuous throughput, so the 10 Gbps port is headroom for bursts, not a sustained allowance. If your traffic is spiky (media delivery, backup windows, nightly syncs), metered bandwidth on a fast port is a good fit. If you're pushing a constant 500 Mbit/s, no plan in this price band will hold without an overage conversation.

Pull your last month of egress from your current host before you order. The bandwidth clause will outlive the CPU choice.

## Who shouldn't buy this

- **A single low-traffic site or a static site.** A $4/month standard VPS handles it. You'd be paying for isolation you don't need.
- **A staging environment you spin up twice a week.** Monthly billing on bare metal is the wrong instrument. Take an hourly VDS.
- **Anyone who needs managed support.** These are unmanaged servers with root access. Patching, hardening and backups are your job.
- **Teams that need managed PCI compliance or audit support.** SpinServers advertises PCI-compliant facilities, but the offering is built for teams running their own compliance work, not for buyers who want compliance handled for them.
- **Multi-region latency requirements.** There are two locations, Dallas and San Jose. If your users are in Frankfurt and Singapore, look elsewhere.

Worth knowing before you commit: month-to-month service at SpinServers generally comes with no refund policy, so the first invoice is the risk. Reviewers have also flagged that published detail on backups and disaster recovery is thin beyond power and network redundancy, and that pricing varies by location, hardware and availability. Ask specifically what happens to your data if a drive fails on day three.

## Picking your configuration

Work down this list and stop at the first line that matches:

- One site, under a few thousand visits a day, no build pipeline → shared VPS at $4–14/month, not this bracket.
- Containerized app or CI runner with 10+ services, needs 16 GB → the $79 Xeon with 32 GB, or a 4-core / 16 GB dedicated VDS at around $90.
- Production Kubernetes or a database over 100 GB → 8+ cores and 64 GB. The $149 Growth Package or a San Jose 16-core configuration.
- 100+ concurrent database connections or a 256 GB working set → Growth Package, $149/month.
- Heavy virtualization, per-core licensed software, or a build farm → the San Jose 32-core with 512 GB, quoted per configuration.

Before you pay, confirm six things: the billing term, the renewal price, whether the refund policy covers your case, which of the two locations you're being provisioned in, that the IPv4 address is included, and whether the Windows or ESXi install you want carries a license cost.

👉 [Start with the $79 dedicated server and upgrade the plan later if you outgrow it](https://bit.ly/Spinservers)
