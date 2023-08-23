# Nexthink Interview Assignment

This document proposes a high-level architecture to replace existing single tenant solution with a scalable & elastic multi-tenant solution.

Refer to [Nexthink Architecture Quiz]() document for detailed problem statement.

**Table of Contents**
- ?
- ?
- ?

### Foreword

The to-be architecture is explained with ```Functional Architecture, Technical Architecture, Component Designs, Deployment Architecture and more```, each addressing unique concerns for distinct stakeholders & audience.

While proposing solution, I made plenty of assumptions, also highlighed rationale behind those assumptions.

#### Assumptions


#### Out of Scope

Due to time constraintes, folloiwng topics are considered as out of scope,

1. Only high-level migration strategy has ebee captured, but not includes Data Migration and component by component cut-over strategy.
2. ?
3. ?

#### Current Solution Limitations & Constraints

#### To-Be Architecture & Solution

Re-engineer & refactor existing components to pave-a-way for a true multi-tenant solution which is resilient, crash & fault tolerant and extremely scalable.

### High-level Goals

The overaching goals of re-architected solution are,

1. **Multi-Tenant Model**: All customers (aka. tenants) shared infrastrucutre with strong ```Tenant Isolation``` with guardrails to deal with noisy neighbours while keeping their data isolated.
2. **Scalablity & Elasticity**: Solution components should be horizontally scalable and leverage elasticity provided by underlying cloud platform. Should withstand bursty workloads during peak usage hours.
4. **Event-driven Interactions**: Solution components should be loosely coupled for resiliency and independently deployable with different frequencies. Also should enable parallel development with multiple teams working across
5. Resilient: Solution component should be resilient to network glitches, hardware failure with 'no single  

3. **Security, Governance and compliance**: Able to 


### Functional Architecture & Design

### Requirements & High-level Use Cases

#### Data Volumes

### Ingestion System Components - Solution Architecture

### Portal subsystem components Solution Architecture - 

#### Analytics & Insights


### Technical Architecture

### Technology Choices & Tech Stack

#### Deployment & Security Architecture

### Security & Privacy

### Performance View

## Data Model 

