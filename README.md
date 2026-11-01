# public cloud hosting: How It Works, What It Really Costs, and How to Pick a Plan Without Bill Shock

Public cloud hosting means renting virtual machines, storage, and bandwidth from a shared pool of infrastructure that a provider maintains for many customers at once. You get on-demand scalability and pay-as-you-go pricing, and the provider handles the hardware. The catch that most "what is public cloud" articles skip: the sticker price of a VM tells you very little, because egress bandwidth, storage tiers, and overage rates are where hyperscaler bills quietly balloon. This guide covers how the model actually works, then walks through Sharktech's public cloud — a 2003-established host that guarantees at least 40% cost savings compared to hyperscalers — as a concrete example of what the numbers look like when bandwidth isn't the expensive part.

> **Quick pick:** Most small and mid-size teams searching for public cloud hosting want cloud elasticity without a surprise invoice. Sharktech's Public Cloud Small plan (4 vCPU / 8 GB RAM / 300 GB SSD / 20 TB outbound traffic) costs **$39/month**, inbound traffic is free, and every plan includes 60 Gbps DDoS protection at no extra charge. 👉 [Order Sharktech Public Cloud Small for $39/mo](https://bit.ly/SharKtech)

## What public cloud hosting actually is (and how it differs from a VPS)

Public cloud hosting pools computing resources — CPU, RAM, storage, networking — across many physical servers and parcels them out to multiple customers over the public internet. Your workload runs on virtual machines that can be created, resized, and destroyed through a dashboard or API, and the provider handles hardware maintenance, updates, and physical security.

The distinction from a traditional VPS matters more than marketing usually admits. A VPS gives you fixed resources on a single physical machine: if that box dies or saturates, you feel it. A public cloud draws from a distributed pool, so a single server failure degrades gracefully, and you can split one resource allocation across several VMs in different locations. It also differs from a private cloud, which reserves dedicated infrastructure for a single organization — that's the option for strict compliance or security requirements, at a notably higher price.

The standard trade-offs are worth stating plainly. Public cloud gives you near-unlimited scalability, no upfront hardware spend, and multi-tenant cost sharing. In exchange, you accept less control over the underlying environment than a private cloud or a bare-metal server, and — if you pick the wrong provider — a billing model that punishes traffic. That last point is where provider choice really diverges.

## Sharktech Public Cloud plans and pricing at a glance

Sharktech runs its Public Cloud on OpenStack across five data centers: Los Angeles, Las Vegas, Denver, Chicago, and Amsterdam. The standard plans use a monthly base price that includes a fixed resource allocation, with usage above that allocation metered hourly.

| Plan | Config (vCPU / RAM / SSD) | Outbound traffic | Price | Order |
| --- | --- | --- | --- | --- |
| Public Cloud Small | 4 cores / 8 GB / 300 GB | 20 TB included | $39.00/mo | [Order Small](https://bit.ly/SharKtech) |
| Public Cloud Medium | 8 cores / 16 GB / 800 GB | 20 TB included | $79.00/mo | [Order Medium](https://bit.ly/SharKtech) |
| Public Cloud Large | 32 cores / 64 GB / 1,500 GB | 20 TB included | $249.00/mo | [Order Large](https://bit.ly/SharKtech) |
| Public Cloud Enterprise | 64 cores / 128 GB / 5,000 GB (configurable) | 20 TB included | $499.00/mo | [Order Enterprise](https://bit.ly/SharKtech) |
| Custom | Fully configurable | Configurable | Contact sales | [Request a custom quote](https://bit.ly/SharKtech) |

A few things every plan includes, regardless of tier:

- **60 Gbps DDoS protection per IP, built in and free.** Sharktech's network has been designed around DDoS mitigation since 2003, and it's not a paid add-on the way it often is at bigger clouds.
- **Free inbound traffic.** Only outbound (egress) traffic counts.
- **First public IPv4 free**, plus IPv6; additional IPv4 addresses are $1.50/month each.
- **Quarterly, semi-annual, and annual billing** on the fixed tiers earns 5%–15% discounts.
- **OpenStack API access**, private networks, routers, security groups, floating IPs, firewalls, and load balancing — standard cloud networking, restricted to approved source IPs.
- **24/7/365 support staffed by infrastructure engineers**, with phone support available — genuinely uncommon at the $39/month tier.

One storage note that affects day-to-day performance. The platform offers three storage tiers, and the published throughput numbers make the differences concrete: NVMe runs at roughly 1.2 GB/s with about 18,000 IOPS (the choice for databases and AI workloads), SSD at about 350 MB/s and 6,000 IOPS for general use, and HDD at around 120 MB/s and 3,000 IOPS for archives and backups. You can mix tiers across volumes, so a database volume on NVMe with backup volumes on HDD is a normal setup.

## The billing details most articles skip

Here's the part that decides whether a cloud bill is predictable or frightening, and it rarely makes it into comparison posts.

**Resource ceilings are not spending caps.** Sharktech's Small, Medium, and Large plans have resource ceilings, and their own FAQ is explicit about this: "Resource ceilings are not monetary spending caps." If you burst past your included allocation, you pay hourly rates for the excess — the ceiling limits how far resources can scale, not how much you can be charged. Enterprise has no preset ceiling. If you need a hard budget guarantee, that's a reason to look at the fixed-allocation line below instead.

**Overage rates are published and low.** Usage above your included allocation is metered hourly:

| Resource | Hourly rate |
| --- | --- |
| CPU | $0.0025 per core |
| RAM | $0.0035 per GB |
| NVMe storage | $0.00009 per GB |
| SSD storage | $0.00006 per GB |
| HDD storage | $0.00002 per GB |

Egress beyond the included pool is **$0.002/GB**. The typical hyperscaler charges roughly $0.05–$0.12/GB for the same thing. Run the arithmetic on a 10 TB/month outbound workload: at $0.09/GB, a hyperscaler bills around $900 just for bandwidth. On a Sharktech plan that includes 20 TB, it's $0. If the workload exceeded the included pool entirely, 10,000 GB × $0.002 is about $20. That 25–60x gap on egress is the single biggest cost lever for anyone hosting websites, APIs, backups, or media.

The platform itself advertises a 99.999% uptime guarantee backed by triple-redundant, hyperconverged infrastructure with automatic failover — treat that as the provider's own claim, but it's the same five-nines figure the big clouds build their SLAs around.

For an independent performance data point, HostAdvice's testing found "6,000+ random IOPS, sub-millisecond network latency … Sharktech delivers genuine power." That's consistent with the NVMe-first storage approach.

👉 [Check current Public Cloud pricing and hourly rates](https://bit.ly/SharKtech) before ordering — the base price covers the included allocation, and Sharktech's cost calculator lets you model your specific usage before committing.

## Fixed-Price Public Cloud: the version for predictable budgets

If metered overages sound like an accounting headache, Sharktech runs a second billing mode on the same OpenStack platform and the same five data centers. You prepay a fixed monthly amount for a set resource allocation, with no hourly charges and no automatic overages. Need more capacity later? You upgrade the allocation through the billing platform.

The published fixed-allocation tiers run as follows:

| Tier | vCPU / RAM | Price |
| --- | --- | --- |
| XS | 8 cores / 16 GB | $86.23/mo |
| S | 16 cores / 32 GB | $140.95/mo |
| M | 32 cores / 64 GB | $250.39/mo |
| L | 64 cores / 128 GB | $469.27/mo |
| XL | 128 cores / 256 GB | $907.03/mo |
| XXL | 256 cores / 512 GB | $1,782.55/mo |

The official guidance for choosing between the two billing modes: the metered Public Cloud suits workloads with changing resource demand; the fixed-allocation mode suits steady workloads and predictable budgets. Both run one or many VMs on the same platform with the same API access and support. Long billing cycles (quarterly through annual) earn 5%–15% discounts on fixed allocations.

👉 [Compare both Public Cloud billing modes](https://bit.ly/SharKtech) if your monthly resource consumption is stable — fixed allocation usually wins on price once you know your steady-state numbers.

## Who Sharktech fits — and who should look elsewhere

Being honest about fit saves everyone time.

**Good fit:**

- **Traffic-heavy workloads**: websites, download servers, backup targets, media delivery. Free ingress and 20 TB included egress change the economics entirely versus per-GB hyperscaler billing.
- **Teams that want real cloud features without enterprise pricing**: OpenStack APIs, private networking, load balancers, and a resource pool you can carve up freely — an 8 vCPU / 8 GB / 300 GB allocation, for example, can run as one VM or be split into four smaller ones as your needs change.
- **DDoS-exposed services**: game servers, public APIs, anything that attracts attacks. 60 Gbps of included mitigation per IP is a line item most providers charge extra for, and it can be expanded to 1 Tbps for enterprise needs.
- **MSPs and agencies** managing client infrastructure across regions — five locations on two continents, and Sharktech runs a Cloud Accelerator Program offering free assessments, migration blueprints, and credits to qualifying MSPs and small businesses.

**Less good fit:**

- **Strict compliance workloads** requiring single-tenant isolation. Public cloud is multi-tenant by definition; you'd want a private cloud or dedicated infrastructure.
- **Anyone deep in a hyperscaler's managed ecosystem.** If your stack depends on specific managed services (managed Kubernetes with proprietary integrations, serverless platforms, vendor-specific AI tooling), a raw OpenStack cloud means re-platforming work. Migrating typically involves creating images of your instances and uploading them — Sharktech supports qcow2 and ISO uploads, and you can download your disk images at any time for offsite backups, so there's no lock-in, but the migration labor is real.
- **Tinkerers who want the absolute cheapest entry point.** Sharktech's own Smart VPS line starts at $7.95/month (or $3.98/month on annual billing at 50% off, applied automatically with no coupon) — but a VPS is a fixed resource slice on Proxmox, without the cloud's API-driven scaling or hourly bursting. Public cloud at $39 is a different product for different needs.

For a sense of the broader market: European providers like my.host compete on data sovereignty and green energy, offering €200 in free credits and a 99.99% SLA on CloudStack-based infrastructure in Amsterdam — a reasonable route if EU data residency is your priority. The hyperscalers remain the choice when you need their managed service catalogs. Sharktech's lane is simpler: OpenStack-native cloud with bandwidth that doesn't punish you, and the company's published guarantee of at least 40% cost savings compared to hyperscalers.

## Getting started: deployment and daily use

Ordering is a portal-based flow: pick a plan, choose one of the five locations, and the resource pool provisions with a public IPv4 attached. From there you work in the cloud panel or through the standard OpenStack REST API, which covers compute, networking, block and object storage, images, and identity/project management.

Day-to-day, three capabilities matter most:

1. **Flexible VM carving.** Resources are allocated to your cloud environment as a pool, not per named VM. Resize, add machines, or consolidate as load changes — the billing tracks the aggregate allocation.
2. **Bring your own OS.** Weekly-updated official Linux cloud images are provided, and you can upload any compatible qcow2 or ISO image, including Windows. Pull your images back down whenever you want a copy.
3. **Standard networking primitives.** Virtual routers, security groups, floating IPs, and load balancing are all built into the platform — no third-party load balancer required for basic setups.

## FAQ

**Is inbound traffic really free on Sharktech Public Cloud?** Yes. Ingress is unmetered on all Public Cloud plans; only outbound traffic counts against the 20 TB included pool, with overage at $0.002/GB.

**What happens if I exceed my plan's resources?** Usage above the included allocation is charged at the published hourly rates (CPU $0.0025/core/hr, RAM $0.0035/GB/hr, and so on). Small, Medium, and Large plans have resource ceilings that limit how far you can burst — but note those ceilings cap resources, not spending. Enterprise has no preset ceiling.

**Can I run Windows?** Yes. The platform supports Linux and Windows VMs, with official Linux cloud images updated weekly and support for uploading your own ISO or qcow2 images.

**Where are the data centers?** Los Angeles, Las Vegas, Denver, Chicago, and Amsterdam. The Las Vegas facility is SOC-2 compliant with fully redundant power and networking, and the network includes transit from China Telecom and China Mobile — relevant if you care about Asia-Pacific connectivity.

**How is this different from a regular VPS?** A VPS is a fixed allocation on one machine. Public cloud runs on OpenStack across a redundant hyperconverged pool, with API-driven provisioning, hourly bursting, multi-VM resource pools, and cloud networking features a VPS doesn't offer.

## Bottom line: picking between the plans

Match the plan to your workload, and the decision gets short:

- **Testing, a staging environment, or a single mid-size site** → Public Cloud Small at $39/month is genuinely enough, and the 20 TB traffic pool is generous at this price.
- **Production apps with variable load** → Medium ($79) or Large ($249), and let hourly bursting absorb peaks instead of overprovisioning.
- **Steady, known resource needs** → the fixed-allocation tiers from XS ($86.23) upward remove overage math entirely.
- **Very large or unusual requirements** → contact sales for a custom allocation rather than stacking multiple plans.

Two things to confirm before you order: where your users are (pick the closest of the five locations), and whether your outbound traffic fits comfortably inside 20 TB — if it regularly exceeds that, the fixed-allocation line or a custom quote will price out better. When you're ready, 👉 [start with Sharktech Public Cloud Small at $39/mo](https://bit.ly/SharKtech) and scale the allocation from there — with ingress free and DDoS protection included, the worst-case first month is a number you already know.
