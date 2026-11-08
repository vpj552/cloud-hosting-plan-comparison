# Cloud computing hosting services: fixed-capacity VPS, serverless, or bare metal — which fits your traffic, what each costs per month, and where the cheap plan stops working (SpinServers plans compared)

Steady traffic doesn't need serverless. A fixed-capacity virtual server at a flat monthly rate covers most sites and small applications, and the entry point in SpinServers' KVM lineup is **$12.00/month** for 2 vCPU, 2 GB RAM, 40 GB RAID-10 SSD and 4 TB of monthly transfer. Auto-scaling and per-second billing start to matter when traffic swings hard enough that you'd otherwise pay for idle capacity all month.

The rest of this page covers the three delivery models sold as "cloud hosting", the four hosting environments they get confused with, the billing math behind a $7.99 headline versus a $12 monthly rate, and three costs that rarely appear on a plan card.

> **Quick pick.** One site or a few apps on predictable traffic → KVM 2vCPU 2GB at $12.00/month. A database plus a build process on the same box → 4 vCPU / 4 GB at $29.00/month. You need the entire physical machine and root on the hardware → dedicated from $79.00/month. 👉 [Check the current SpinServers KVM VPS rates](https://bit.ly/Spinservers)

## The full SpinServers lineup

SpinServers sells two things: KVM virtual servers with fixed capacity and pre-built dedicated hardware. Prices below are the listed "starting from" monthly rates; configurations can change at checkout, and the plans are grouped the way the provider groups them.

**KVM virtual servers**

| Plan | vCPU / RAM | SSD / monthly transfer | Listed price | Order |
| --- | --- | --- | --- | --- |
| KVM 2vCPU 2GB | 2 / 2 GB DDR4 | 40 GB RAID-10 / 4 TB | $12.00/mo | [Order this plan](https://bit.ly/Spinservers) |
| KVM 4vCPU 4GB | 4 / 4 GB DDR4 | 80 GB RAID-10 / 8 TB | $29.00/mo | [Order this plan](https://bit.ly/Spinservers) |
| KVM 6vCPU 8GB | 6 / 8 GB DDR4 | 120 GB RAID-10 / 8 TB | $39.00/mo | [Order this plan](https://bit.ly/Spinservers) |
| KVM 8vCPU 8GB | 8 / 8 GB DDR4 | 160 GB RAID-10 / 10 TB | $45.00/mo | [Order this plan](https://bit.ly/Spinservers) |
| KVM 12vCPU 12GB | 12 / 12 GB DDR4 | 160 GB RAID-10 / 10 TB | $62.00/mo | [Order this plan](https://bit.ly/Spinservers) |
| KVM 16vCPU 16GB | 16 / 16 GB DDR4 | 320 GB RAID-10 / 15 TB | $74.00/mo | [Order this plan](https://bit.ly/Spinservers) |
| Hybrid KVM 32vCPU 32GB | 32 / 32 GB | 500 GB SSD / 20 TB | $89.00/mo | [Order this plan](https://bit.ly/Spinservers) |

Every KVM plan ships with a 1 Gbps network port and one IPv4 plus one IPv6 address. The first four sit under "Simple Application Servers", the last three under "Advanced Application Servers".

**Pre-built dedicated servers**

| Configuration | Cores / RAM | Storage / transfer | Listed price | Order |
| --- | --- | --- | --- | --- |
| Intel Xeon E3-1280 v5, Dallas | 4 / 32 GB | 1,000 GB NVMe / 30 TB | $79.00/mo | [Order this server](https://bit.ly/Spinservers) |
| Intel Xeon E3-1280 v5, San Jose | 4 / 32 GB | 1,000 GB NVMe / 30 TB | $79.00/mo | [Order this server](https://bit.ly/Spinservers) |
| Dual Intel Xeon Gold 6148, Dallas | 40 / 256 GB | 3,840 GB SSD / 30 TB | $235.00/mo | [Order this server](https://bit.ly/Spinservers) |
| Dual Intel Xeon Platinum 8173M, Dallas | 56 / 512 GB | 7,680 GB SSD / 30 TB | $390.00/mo | [Order this server](https://bit.ly/Spinservers) |

Two things about that last table worth noting before you read further. The $79 configuration gives you a whole physical machine with 32 GB of RAM for less than the price of a 16 vCPU virtual server, because virtual servers are priced on the assumption that you'll share the hardware. And these are unmanaged boxes with full root access; the provider lists cPanel and Plesk as available control panels, and support runs through ticket, phone and email.

## What "cloud computing hosting services" actually covers

Three delivery models get sold under that phrase.

A **single fixed-capacity virtual server** is the simplest: you pick vCPU, RAM and storage, and those resources are yours for the month. SpinServers' KVM plans are this model. A **cloud network of physical and virtual servers spread across regions** is the second; it's what people usually mean when they talk about scaling horizontally, and it's how providers put workloads near users in different countries. The third is **serverless**, where the provider runs everything, your code fires on events, and you're billed only for the compute time you consume. Nothing runs and nothing bills while the code is idle.

Google's documentation uses a different cut, listing four hosting environments: shared, dedicated, managed and VPS. Shared puts many domains on one server and caps each site at that server's resources. Dedicated leases one or more servers to a single customer, who often manages them. Managed moves the administration to the provider. VPS slices one physical server into isolated virtual environments.

Both frameworks describe the same market from different angles. The AWS version tells you what you're buying; the Google version tells you who's doing the work. Worth keeping separate from either: cloud hosting can deliver web hosting, but web hosting doesn't necessarily involve cloud computing. A shared plan on a single rented machine is web hosting without a cloud layer anywhere in it.

## Cloud, VPS, shared, dedicated: the differences that change your bill

|  | Shared | Cloud network | Single VPS | Dedicated |
| --- | --- | --- | --- | --- |
| Resources | Shared across tenants on one server | Virtualized, spread across a cluster | Fixed allocation on one server | Entire machine, one customer |
| Performance | Moves with neighbours' traffic | Dynamically allocated | Stable until you hit the allocation | Consistently high |
| Scaling | Fixed, plan-bound | Up or down on demand | Plan change or migrate | Upgrade or migrate hardware |
| Failure boundary | One server takes every site down | Workload shifts to another node | The host machine and the VM go together | That one physical server |
| Isolation | Lowest | Segmented by virtualization | Higher than shared | Highest |
| Control | Minimal | Medium to high | Root access | Full root and hardware control |
| Cost model | Lowest flat fee | Usage-based | Flat monthly | Highest flat fee |

The failure-boundary row is the one people skip. A VPS is confined to the resources of a single server, so the hypervisor's host is your availability ceiling. A distributed cloud network can move work to another node. A dedicated box is as reliable as the one machine sitting in the rack.

Google's page notes that VPS is sometimes called "the private cloud". AWS uses private cloud for something narrower: resources isolated to one organisation, usually on dedicated hardware it controls. Treat the two as different terms even though marketing blurs them.

## What the monthly price actually buys

Three pricing logics are in play, and their headline numbers can't be lined up side by side.

**Long-term prepay, quoted as a monthly equivalent.** Hostinger lists managed cloud hosting at **$7.99, $15.99 and $29.99 per month**, and its page states these are the monthly prices of the 48-month plan. No renewal rate and no month-to-month rate appear on that page. Four years at $7.99 works out to $383.52 across the term, paid on a four-year commitment rather than monthly.

**Flat monthly, no stated term.** SpinServers lists the KVM 2vCPU 2GB plan at $12.00/month with no term requirement shown on the listing. The same 48 months at today's rate comes to $576, and you can leave at the end of any month. The gap between $383.52 and $576 is what the four-year lock-in is worth.

**Consumption plus discounts.** AWS bills for the instances and resources you actually use, sells unused EC2 capacity as Spot instances at up to 90% below On-Demand pricing, and offers Savings Plans at up to 72% off in exchange for a commitment that can be shared across instances, containers and serverless. Google Cloud bills pay-as-you-go, applies automatic monthly discounts as usage grows, and charges less for prepaid resources. Atlantic.Net sells cloud servers pay-as-you-go on compute, storage and bandwidth, or as reserved instances.

A $7.99 line, a $12.00 line and a per-second EC2 line describe different commitments. Compare total spend over the term you'll realistically stay, not the first number on the pricing page.

## Costs that never make it onto the plan card

**Outbound email is blocked by default.** SpinServers closes port 25 on every VPS to limit IP abuse. If your application sends mail through SMTP on the server itself, you have to open a ticket with a justification, and the provider reserves the right to refuse. Budget for a transactional email service, or plan for that support step.

**Backups are usually an add-on.** AWS describes backup and recovery as an additional capability you buy for disaster recovery, not something bundled with a self-managed server. Ask the same question of any host: is a snapshot schedule included, and what does restoring from it cost.

**Extra IP addresses are metered.** Atlantic.Net includes one IPv4 per server and charges **$3.65/month ($0.005431/hour)** for each additional one. SpinServers includes one IPv4 plus one IPv6 on its KVM plans. If you're terminating TLS for several domains on separate addresses, that line item adds up quietly.

**Patching is your job on unmanaged plans.** AWS spells out the split: the provider patches its own systems, and customers running self-managed cloud hosting update operating systems, applications and libraries themselves. Serverless and managed services shift more of that responsibility to the provider. SpinServers' KVM and dedicated plans are unmanaged, so kernel updates, application security patches and the backup policy are yours.

That's the real dividing line between a $12 virtual server and a $29.99 managed plan. Not CPU, not disk. Who gets paged when a library has a CVE.

## When you shouldn't buy a cloud server

A single small site with modest traffic belongs on shared hosting. It's the cheapest option, the provider handles the stack, and the resource ceiling on one server won't bind. Moving that site to a virtual server buys you root access and a patching schedule you now own.

Dedicated hardware is for workloads that must not share resources with anyone: large databases, compliance-sensitive environments, applications whose licensing is tied to physical cores. It also puts your availability in the hands of one machine, and scaling means migrating to a bigger box rather than turning a dial.

Serverless fits traffic that spikes and drops, or a team with no interest in configuring infrastructure. Event-driven billing means an idle application costs nothing, and the provider handles the operating system underneath.

A flat-rate virtual server fits the wide middle: predictable monthly spend, root access, full control over the stack, and a resource ceiling you can see and price out in advance.

## FAQ

**Does serverless charging stop when the app is idle?**
Yes. Serverless cloud hosting bills only for compute time consumed, and AWS Lambda is described as charging for the compute time you use. An application that receives no requests that hour costs nothing for that hour.

**Can I pay month to month?**
SpinServers lists its KVM plans at monthly rates with no term stated on the listing. AWS leases virtual cloud servers on rolling monthly subscriptions. Hostinger's advertised $7.99–$29.99 figures are the monthly equivalent of a 48-month plan, so if monthly cash flow matters, check which of the three you're looking at.

**What happens when the physical host dies?**
On a single VPS, the VM goes down with the host machine; the provider has to bring that node back or migrate the instance. On a distributed cloud network, workloads can shift between nodes. On dedicated hardware, you're waiting for that specific server to be repaired.

**Are CDN and load balancing included?**
They're separate technologies, and AWS lists Elastic Load Balancing as its own compute service alongside a content delivery network. Neither appears in the plan features for SpinServers' KVM virtual servers, so if you need them, price them as separate line items.

## Picking a plan

Match the form to the workload first. A single site or app with steady traffic → a fixed-capacity virtual server, and the KVM 2vCPU 2GB at $12.00/month covers most of them. Something with a database, a queue worker and a build step on the same host → 4 vCPU / 4 GB at $29.00/month. Traffic that spikes unpredictably → serverless, accepting that you give up root access in exchange for zero idle cost. A workload that legally or technically cannot share hardware → dedicated, starting at $79.00/month for a 4-core, 32 GB machine with 30 TB of transfer.

Two things to confirm before you pay. First, the billing term and the renewal price, in writing, because a monthly equivalent of a 48-month plan is not a monthly rate. Second, whether backups are included or billed separately, and what a restore costs when you need one at 2 a.m.

👉 [Compare the SpinServers KVM and dedicated configurations at their listed monthly rates](https://bit.ly/Spinservers)
