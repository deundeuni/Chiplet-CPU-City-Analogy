> 본 문서는 개념 비유 정리이며, 규격·수치는 예시이다. 선행기술 개시 문서가 아니다.
> 본 문서의 한국어 원문이 기준 원본이며, 번역본은 참고용입니다.
> This document is a conceptual analogy summary; specifications and numerical values are examples. It is not a prior art disclosure document.
> The Korean text is the authoritative reference; the English version is provided for reference only.

English | [한국어](./README.ko.md)

# Chiplet CPU Architecture Urban Planning Analogy Summary

- File name: README.md
- Repository: Chiplet-CPU-City-Analogy
- Author/Architect: deundeuni
- License: Creative Commons Attribution 4.0 International (CC BY 4.0)
- Version: v1.2
- Revision history:
  - v1.2 - Added Item 20 (Co-Development of Jobs and Infrastructure, designer's inference)
  - v1.1 - Added Item 19 (Expansion from Chiplet to System) and organized reference mapping numbers
  - v1.0 - Initial release

---

## Overview

This document is a conceptual analogy document prepared to intuitively understand the internal architecture, data flows, and inter-component dynamics of highly integrated semiconductors (CPU/APU) from the perspective of urban planning.

- Monolithic Architecture — A structure in which all compute cores, caches, and I/Os are integrated on a single silicon die, corresponding to the analogy of a naturally developed city.
- Chiplet / MCM Architecture — A structure in which dies are divided by function, manufactured separately, and combined via high-density packaging, corresponding to the analogy of a master-planned city divided by intended land use.

This document is a personal concept formulated by an individual designer who has not specialized in either semiconductors or urban planning, framing chiplet design through everyday impressions of how new towns and their living infrastructure develop over time. The technical descriptions reference publicly available materials and do not constitute an official document of any specific company, institution, or standards organization.

---

## Urban Planning Analogies by Major Architectural Category

### 1. Chip Manufacturing Shape and Circular Wafers
Due to the constraints of straight-line dicing processes, individual chips are generally manufactured in rectangular shapes. The loss rate at the perimeter of a circular wafer varies depending on chip size; larger monolithic chips carry a greater risk of edge waste and defects. (System on Wafer (SoW) is a specialized approach whose primary goal is not the reduction of perimeter waste, but rather connecting an entire wafer as a single system to secure bandwidth and integration.)

### 2. Memory Hierarchy and Latency Structure
- L1/L2 Cache: Private workbenches or precision lockers closely located inside the core.
- L3 Cache: Unlike inner-core caches (L1/L2), an area shared among nearby cores located in close proximity—functioning as a local logistics hub.
- External DRAM: Large logistics warehouses located on the outskirts of the city, where data access can incur latencies of several tens of nanoseconds or more.
- Memory Controller: While typically placed on the perimeter, designs also exist where it is closely positioned near the cores according to performance optimization goals.

### 3. Interconnect Tollgates and Bottlenecks
Die boundaries and bus entryways are analogous to logistics checkpoints and tollgates. Data bottlenecks concentrate at tollgate sections due to three main reasons: signal noise, physical pin count (road width) constraints, and localized thermal bottlenecks.

### 4. Central Control and City Hall Organization (P-Core / E-Core / NPU / Scheduler)
Like a city hall organization chart that oversees municipal administration, high-performance P-Cores (key administrators), high-efficiency E-Cores (working administrators), and AI-dedicated NPUs (specialized departments) divide roles, while the job scheduler dynamically controls task assignments across the entire city.

### 5. Intelligent In-Memory Computing (HBM-PIM)
An intelligent logistics center structure aimed at reducing traffic congestion and power consumption caused by data movement by mounting Processing-In-Memory (PIM) modules capable of self-sorting and processing inside memory warehouses (HBM) beyond mere storage. (Proof-of-concept and limited application stage)

### 6. On-Chip NoC and Die-to-Die Interconnect Structures
- Mesh structures correspond to intra-city subway networks, and Ring Bus is a lightweight variant thereof (see 6.5). Both belong to the category of On-Chip Network-on-Chip (NoC) within a single die.
- On the other hand, Infinity Fabric (AMD proprietary standard) and UCIe (Universal Chiplet Interconnect Express, an open-standard road network) are die-to-die interconnect standards, differing in physical and logical layers from on-chip NoC.
- Direct transfers (Bypass) during internal signal movement correspond to taxis, while shared bus schemes (legacy) correspond to shared buses.
- Furthermore, depending on design objectives, there are designs that operate On-Chip Networks (NoCs) separately for data, instruction, and control signals.

#### 6.5. Ring Bus
Ring Bus is a lightweight, low-cost variant of the subway network (Mesh NoC). It has a simple structure like small shared cars or express courier routes, making it useful for small-to-medium core configurations, but it carries a structural limitation where average hop count and latency increase as the number of nodes grows.

#### 6.6. DMA and Auxiliary Data Transfer Structures
Direct Memory Access (DMA) structures acting as mail carriers are utilized to reduce direct involvement of compute cores (performing primary tasks) during large data transfers, and DMA structures supporting chiplet-to-chiplet transfers also exist. This is conceptually linked to Remote Direct Memory Access (RDMA) frameworks.

### 7. Interposer and CXL-Based Resource Sharing
An interposer, which physically and electrically connects separated chiplets underneath, acts as the building lot site (foundational ground) supporting above-ground buildings (chiplets) and embedding high-density wiring networks underground. Furthermore, combining Compute Express Link (CXL) protocols enables flexible sharing and expansion of memory resources across multiple cities.

### 8. Shared Infrastructure and Composable Architecture
Similar to public infrastructure facilities shared by the entire city, this is a dynamic resource re-configuration architecture that pools compute, memory, and I/O resources and dynamically allocates and reassigns them as needed.

### 9. Backside Power Delivery Network (BSPDN / PowerVia)
A technology that moves power wiring to the backside of the die to eliminate contention with signal wiring. Prior implementation examples like Intel PowerVia exist, and major foundry technologies such as TSMC BSPDN can be viewed as being in the adoption/planned stage.

### 10. Sewage, Drainage, and Thermal Management Systems (Thermal Management)
Heat sinks, heat pipes, and liquid cooling designed to dissipate heat from high-performance cores are analogous to city sewage, drainage, and climate control (heat island prevention) systems. Next-generation microfluidic direct cooling technology is effective, but carries practical limits as it is currently in the research and prototype stage.

### 11. High-Rise Architecture and 3D V-Cache
A high-rise building construction method to overcome the limits of planar urban expansion, directly corresponding to 3D V-Cache technology that vertically stacks L3 cache dies on top of compute cores. However, 3D stacking can affect thermal dissipation and yields.

### 12. Land Value Differentiation and Process Heterogeneous Integration
Just as cities utilize land value differentials between downtown (high-cost land) and outskirts (low-cost land), compute cores with high scaling efficiency utilize cutting-edge advanced nodes, while I/O controllers with low area-reduction benefits mix relatively mature nodes (e.g., 6nm, numbers for illustrative purposes) to optimize the cost-to-performance ratio.

### 13. Known Good Die (KGD) Inspection System
Analogous to a quality assurance process that strictly inspects component dies in advance to ensure normal operation before constructing a master-planned assembly city.

### 14. Clock Tower and Clock Distribution Network (Clock Tree / CDC)
A clock distribution network corresponding to a central clock tower that controls operational time differences across the city. Clock Domain Crossing (CDC) synchronization devices operate to prevent signal instability (metastability) when crossing between different clock tower zones.

### 15. Emergency Disaster Monitoring and Security (RAS / TEE)
ECC and bad-core disabling systems (RAS) that detect and correct bit-flip errors during transmission correspond to municipal firefighting and disaster recovery systems, while hardware security isolation areas (TEE) correspond to access-controlled zones. The RAS/security concept in this section belongs to the same family as those in the Chiplet-APU White Paper and Modular Survival Architecture (ARCHITECTURE_STRATEGY) document, and is connected to both documents.

### 16. Optical Interconnect (CPO)
Co-Packaged Optics (CPO) technology, which uses light (photons) instead of electrical signals to transmit data, is analogous to dedicated airports and regional high-speed transit networks for long-distance, high-speed travel.

### 17. NUMA Local Administrative Ordinances and Adjacent Logistics
A mechanism that assigns each core zone to prioritize access to its nearest memory node, analogous to local administrative ordinances per city district and the principle of prioritizing adjacent logistics centers.

### 18. Station-Area Development and Hub-Centric Placement
New towns or redevelopment areas generally develop around train stations or on vacant lots near them, with municipal infrastructure like roads, power, and water connecting to and expanding from those hubs. Similarly, in chiplet architectures, there are configurations that position and connect compute chiplets and memories around interconnect hubs such as I/O dies or fabric switches, analogous to station-area development. (This is an analogy, and actual placement varies by design.)

### 19. Expansion from Chiplet to System (Connecting Old and New Districts)
This document mainly focuses on the inside of the chiplet package (new-district complex), and this item is a conceptual expansion to the entire system outside the package. As it is not directly within the main scope, only a rough correspondence is presented. Just as a new city must be connected to the existing city center via roads, railways, and communications, a modern chiplet package (new district) is also compatible with and connected to devices of legacy standards (old district). (This is an analogy, and actual configurations vary by system.)
- Motherboard: The foundational ground and arterial road network of the entire city connecting complexes and districts. (Item 7 Interposer corresponds to the internal ground within a complex)
- CPU: The main municipal hall complex of the new city center (Item 4).
- GPU: A separately established large specialized industrial park. It has its own logistics warehouse (VRAM, etc.) and connects to the main municipal hall via a high-speed arterial road (PCIe).
- RAM: Large logistics warehouses located on the outskirts (Item 2).
- SSD: Regional storage center.
- Network: Regional road and postal network connecting to neighboring cities.
- Bluetooth: Short-range alley communication network.
- Monitor/Printer: Display board showing city status, and external print shop outputting deliverables.
- External Ports (USB, etc.): Gateway ports for devices outside the city to enter and exit.
- Server: A neighboring metropolis connected via network. (Conceptually linked to 6.6 RDMA and Item 7 CXL)

### 20. Co-Development of Jobs and Infrastructure (Designer's Inference)
When jobs (factories, business facilities) appear in a new town, infrastructure such as roads, residential districts, city hall, water and sewage, transit, and convenience facilities is developed alongside them, and it is the designer's observation that their scale tends to be set not by everyday usage but by peak demand, such as commuting hours or periods of concentrated logistics. From this, the designer infers that in chiplets as well, when compute workloads (jobs) arise, infrastructure such as interconnect, power delivery, cooling, and cache for handling that traffic will be configured around peak load. (This is the designer's personal inference, not a verified fact. Actual design criteria vary by product, cost, and objectives, and are not necessarily based on maximum values.)

---

## Related Technologies and Reference Materials

> This section lists public standards and references related to the conceptual analogies for informational purposes, and does not constitute prior art or patent validity determination material. Versions reflect the time of writing and may be revised hereafter.

**Standards and Specifications**
- PCI Express Base Specification (PCI-SIG) — Base standard for CXL and UCIe (Items 6, 7, 19)
- Compute Express Link (CXL) Specification (CXL Consortium) — Memory pooling and sharing (Items 7, 8, 19)
- UCIe Specification (UCIe Consortium) — PCIe/CXL-based die-to-die interconnect (Items 6, 7)
- Bunch of Wires (BoW) (OCP ODSA) — Open die-to-die interface preceding UCIe (Item 6)
- AMBA CHI Chip-to-Chip (Arm) — Chip-to-chip coherent interconnect protocol (Item 6)
- JESD270-4 High Bandwidth Memory (HBM4) (JEDEC) — In-package stacked memory (Item 5)
- IEEE Std 1838-2019 (IEEE) — Test access architecture for 3D stacked ICs, related to KGD (Item 13)

**Literature**
- Naffziger, S. et al., "Pioneering Chiplet Technology and Design for the AMD EPYC and Ryzen Processor Families: Industrial Product," ISCA 2021, pp. 57-70 — Chiplet adoption background, yield, cost, heterogeneous nodes (Items 1, 12)
- Dally, W. J., & Towles, B. (2004) Principles and Practices of Interconnection Networks (Morgan Kaufmann) — General NoC (Item 6)
- Heterogeneous Integration Roadmap (IEEE EPS, SEMI, etc., 2019~) — Industry roadmap for heterogeneous integration (Item 12)

---

## Acknowledgments

The conceptual analogies and structural summaries presented in this document are deeply grounded in the contributions of numerous pioneering designers, scholars, industrial researchers who opened the field of ultra-high-density semiconductors and computer architecture, as well as technical documentation writers who systematically refined and shared complex semiconductor knowledge.

We express our deep respect and gratitude to the researchers at major academic societies such as ISCA and IEEE who established the academic and technical foundations of NoC, chiplets, heterogeneous integration, advanced packaging, and memory interconnects; to all experts who contributed to global technology standardization including UCIe, CXL, and JEDEC; and to document consolidators who clearly organized and conveyed relevant knowledge for the public and future generations.

---

## Notice & Disclaimer

- **Modesty Declaration**: The analogies and structural classifications in this document are intended for conceptual understanding; actual design and manufacturing implementations may vary depending on processes, tools, and product requirements. Similar explanations may have already been made by other researchers or materials, and this document asserts no exclusive rights.
- **AS-IS Provision**: The contents of this document are provided as-is, without warranty regarding completeness, fitness for a particular purpose, or absence of errors. Verification by experts is required for actual design and implementation.
- **Unintentional Omission**: Unintentional omissions, typos, or narrative omissions may exist and may be supplemented through future revisions.
- **Limits of Analogy**: Analogies are tools used to explain structures and do not fully represent all details of physical and electronic semiconductor behavior.
- **Personal Concept**: This document was formulated by an individual designer who is a non-expert in both semiconductors and urban planning, framing chiplet design through everyday impressions of how new towns and living infrastructure develop over time. Content regarding cities is not based on specific cases or sources, nor is it an accurate definition or case analysis of urban planning. It is not an official commentary on product specifications, industry practices, or urban planning, and as a non-expert perspective in both fields, technical and terminological inaccuracies may exist. Mentioned company and specification names are for factual reference only and imply no affiliation or endorsement.
- **Designer and Tools**: Problem formulation, analogy system establishment, structural classification, and final approval were performed by the designer (deundeuni). General-purpose generative AI tools were used during the writing process for text refinement, structuring, and review assistance as auxiliary tools only.

---

## Related Document Links

- Chiplet-APU Survival Architecture (`ARCHITECTURE_STRATEGY`, Separate Repository / Defensive Publication Document) — A defensive publication document distinct from this introductory analogy commentary
