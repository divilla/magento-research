# AWS Marketplace: top 100 AMI products by public marketplace order

Research snapshot: **2026-08-07 03:23 UTC**. Catalog size at retrieval: **7,177 AMI listings**.

## Important limitation

AWS Marketplace does **not** publish product sales, revenue, instance counts, active users, or a “best selling” sort. Its public Discovery search supports relevance and customer-rating sorts, but not sales. Consequently, this is the closest reproducible public answer: the first 100 products in the [live AWS Marketplace AMI browse results](https://aws.amazon.com/marketplace/search/results?FULFILLMENT_OPTION_TYPE=AMAZON_MACHINE_IMAGE&filters=FULFILLMENT_OPTION_TYPE), using AWS's own `RELEVANT` descending order.

This order should be read as **marketplace visibility / AWS relevance**, not audited unit sales. Reviews are included as a secondary signal only; AWS can share reviews across related listing families, so review totals are not a reliable sales rank either. See the official [SearchListings API reference](https://docs.aws.amazon.com/marketplace/latest/APIReference/API_marketplace-discovery_SearchListings.html) and [AWS Marketplace ratings and reviews guidance](https://docs.aws.amazon.com/marketplace/latest/userguide/product-marketing.html).

## What the top 100 says about the market

- **Security dominates the premium positions.** The first 18 results are mostly Fortinet and Palo Alto firewalls, WAF, management, logging, sandboxing, and hardened images.
- **The catalog rewards deployment primitives.** Hardened OS images, Linux/Windows distributions, Docker, databases, and networking appliances dominate; only two WordPress images appear, at ranks 43 and 62.
- **Pricing is overwhelmingly consumption-oriented.** 81 listings expose PAYG plus an annual option, 1 is PAYG-only, 17 are BYOL, and 1 is free.
- **Low or zero Marketplace software fees are common.** 45 listings start at `$0.00/hr` in seller software fees, but EC2 and other AWS charges still apply. Another 17 are BYOL and require a separately acquired license.
- **Paid security carries meaningful hourly prices.** Visible examples range from `$0.35/hr` for Cisco ASA and `$0.36/hr` for FortiGate to `$1.35/hr` for a Palo Alto bundle; FortiSandbox varies from `$2.44–$32.99/hr` by dimension/instance.
- **Visibility is concentrated.** Supported Images has 40 of the 100 positions, CIS 21, Fortinet 21, Palo Alto 10, Cisco 4, ProComputers 3, and Canonical 1. This is evidence of search-position concentration—not vendor sales share.

## Pricing interpretation

- **PAYG**: seller software is metered, normally per instance-hour; `PAYG + annual` means an annual/upfront option is also advertised.
- **BYOL**: bring your own license—no hourly Marketplace software fee is shown, but an external vendor license is required.
- **Price/hour** is the public *starting seller software price* or range returned by AWS. It excludes EC2, storage, data transfer, and other AWS infrastructure charges. `$0.00/hr` therefore does not mean the deployment costs nothing. AWS documents these distinctions in [AMI product pricing](https://docs.aws.amazon.com/marketplace/latest/userguide/pricing-ami-products.html).

## Top 100

| Rank | Product | Vendor | Model | Starting seller price/hour | AWS reviews | Rating |
|---:|---|---|---|---:|---:|---:|
| 1 | [Fortinet FortiGate VM Next-Generation Firewall](https://aws.amazon.com/marketplace/pp/prodview-wory773oau6wq) | Fortinet Inc. | PAYG + annual | $0.36/hr | 47 | 3.9 |
| 2 | [VM-Series Next-Gen Virtual Firewall w/ Advanced Security Subs (PAYG)](https://aws.amazon.com/marketplace/pp/prodview-3xtziatyes54i) | Palo Alto Networks | PAYG + annual | $1.35/hr | 13 | 4.4 |
| 3 | [Fortinet FortiWeb Web Application Firewall WAF (PAYG)](https://aws.amazon.com/marketplace/pp/prodview-hi4pzmnlcgpy4) | Fortinet Inc. | PAYG + annual | $0.96/hr | 8 | 3.8 |
| 4 | [FortiGate Next-Generation Firewall (ARM64/Graviton)](https://aws.amazon.com/marketplace/pp/prodview-ohcnwr7nr2icy) | Fortinet Inc. | PAYG + annual | $0.36/hr | 28 | 4.3 |
| 5 | [VM-Series Next-Gen Virtual Firewall w/Advanced Threat Prevention (PAYG)](https://aws.amazon.com/marketplace/pp/prodview-mn63yjbq37n4c) | Palo Alto Networks | PAYG + annual | $0.99/hr | 14 | 4.1 |
| 6 | [Fortinet FortiGate (BYOL) Next-Generation Firewall](https://aws.amazon.com/marketplace/pp/prodview-lvfwuztjwe5b2) | Fortinet Inc. | BYOL | external license | 16 | 4.5 |
| 7 | [VM-Series Virtual Next-Generation Firewall (BYOL)](https://aws.amazon.com/marketplace/pp/prodview-ccntnbzdod74k) | Palo Alto Networks | BYOL | external license | 20 | 3.7 |
| 8 | [Palo Alto Networks Panorama](https://aws.amazon.com/marketplace/pp/prodview-cjgnbhu6bozno) | Palo Alto Networks | BYOL | external license | 4 | 4.3 |
| 9 | [Fortinet FortiAnalyzer (BYOL) Centralized Security Logging and Reporting](https://aws.amazon.com/marketplace/pp/prodview-6dt7z5twj7t7a) | Fortinet Inc. | BYOL | external license | 0 | — |
| 10 | [Fortinet FortiManager (BYOL) Centralized Security Management](https://aws.amazon.com/marketplace/pp/prodview-l6rxheua5mbls) | Fortinet Inc. | BYOL | external license | 0 | — |
| 11 | [Fortinet FortiSandbox Zero-Day Threat Protection (On-Demand)](https://aws.amazon.com/marketplace/pp/prodview-xzckvcfxaxga2) | Fortinet Inc. | PAYG | $2.44–$32.99/hr | 3 | 4.0 |
| 12 | [CIS Hardened Image Level 1 on Microsoft Windows Server 2022](https://aws.amazon.com/marketplace/pp/prodview-qzirg5jhzmmf6) | Center for Internet Security | PAYG + annual | $0.02/hr | 4 | 4.4 |
| 13 | [Fortinet FortiGate (BYOL) Next-Generation Firewall (ARM64/Graviton)](https://aws.amazon.com/marketplace/pp/prodview-ccnrlwz74uwgk) | Fortinet Inc. | BYOL | external license | 14 | 4.5 |
| 14 | [FortiManager Centralized Security Management (Max 10 managed devices)](https://aws.amazon.com/marketplace/pp/prodview-4rgupihrc4lgq) | Fortinet Inc. | PAYG + annual | $0.54/hr | 3 | 3.8 |
| 15 | [CIS Hardened Image Level 1 on Microsoft Windows Server 2019](https://aws.amazon.com/marketplace/pp/prodview-ikkh3uo3l4zhw) | Center for Internet Security | PAYG + annual | $0.02/hr | 4 | 4.4 |
| 16 | [CIS Hardened Image Level 1 on Amazon Linux 2023](https://aws.amazon.com/marketplace/pp/prodview-fqqp6ebucarnm) | Center for Internet Security | PAYG + annual | $0.02/hr | 46 | 4.3 |
| 17 | [AI Runtime Security](https://aws.amazon.com/marketplace/pp/prodview-pasyge5z56oiw) | Palo Alto Networks | BYOL | external license | 0 | — |
| 18 | [Fortinet FortiAuthenticator (BYOL)](https://aws.amazon.com/marketplace/pp/prodview-ciradouxpsbca) | Fortinet Inc. | BYOL | external license | 1 | 4.5 |
| 19 | [Oracle Linux 8 — Support by SupportedImages](https://aws.amazon.com/marketplace/pp/prodview-uddeiwhf2l26w) | Supported Images | PAYG + annual | $0.00/hr | 5 | 4.2 |
| 20 | [CIS Hardened Image Level 1 on Ubuntu Linux Server 22.04 LTS](https://aws.amazon.com/marketplace/pp/prodview-7afxz7ijttzk4) | Center for Internet Security | PAYG + annual | $0.02/hr | 8 | 3.9 |
| 21 | [Fortinet FortiSIEM-VM (BYOL) - Security Information and Event Management](https://aws.amazon.com/marketplace/pp/prodview-6rqkoxup67mhq) | Fortinet Inc. | BYOL | external license | 0 | — |
| 22 | [FortiMail Secure Email Gateway](https://aws.amazon.com/marketplace/pp/prodview-bu7twvmq4q5v6) | Fortinet Inc. | BYOL | external license | 0 | — |
| 23 | [CIS Hardened Image Level 1 on Red Hat Enterprise Linux 8](https://aws.amazon.com/marketplace/pp/prodview-kg7ijztdpvfaw) | Center for Internet Security | PAYG + annual | $0.02/hr | 131 | 4.4 |
| 24 | [Fortinet FortiWeb Web Application Firewall WAF VM (BYOL)](https://aws.amazon.com/marketplace/pp/prodview-veogyjjtq5uvq) | Fortinet Inc. | BYOL | external license | 0 | — |
| 25 | [Ubuntu 22 (Ubuntu 22.04 LTS) — Support by SupportedImages](https://aws.amazon.com/marketplace/pp/prodview-cs32nfwh3hkvi) | Supported Images | PAYG + annual | $0.00/hr | 6 | 4.4 |
| 26 | [Fortinet FortiAnalyzer (PAYG) Centralized Logging/Reporting](https://aws.amazon.com/marketplace/pp/prodview-wy43e3tw4wm3e) | Fortinet Inc. | PAYG + annual | $0.54/hr | 5 | 4.0 |
| 27 | [CIS Hardened Image Level 1 on Red Hat Enterprise Linux 9](https://aws.amazon.com/marketplace/pp/prodview-6oyclaofcaa2g) | Center for Internet Security | PAYG + annual | $0.02/hr | 130 | 4.4 |
| 28 | [Oracle Linux 9 — Support by SupportedImages](https://aws.amazon.com/marketplace/pp/prodview-n5x4eougzrol6) | Supported Images | PAYG + annual | $0.00/hr | 5 | 4.2 |
| 29 | [CentOS 10 (centos 10) — Support by SupportedImages](https://aws.amazon.com/marketplace/pp/prodview-gducqo5toqumc) | Supported Images | PAYG + annual | $0.00/hr | 6 | 4.5 |
| 30 | [CentOS 10 — Support by SupportedImages](https://aws.amazon.com/marketplace/pp/prodview-tlabscjpjaocy) | Supported Images | PAYG + annual | $0.00/hr | 6 | 4.5 |
| 31 | [Ubuntu 26 — Support by SupportedImages](https://aws.amazon.com/marketplace/pp/prodview-5e266fdamfqsq) | Supported Images | PAYG + annual | $0.00/hr | 6 | 4.4 |
| 32 | [CentOS 9 (centos 9) — Support by SupportedImages](https://aws.amazon.com/marketplace/pp/prodview-j2th3juwkr5ry) | Supported Images | PAYG + annual | $0.00/hr | 6 | 4.5 |
| 33 | [Ubuntu 24.04 LTS (Ubuntu 24.04) — Support by SupportedImages](https://aws.amazon.com/marketplace/pp/prodview-jiqlsnos3bdxm) | Supported Images | PAYG + annual | $0.00/hr | 0 | — |
| 34 | [Windows Server 2022 (Windows Server 2022) — Support by SupportedImages](https://aws.amazon.com/marketplace/pp/prodview-pjmqz2ibfk6wm) | Supported Images | PAYG + annual | $0.00/hr | 4 | 4.4 |
| 35 | [Oracle Linux 10 — Support by SupportedImages](https://aws.amazon.com/marketplace/pp/prodview-cpyw7u7gmjrjg) | Supported Images | PAYG + annual | $0.00/hr | 5 | 4.2 |
| 36 | [CIS Hardened Image Level 1 on Ubuntu Linux Server 24.04 LTS](https://aws.amazon.com/marketplace/pp/prodview-6l5e56nst6r3g) | Center for Internet Security | PAYG + annual | $0.02/hr | 0 | — |
| 37 | [(Federal) VM-Series Virtual NextGen Firewall Bundle2 with 24x7 Support](https://aws.amazon.com/marketplace/pp/prodview-wsu46li6jw3je) | Palo Alto Networks | PAYG + annual | $1.06/hr | 12 | 4.3 |
| 38 | [Amazon Linux 2023 AMI (amazon linux 2023) — Support by SupportedImages](https://aws.amazon.com/marketplace/pp/prodview-ia3l7n7czmqsk) | Supported Images | PAYG + annual | $0.00/hr | 0 | — |
| 39 | [CIS Hardened Image Level 2 on Amazon Linux 2023](https://aws.amazon.com/marketplace/pp/prodview-uis4wvkb7g3wq) | Center for Internet Security | PAYG + annual | $0.02/hr | 46 | 4.3 |
| 40 | [ECS-Optimized Amazon Linux 2023 AMI (ecs) — Support by SupportedImages](https://aws.amazon.com/marketplace/pp/prodview-yu2ho7vqjrm7w) | Supported Images | PAYG + annual | $0.00/hr | 46 | 4.3 |
| 41 | [Red Hat Enterprise Linux 8 (redhat 8) — Support by SupportedImages](https://aws.amazon.com/marketplace/pp/prodview-crgmvspeg7yku) | Supported Images | PAYG + annual | $0.00/hr | 130 | 4.4 |
| 42 | [CIS Hardened Image Level 1 on Microsoft Windows Server 2016](https://aws.amazon.com/marketplace/pp/prodview-gtdqnprx5fr6g) | Center for Internet Security | PAYG + annual | $0.02/hr | 5 | 4.5 |
| 43 | [Wordpress on Ubuntu 26](https://aws.amazon.com/marketplace/pp/prodview-aqbhn643zghb2) | Supported Images | PAYG + annual | $0.00/hr | 4 | 3.5 |
| 44 | [FortiAnalyzer Centralized Logging/Reporting (2 managed devices)](https://aws.amazon.com/marketplace/pp/prodview-h2lf6do2y4y4g) | Fortinet Inc. | PAYG + annual | $0.01/hr | 5 | 4.0 |
| 45 | [Debian 13 (debian 13 x86_64) — Support by SupportedImages](https://aws.amazon.com/marketplace/pp/prodview-7bciw7mamgieo) | Supported Images | PAYG + annual | $0.00/hr | 11 | 4.3 |
| 46 | [Red Hat Enterprise Linux 10 (redhat 10) — Support by SupportedImages](https://aws.amazon.com/marketplace/pp/prodview-hspj7ypzpewow) | Supported Images | PAYG + annual | $0.00/hr | 130 | 4.4 |
| 47 | [Red Hat Enterprise Linux 9 (redhat 9) — Support by SupportedImages](https://aws.amazon.com/marketplace/pp/prodview-vvgm4hj6b7adw) | Supported Images | PAYG + annual | $0.00/hr | 130 | 4.4 |
| 48 | [Debian 12 (debian 12 x86_64) — Support by SupportedImages](https://aws.amazon.com/marketplace/pp/prodview-fhnwl3kkhercu) | Supported Images | PAYG + annual | $0.00/hr | 0 | — |
| 49 | [Windows Server 2019 (Windows Server 2019) — Support by SupportedImages](https://aws.amazon.com/marketplace/pp/prodview-ofzhts6hsibuk) | Supported Images | PAYG + annual | $0.00/hr | 4 | 4.4 |
| 50 | [Fortinet FortiManager (PAYG) Centralized Security Management](https://aws.amazon.com/marketplace/pp/prodview-jphf6k3dqwibw) | Fortinet Inc. | PAYG + annual | $0.54/hr | 0 | — |
| 51 | [Docker on Ubuntu 22.04 LTS](https://aws.amazon.com/marketplace/pp/prodview-46hx72bsta4dw) | Supported Images | PAYG + annual | $0.00/hr | 10 | 4.4 |
| 52 | [Amazon Linux 2 AMI (amazon linux 2) — Support by SupportedImages](https://aws.amazon.com/marketplace/pp/prodview-4us4yprgzaxks) | Supported Images | PAYG + annual | $0.00/hr | 46 | 4.3 |
| 53 | [Debian 11 (debian 11 x86_64) — Support by SupportedImages](https://aws.amazon.com/marketplace/pp/prodview-keyr3cdc5hmxk) | Supported Images | PAYG + annual | $0.00/hr | 11 | 4.3 |
| 54 | [CIS Hardened Image Level 2 on Microsoft Windows Server 2022](https://aws.amazon.com/marketplace/pp/prodview-lhbxwzmvsawbw) | Center for Internet Security | PAYG + annual | $0.02/hr | 4 | 4.4 |
| 55 | [CIS Hardened Image Level 1 on Microsoft Windows Server 2025](https://aws.amazon.com/marketplace/pp/prodview-okv4xiseyoaj4) | Center for Internet Security | PAYG + annual | $0.02/hr | 0 | — |
| 56 | [(Federal) VM-Series Virtual NextGen Firewall Bundle3 with 24x7 Support](https://aws.amazon.com/marketplace/pp/prodview-gfbcyenj6z75u) | Palo Alto Networks | PAYG + annual | $1.15/hr | 12 | 4.3 |
| 57 | [Docker on CentOS 10 (x86_64 docker)](https://aws.amazon.com/marketplace/pp/prodview-og4x5pw64ud62) | Supported Images | PAYG + annual | $0.00/hr | 8 | 4.4 |
| 58 | [Windows Server 2025 (Windows Server 2025) — Support by SupportedImages](https://aws.amazon.com/marketplace/pp/prodview-cnw74vouqzuyk) | Supported Images | PAYG + annual | $0.00/hr | 4 | 4.4 |
| 59 | [VM-Series Virtual NextGen Firewall for ARM - PAYG](https://aws.amazon.com/marketplace/pp/prodview-cjfzbdnaojqci) | Palo Alto Networks | PAYG + annual | $0.77/hr | 0 | — |
| 60 | [Docker on Amazon 2023](https://aws.amazon.com/marketplace/pp/prodview-gvyxq52kvfjgs) | Supported Images | PAYG + annual | $0.00/hr | 1 | 4.5 |
| 61 | [Ubuntu 26 (Ubuntu 26.04 LTS) — Support by SupportedImages](https://aws.amazon.com/marketplace/pp/prodview-sqbvczcapqjye) | Supported Images | PAYG + annual | $0.00/hr | 6 | 4.4 |
| 62 | [Wordpress on Amazon Linux 2023](https://aws.amazon.com/marketplace/pp/prodview-dyr3tpwqzhylw) | Supported Images | PAYG + annual | $0.00/hr | 13 | 4.1 |
| 63 | [CIS Hardened Image Level 2 on Microsoft Windows Server 2019](https://aws.amazon.com/marketplace/pp/prodview-mytoha3qyuk7y) | Center for Internet Security | PAYG + annual | $0.02/hr | 6 | 3.6 |
| 64 | [Cisco Secure Firewall ASA Virtual - PAYG](https://aws.amazon.com/marketplace/pp/prodview-k3dpkteh6bgzi) | Cisco Systems, Inc. | PAYG + annual | $0.35/hr | 33 | 3.3 |
| 65 | [CIS Hardened Image Level 1 on EKS-Optimized Amazon Linux 2023](https://aws.amazon.com/marketplace/pp/prodview-oyzfkxtyl3gyi) | Center for Internet Security | PAYG + annual | $0.02/hr | 0 | — |
| 66 | [VM-Series Virtual Next-Generation Firewall - ARM (BYOL)](https://aws.amazon.com/marketplace/pp/prodview-hlkjqryeioz4e) | Palo Alto Networks | BYOL | external license | 15 | 4.1 |
| 67 | [CIS Hardened Image Level 2 on Red Hat Enterprise Linux 9](https://aws.amazon.com/marketplace/pp/prodview-6axx7cl7vguti) | Center for Internet Security | PAYG + annual | $0.02/hr | 130 | 4.4 |
| 68 | [FortiNAC Secure Network Access Control - BYOL](https://aws.amazon.com/marketplace/pp/prodview-xomjztyuhmjvm) | Fortinet Inc. | BYOL | external license | 0 | — |
| 69 | [FortiClient EMS (BYOL)](https://aws.amazon.com/marketplace/pp/prodview-yoem7yylnxwtc) | Fortinet Inc. | BYOL | external license | 0 | — |
| 70 | [AlmaLinux 10 (Alma Linux 10) — Support by SupportedImages](https://aws.amazon.com/marketplace/pp/prodview-tsvy6tu2a743c) | Supported Images | PAYG + annual | $0.00/hr | 7 | 4.3 |
| 71 | [Amazon Linux 2023 AMI ARM64 — Support by SupportedImages](https://aws.amazon.com/marketplace/pp/prodview-llwcofq2fsafg) | Supported Images | PAYG + annual | $0.00/hr | 0 | — |
| 72 | [SQL Server 2022 Standard on Windows 2025 — Support by SupportedImages](https://aws.amazon.com/marketplace/pp/prodview-w7pxorue26fi6) | Supported Images | PAYG + annual | $0.00/hr | 4 | 4.4 |
| 73 | [FortiAnalyzer Centralized Logging/Reporting (10 managed devices)](https://aws.amazon.com/marketplace/pp/prodview-wabutfmgsmt4s) | Fortinet Inc. | PAYG + annual | $0.54/hr | 5 | 4.0 |
| 74 | [(Federal) VM-Series Virtual NextGen Firewall Bundle1 with 24x7 Support](https://aws.amazon.com/marketplace/pp/prodview-3lydqnb45pbsm) | Palo Alto Networks | PAYG + annual | $0.79/hr | 12 | 4.3 |
| 75 | [AlmaLinux 9 (Alma Linux 9) — Support by SupportedImages](https://aws.amazon.com/marketplace/pp/prodview-kblsqjv3iogvg) | Supported Images | PAYG + annual | $0.00/hr | 0 | — |
| 76 | [CIS Hardened Image Level 2 on Microsoft Windows Server 2025](https://aws.amazon.com/marketplace/pp/prodview-w2q7uq7vz73li) | Center for Internet Security | PAYG + annual | $0.02/hr | 0 | — |
| 77 | [PostgreSQL on Amazon Linux 2023](https://aws.amazon.com/marketplace/pp/prodview-zb6iig5c2z7zq) | Supported Images | PAYG + annual | $0.00/hr | 0 | — |
| 78 | [Fortinet FortiRecorder-VM Network Video Security](https://aws.amazon.com/marketplace/pp/prodview-27gp7fjrct4bm) | Fortinet Inc. | PAYG + annual | $0.00/hr | 0 | — |
| 79 | [Cisco Meraki vMX](https://aws.amazon.com/marketplace/pp/prodview-o5hpcs2rygxnk) | Cisco Systems, Inc. | BYOL | external license | 3 | 4.0 |
| 80 | [Fortinet-FortiSOAR-Enterprise (BYOL)](https://aws.amazon.com/marketplace/pp/prodview-ajgaysp4jbybq) | Fortinet Inc. | BYOL | external license | 0 | — |
| 81 | [CIS Hardened Image Level 1 on Amazon Linux 2023 GPU Optimized DLAMI](https://aws.amazon.com/marketplace/pp/prodview-6h4cjwmouqsmy) | Center for Internet Security | PAYG + annual | $0.02/hr | 0 | — |
| 82 | [CIS Hardened Image Level 1 on Amazon Linux 2023 (ARM)](https://aws.amazon.com/marketplace/pp/prodview-3fovewsamhmzm) | Center for Internet Security | PAYG + annual | $0.02/hr | 0 | — |
| 83 | [Cisco Catalyst 8000V for SD-WAN & Routing](https://aws.amazon.com/marketplace/pp/prodview-rohvq2cjd4ccg) | Cisco Systems, Inc. | BYOL | external license | 0 | — |
| 84 | [ECS-Optimized Amazon Linux 2 (ecs) — Support by SupportedImages](https://aws.amazon.com/marketplace/pp/prodview-4ftun222na2og) | Supported Images | PAYG + annual | $0.00/hr | 8 | 4.3 |
| 85 | [CIS Hardened Image Level 2 on Red Hat Enterprise Linux 8](https://aws.amazon.com/marketplace/pp/prodview-6ti3cuig7pl5u) | Center for Internet Security | PAYG + annual | $0.02/hr | 131 | 4.4 |
| 86 | [PostgreSQL on Ubuntu 24.04 LTS](https://aws.amazon.com/marketplace/pp/prodview-34vbk56swxjtm) | Supported Images | PAYG + annual | $0.00/hr | 11 | 4.2 |
| 87 | [Ubuntu 24.04 LTS (Ubuntu 24) (ARM) — Support by SupportedImages](https://aws.amazon.com/marketplace/pp/prodview-ckhhyq5ubgtus) | Supported Images | PAYG + annual | $0.00/hr | 0 | — |
| 88 | [CentOS 9 — Support by ProComputers](https://aws.amazon.com/marketplace/pp/prodview-smszvabbrawjm) | ProComputers | PAYG + annual | $0.00/hr | 6 | 4.5 |
| 89 | [CIS Hardened Image Level 1 on Amazon Linux 2023 Parallel Compute Service](https://aws.amazon.com/marketplace/pp/prodview-kvqikuru5ri4m) | Center for Internet Security | PAYG + annual | $0.02–$0.02/hr | 0 | — |
| 90 | [Cassandra (cassandra)](https://aws.amazon.com/marketplace/pp/prodview-a26ry34i3oywq) | Supported Images | PAYG + annual | $0.00/hr | 0 | — |
| 91 | [OpenJDK Java](https://aws.amazon.com/marketplace/pp/prodview-fudhqhhuatizi) | Supported Images | PAYG + annual | $0.00/hr | 11 | 4.4 |
| 92 | [Jenkins on CentOS 10](https://aws.amazon.com/marketplace/pp/prodview-qv2tobl7tijam) | Supported Images | PAYG + annual | $0.00/hr | 7 | 4.1 |
| 93 | [CIS Hardened Image STIG on Microsoft Windows Server 2022](https://aws.amazon.com/marketplace/pp/prodview-sgnc2dldqdeaw) | Center for Internet Security | PAYG + annual | $0.02/hr | 0 | — |
| 94 | [Cisco Secure Firewall Threat Defense Virtual - PAYG](https://aws.amazon.com/marketplace/pp/prodview-agotwrhawevmc) | Cisco Systems, Inc. | PAYG + annual | $1.00/hr | 16 | 4.0 |
| 95 | [Supabase on Ubuntu 24.04 LTS — Support by SupportedImages](https://aws.amazon.com/marketplace/pp/prodview-bolyo34t4sdn2) | Supported Images | PAYG + annual | $0.00/hr | 0 | — |
| 96 | [CIS Hardened Image Level 1 on ECS-Optimized Amazon Linux 2023](https://aws.amazon.com/marketplace/pp/prodview-o5zt4oulb7mk4) | Center for Internet Security | PAYG + annual | $0.02/hr | 0 | — |
| 97 | [Rocky Linux 9 (Rocky 9) — Support by ProComputers](https://aws.amazon.com/marketplace/pp/prodview-c755eecdjt7gs) | ProComputers | PAYG + annual | $0.00/hr | 7 | 4.3 |
| 98 | [Ubuntu 24 — Support by SupportedImages](https://aws.amazon.com/marketplace/pp/prodview-hy6xzebkwubo6) | Supported Images | PAYG + annual | $0.00/hr | 6 | 4.4 |
| 99 | [Ubuntu 22.04 LTS - Jammy](https://aws.amazon.com/marketplace/pp/prodview-f2if34z3a4e3i) | Canonical Group Limited | Free | $0.00/hr | 6 | 3.7 |
| 100 | [Red Hat Enterprise Linux 8 (RHEL 8) — Support by ProComputers](https://aws.amazon.com/marketplace/pp/prodview-7oheb6awjgi5k) | ProComputers | PAYG + annual | $0.00/hr | 130 | 4.4 |

## Bottom line for Magento / webshop positioning

The public AMI front page is primarily a **security, operating-system, and infrastructure appliance channel**. Webshop software has almost no visible presence: two generic WordPress images, no Magento, and no dedicated commerce platform in this top 100 snapshot. That supports the earlier conclusion: AWS Marketplace is most credible for a Magento offer when the product is framed as an **enterprise deployment appliance, managed commerce stack, security/compliance image, or procurement vehicle**—not as the main channel for merchants shopping for storefront software.

## Sources

- [Live AWS Marketplace AMI results](https://aws.amazon.com/marketplace/search/results?FULFILLMENT_OPTION_TYPE=AMAZON_MACHINE_IMAGE&filters=FULFILLMENT_OPTION_TYPE)
- [AWS Marketplace SearchListings API](https://docs.aws.amazon.com/marketplace/latest/APIReference/API_marketplace-discovery_SearchListings.html)
- [AWS Marketplace Discovery APIs](https://docs.aws.amazon.com/marketplace/latest/developerguide/discovery-apis.html)
- [AMI product pricing](https://docs.aws.amazon.com/marketplace/latest/userguide/pricing-ami-products.html)
- [Ratings, reviews, and product marketing](https://docs.aws.amazon.com/marketplace/latest/userguide/product-marketing.html)
