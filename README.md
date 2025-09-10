# Mạng máy tính: Kiến trúc và giao thức

Bản dịch đã được hoàn thiện (Đội ơn Gemini, ChatGPT, MS Copilot, Grok, AIStudio...), nhưng mà vẫn chưa soát lại hết (+ lọc khá nhiều chỗ vẫn chưa hay).

## Mục lục

### Introduction

- [Giới thiệu về Internet](intro/intro.md)
- [Các Layer của Internet](intro/layers.md)
- [Headers](intro/headers.md)
- [Kiến trúc mạng](intro/architecture.md)
- [Designing Resource Sharing](intro/sharing-resources.md)
- [Links](intro/links.md)

### Routing

- [Introduction to Routing](routing/intro.md)
- [Model for Intra-Domain Routing](routing/model.md)
- [Routing States](routing/solutions.md)
- [Distance-Vector Protocols](routing/distance-vector.md)
- [Link-State Protocols](routing/link-state.md)
- [Addressing](routing/addressing.md)
- [Router Hardware](routing/router.md)
- [Model for Inter-Domain Routing](routing/autonomous-systems.md)
- [Border Gateway Protocol (BGP)](routing/bgp.md)
- [BGP Implementation and Issues](routing/bgp-implementation.md)
- [IP Header](routing/ip-header.md)

### Transport

- [Transport Layer Principles](transport/reliability.md)
- [TCP Design](transport/tcp-design.md)
- [TCP Implementation](transport/tcp-implementation.md)
- [Congestion Control Principles](transport/cc-principles.md)
- [Congestion Control Design](transport/cc-design.md)
- [Congestion Control Implementation](transport/cc-implementation.md)
- [TCP Throughput Model](transport/throughput-model.md)
- [Congestion Control Issues](transport/cc-issues.md)
- [Router-Assisted Congestion Control](transport/router-based-cc.md)

### Applications

- [DNS](applications/dns.md)
- [HTTP](applications/http.md)

### End-to-End

- [Ethernet](end-to-end/ethernet.md)
- [Layer 2 Routing (STP)](end-to-end/l2-routing.md)
- [ARP: Connecting Layers 2 and 3](end-to-end/arp.md)
- [DHCP: Joining Networks](end-to-end/dhcp.md)
- [NAT: Network Address Translation](end-to-end/nat.md)
- [TLS: Secure Bytestreams](end-to-end/tls.md)
- [End-to-End Connectivity](end-to-end/end-to-end.md)

### Datacenters

- [Topologies](datacenter/topology.md)
- [Congestion Control](datacenter/datacenter-cc.md)
- [Routing](datacenter/datacenter-routing.md)
- [Addressing](datacenter/datacenter-addressing.md)
- [Virtualization](datacenter/virtualization.md)
- [Software-Defined Networking](datacenter/sdn.md)
- [Host Networking](datacenter/host-networking.md)

### Beyond Client-Server

- [Multicast](beyond-client-server/intro.md)
- [IP Multicast](beyond-client-server/ip-multicast-service-model.md)
- [DVMRP](beyond-client-server/dvmrp.md)
- [Core-Based Trees](beyond-client-server/cbt.md)
- [IP Multicast Challenges](beyond-client-server/ip-multicast-challenges.md)
- [Overlay Multicast](beyond-client-server/overlay-multicast.md)
- [Collective Operations](beyond-client-server/collective-operations.md)
- [Collective Implementations](beyond-client-server/collective-implementations.md)

### Wireless

- [Wireless Links](wireless/wireless-links.md)
- [Cellular](wireless/cellular.md)

### Glossary

- [Glossary](glossary.md)

## Phần mở đầu gốc

_By [Peyrin Kao](https://peyrin.github.io), based on lectures by [Sylvia Ratnasamy](https://www2.eecs.berkeley.edu/Faculty/Homepages/ratnasamy.html), [Rob Shakir](https://rob.sh/), and others._

These are the course notes for [CS 168: Introduction to the Internet](https://cs168.io/) at [UC Berkeley](https://eecs.berkeley.edu/).

Here is the official course description:

<p class="blue">
This course is an introduction to the Internet architecture. We will focus on the concepts and fundamental design principles that have contributed to the Internet's scalability and robustness and survey the various protocols and algorithms used within this architecture. Topics include layering, addressing, intradomain routing, interdomain routing, reliable delivery, congestion control, and the core protocols (e.g., TCP, UDP, IP, DNS, and HTTP) and network technologies (e.g., Ethernet, wireless).
</p>

## Disclaimer: Beta

These notes have not been proofread. They likely contain errors.

If you're a CS 168 student at Berkeley, in any case of dispute, the official course lectures are the correct source of truth.

## Diagrams

[Slideshow versions of these notes with diagrams are available here.](https://drive.google.com/drive/folders/13RnAGH1OrsOVvXdmQC73WkmoVD9r5lzd)

## PDF Version

[These notes are available as a PDF here.](https://drive.google.com/file/d/1PPSkHOnFsOI9noWWMuJnaxmsOzM6RIKX/view?usp=sharing)

The PDF version is not always up-to-date. It was last updated in November 2024.

## Corrections

As of the Fall 2024 semester, this textbook is still being actively maintained and updated.

If you see any parts that needs to be corrected, please open a Github issue [here](https://github.com/berkeley-cs168/textbook/issues).

## Source and Changelog

The source for the textbook and a log of all changes is [available on Github](https://github.com/berkeley-cs168/textbook).

## License

<a rel="license" href="http://creativecommons.org/licenses/by-sa/4.0/"><img alt="Creative Commons License" style="border-width:0" src="https://i.creativecommons.org/l/by-sa/4.0/88x31.png" /></a><br />This <span xmlns:dct="http://purl.org/dc/terms/" href="http://purl.org/dc/dcmitype/Text" rel="dct:type">work</span> is licensed under a <a rel="license" href="http://creativecommons.org/licenses/by-sa/4.0/">Creative Commons Attribution-ShareAlike 4.0 International License</a>.
