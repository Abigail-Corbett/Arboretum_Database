# Arboretum_Database
---
## Project Overview
This project documents the end-to-end lifecycle of an Arboretum Database, moving from initial business rules and Entity-Relationship Modeling (ERM) to a fully normalized schema implemented in MySQL. The system tracks plants and their specific environmental requirements, including soil, climate, and size characteristics.

## Conceptual Design (ERM)
**The database was originally designed around the following Business Rules:**

Every plant is associated with exactly one soil type and one size category.

Every soil type and size category can support multiple plants.

Each climate is mapped to a specific soil type/location.

Solar exposure is dictated by the specific climate zone.

<img width="1080" height="418" alt="image" src="https://github.com/user-attachments/assets/39e464d4-db86-4d52-98e2-a8586d9c3aae" />

### Implementation of Relationships
For 1:M (One-to-Many) relationships, the parent table's Primary Key (PK) was implemented as a Foreign Key (FK) within the child table.

Example: The Climate table uses locationID as a Foreign Key. This allows multiple climate profiles to reference a single location without duplicating location data.

---

## Normalization & Schema Refinement
To ensure data integrity and reduce redundancy, the schema was refined to reach Third Normal Form (3NF).

### Modifications for 3NF
Table Splitting: The original SoilType table was split into two distinct entities: Location and Soil.

Justification: This removal of transitive dependencies ensures that non-key attributes (like specific soil composition) depend only on the primary key, satisfying 3NF requirements.

<img width="975" height="898" alt="image" src="https://github.com/user-attachments/assets/e6dfae42-16e2-4553-b3b4-889a08483131" />

---

## Documentation & Execution

### 1. Virtual Machine Provisioning
Successfully downloaded and created the two virtual machines.

<img width="566" height="314" alt="VirtualBox Manager View" src="https://github.com/user-attachments/assets/b96176e0-81f6-475f-b43b-f32c2ed36090" />

### 2. Environment Initialization
Initialized the Kali Linux 2025.4 virtual instance via Oracle VirtualBox, confirming the integrity of the virtual appliance import process. Utilized the `whoami` command to verify current user privileges and ensure that the shell environment was correctly initialized.

<img width="682" height="430" alt="Kali Terminal Verification" src="https://github.com/user-attachments/assets/393c9363-238f-4190-af1a-9d11be6c6239" />

> **Note:** By verifying the environment with a basic terminal command like `whoami`, I established a baseline for the system's state before moving into network reconnaissance. Operating within a Host-Only network ensures that all future testing is contained within a secure, private sandbox, preventing unauthorized traffic from reaching the Local Area Network (LAN).

### 3. Connectivity Testing
I successfully deployed the Metasploitable 2 node and utilized the `ifconfig` command to identify the target IP address within the local subnet. I then verified the connection between the two machines using the Kali Linux command:
`ping [target_ip_address]`

---

## Troubleshooting & Lab Maintenance

### **Issue: Dynamic Host Configuration Protocol (DHCP)**
* **Problem:** After moving the victim node from a NAT configuration to a Host-Only Adapter, the operating system kept the previous IP address, which prevented communication with the attacker node.
* **Solution:** Performed a manual DHCP renewal (forcing the computer to ask for new network info) using the following commands:
 ```bash
    sudo dhclient -r eth0
    sudo dhclient eth0
```
## Collaborative Evolution
The project benefited from peer review, resulting in the following technical improvements:

Visual Clarity: Added direction arrows and explicit PK/FK mapping to the ERM diagrams.

Granularity: Expanded attributes to include scientific naming and specific soil/climate metrics for better data retrieval.

---
## Future Optimization
To further increase database efficiency and reduce complexity, a proposed modification for Version 2.0 includes:

Entity Consolidation: Eliminate the Sun entity and migrate the sunAmt attribute directly into the Climate table.

Reasoning: Since sun exposure is logically dictated by climate patterns, this modification simplifies the schema and reduces the number of joins required for environmental queries without losing critical data.

## Tools & Technologies
Database: MySQL

Modeling: Microsoft Visio

---

## Author 
Abigail Corbett <br> 
April 15th, 2026
