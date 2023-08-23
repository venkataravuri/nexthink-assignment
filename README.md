<img src="nexthink-logo.png" width="30%" height="30%">

# Nexthink Interview Assignment

### Quick Overview

A high-level architecture of alternative forward-looking solution that replaces existing single-tenant solution with a scalable & elastic multi-tenant solution. It also highlights how the proposed solution addresses limitations & constraints for current system with a re-engineered and re-architected solution.

Refer to assignment problem statement [Nexthink Architecture Quiz]() for existing system contraints and goals of prposed solution.

**Disclaimer**

System design & architecture has many approaches and alternatives, approaches that I took in prposed solution is soley based on assignment instructions with narrow descriptions. Hence, it could be changed based on understand use cases in depth. Architecure is about "Trade-offs" along with several dimensions scalability, reliability, throughput, cost-effectivness and more. Proposed architecture best of everything.  

**Table of Contents**
- ?
- ?
- ?

### Foreword

The **to-be architecture** is explained through ```Functional Architecture, Technical Architecture, Component Designs, Deployment Architecture and more```, each addressing unique concerns for distinct stakeholders & audience.

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
5. Resilient: Solution component should be resilient to network glitches, hardware failure with 'no single-point failue' and be crash-tolerant wit recoverability & fault-tolerant.

Leverage mix of cloud agnostic & could-specific services 

3. **Security, Governance and compliance**: Able to 


### Functional Architecture & Design

### Requirements & High-level Use Cases

#### Data Volumes

## Solution Architecture

### Ingestion subsystem components & design

The subsystem components are designed to,
- Handle **write-heavy traffic** with **high concurrency**
- Ensure very **low-latency** and high-throughput
- Follows **Pub/Sub model** for scalability and handle **backpressure**
- Processing of events should be idempotent and **crash-tolerant**
- Resiliencey when service crashes

Ingestion mechanism supports in-steam trends/analytics for SRE & Tech Ops teams to spot any anomolies and take corrective action.

<img src="" width="" height="" alt="Ingestion subsystem" />

Refer to Miro diagram.

### Critical Components Role & Responsibilities

#### Ingestion Gateway

Ingestion Gateway is a horizontally scalable bi-directional communication service to captures 'Collector Agent' emitter events/data, validates them and deliver to relevant Kafka topics to further processing. The validation includes,
1. Authenticate Collector Agents through Client Certificates or other credentials/token-based mechnisms.
2. De-compress, perfrom schema & semantic validation of Payloads along with JSON vulneriblity checks.
3. Induce tracking/trace id (if not exists)
4. Rate-limits (may require **Redis with sliding-window pattern**)
   
- Gateway is also responsible to trigger remote actions on 'Collector Agents' when they are connected. 
- Collector Agent & Gateway ensure that events are delivered at-least once / exactly-once through re-try and tracking id mechanisms. 
- Gateway uses Kafka cluster acts as buffer layer to  Backpressure
- Batched 

#### Scaling to ?? millions events

To handle bursty workloads & latency-sensitive workloads, Gateway components are deployed to Kubernetes(K8s) cluster with horizontal Pod Autoscaler (HPA) based on throughput metrics.

Processing of raw data is des-coupled from capture for high-throughput. Backpressures due to downstream processing delays and database bottlenecks are handled through Kafka as buffer layer.

**Alternatives**: For extreme low-latency processing ```Disruptor``` pattern can be employeed, but its too complex.

**Kafka Topic Strategy**
For parallel processing, multiple Kafka topics with partitions should be introduced. Topics can be designed by tenant or by data/entity type or by function and more. Topic by tenant may not be ideal, when a new tenant is added new topics & partitions should be created along with consumers should be introduced.

### Streaming Apps & Near-realtime Analytics

Streaming apps will process incoming data/events to,

1. Detect anomolies
2. Alert & Notify customers for any anolomies
3. Observe metrics (throughput and latencies) and take corrective actions.

A dashobard for Tech. Ops. teams to monitor health of Ingestion Processing pipline.

### Ingestion Processors (Microservices)

A set of Self Contained Services (Microservices) are deployed to,
- De-duplication of raw data (We can emply '**Rotating Bloom Filters**')
- Enrich data before storing into Clickhouse
- Transform into query-friendly db format

These Microservices are Kafka consumers and auto-scaled through K8s HPA. They have thier own database schema hosted on shared AWS RDS PostgreSQL (Is it really requred?).

There could be raw data capture service for audits, compliance and future legal conflicts or Peformance & Volume testing dress reherrsals.

### Portal subsystem components Solution Architecture - 

#### Analytics & Insights


### Technical Architecture

### Technology Choices & Tech Stack

#### Deployment & Security Architecture

### Security & Privacy

### Performance View

## Data Model 

