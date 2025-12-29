**Naivas Supermarket Enterprise Network**

A Deliberate, Redundant, and Production‑Minded Campus LAN Design


**Executive Summary**

This project models a realistic enterprise campus network for a supermarket environment, inspired by Naivas’ operational layout. The design goes beyond basic connectivity to emphasize determinism, resilience, and operational clarity — the qualities expected in production networks managed by NOC teams and enterprise engineers.

Rather than treating configuration as an end in itself, this lab demonstrates intentional design choices: where **routing** lives, how **loops** are controlled, why **redundancy** is structured the way it is, and how failure is anticipated rather than feared.


**Design Philosophy**

This network is built on three guiding principles:

**Role Separation** – Access switches forward; distribution switches decide.

**Predictability over cleverness** – One authoritative routing point, deterministic STP roots.

**Failure‑aware design** – Redundancy exists to be controlled, not to surprise operators.  


**Topology Overview**

**Logical Layers**

**Access layer**	[2960‑24TT (x2)]	Endpoint connectivity, VLAN membership

**Distribution layer**	[3560‑24PS, 2950T‑24]	STP control, aggregation, Layer‑3 boundary


**Device Roles**

Device	Model	Role

**Distribution‑SW0**	3560‑24PS	Primary Distribution & Routing Anchor

**Distribution‑SW1**	2950T‑24	Secondary Distribution & STP Backup

Access‑SW1	2960‑24TT	Access Layer
Access‑SW2	2960‑24TT	Access Layer


**Business‑Driven VLAN Segmentation**

Departments are mapped directly to network boundaries, reflecting how retail operations scale and troubleshoot in practice.

VLAN	Department	Subnet	Default Gateway
10	Warehouse	57.16.21.0/24	57.16.21.1
20	Bakery & Grocery	20.20.3.0/24	20.20.3.1
30	Server Room	137.10.12.0/24	137.10.12.1
40	Cashiers (POS)	150.14.34.0/24	150.14.34.1

**Design Intent**: Segmentation limits broadcast domains, isolates faults, and enables policy control as the network grows.


**Spanning Tree Strategy (Rapid PVST+)**

Why STP Still Matters

In redundant Layer‑2 designs, loops are not a theoretical risk — they are inevitable. STP is therefore treated not as a default feature, but as a controlled system with deliberate root placement.

**Root Bridge Placement**

VLANs	Root Primary	Root Secondary
10, 20, 30, 40	Distribution‑SW0	Distribution‑SW1

**Rationale**: The switch making Layer‑3 decisions must also be the Layer‑2 reference point. This avoids inefficient traffic paths and simplifies troubleshooting.

**Layer‑3 Boundary & Routing Design**

**Centralized Inter‑VLAN Routing**

All SVIs are intentionally centralized on Distribution‑SW0, establishing a single, authoritative routing boundary.

This avoids:

Multiple competing default gateways

Black‑holed traffic due to misaligned STP paths

Unclear fault domains during outages


**Closing Statement**

This project reflects how I approach networking: with intent, restraint, and respect for operational reality. I am not interested in fragile brilliance — I am interested in networks that survive growth, failure, and human error.

My goal is to contribute to environments where reliability is not a hope, but a design outcome.

AUTHOR - BRADLEY GIOVANNI  NETWORK ENGINEER  |  NETWORK ADMINISTRATOR  | NOC TECHNICIAN

[![LinkedIn](https://img.shields.io/badge/LinkedIn-Connect-blue?style=for-the-badge&logo=linkedin)](https://www.linkedin.com/in/bradley-giovanniii293)
---
