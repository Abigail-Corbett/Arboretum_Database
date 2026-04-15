# Arboretum_Database
## Project Overview
This project documents the end-to-end lifecycle of an Arboretum Database, moving from initial business rules and Entity-Relationship Modeling (ERM) to a fully normalized schema implemented in MySQL. The system tracks plants and their specific environmental requirements, including soil, climate, and size characteristics. This was an assignment for a course in Database Concepts with multiple parts over the course of two weeks. 

## Conceptual Design (ERM)
**The database was originally designed around the following Business Rules:**

Every plant is associated with exactly one soil type and one size category.

Every soil type and size category can support multiple plants.

Each climate is mapped to a specific soil type/location.

Solar exposure is dictated by the specific climate zone.

<img width="1080" height="418" alt="image" src="https://github.com/user-attachments/assets/39e464d4-db86-4d52-98e2-a8586d9c3aae" />

> **Note:** Made using Microsoft Visio

---

## Normalization & Schema Refinement
To ensure data integrity and reduce redundancy, the schema was refined to reach Third Normal Form (3NF).

**Original ER Model**: 
<img width="1065" height="427" alt="image" src="https://github.com/user-attachments/assets/da0da006-e628-45eb-87b0-c56773473d6f" />
> **Note:** Made using Microsoft Visio 


### Modifications for 3NF
Table Splitting: The original SoilType table was split into two distinct entities: Location and Soil.

Justification: This removal of transitive dependencies ensures that non-key attributes (like specific soil composition) depend only on the primary key, satisfying 3NF requirements.

<img width="975" height="898" alt="image" src="https://github.com/user-attachments/assets/e6dfae42-16e2-4553-b3b4-889a08483131" />

### Implementation of Relationships
For 1:M (One-to-Many) relationships, the parent table's Primary Key (PK) was implemented as a Foreign Key (FK) within the child table.

Example: The Climate table uses locationID as a Foreign Key. This allows multiple climate profiles to reference a single location without duplicating location data.

--- 
## Collaborative Evolution
The project benefited from peer review, resulting in the following technical improvements:

**Visual Clarity**: Added direction arrows and explicit PK/FK mapping to the ERM diagrams.

**Granularity**: Expanded attributes to include scientific naming and specific soil/climate metrics for better data retrieval.

---
## Future Optimization
To further increase database efficiency and reduce complexity, a proposed modification for Version 2.0 includes:

**Entity Consolidation**: Eliminate the Sun entity and migrate the sunAmt attribute directly into the Climate table.

**Reasoning**: Since sun exposure is logically dictated by climate patterns, this modification simplifies the schema and reduces the number of joins required for environmental queries without losing critical data.

## Tools & Technologies
**Database**: MySQL

**Modeling**: Microsoft Visio

---

## Author 
Abigail Corbett <br> 
April 15th, 2026
