<img src="docs/images/nexthink-logo.png" width="20%" height="20%">

# 🔥 Nexthink Interview Assignment 🎉

Assignment response is documented in my personal Github repository at using Markdown language, 🌎 ⚓ https://github.com/venkataravuri/nexthink-assignment/

### 🚁 Quick Overview

A high-level architecture of alternative forward-looking solution that replaces existing single-tenant solution with a scalable & elastic multi-tenant solution. It also highlights how the proposed solution addresses limitations & constraints for current system with a re-engineered and re-architected solution.

Refer to assignment problem statement [Nexthink Architecture Quiz]() for existing system contraints and goals of prposed solution.

The 🎡 **to-be architecture** is explained through ```Functional Architecture, Technical Architecture, Component Designs, Deployment Architecture and more```, each addressing unique concerns for distinct stakeholders & audience.

> While proposing solution, I made plenty of assumptions, also highlighed rationale behind those assumptions.

‼️ **Disclaimer**

System design & architecture has many approaches and alternatives, approaches that I took in prposed solution is soley based on assignment instructions with narrow descriptions. Hence, it could be changed based on understand use cases in depth. Architecure is about "Trade-offs" along with several dimensions scalability, reliability, throughput, cost-effectivness and more. Proposed architecture best of everything.  

### 📚 Table of Contents
- [Assumptions]() & [Out of Scope]()
- [Current Solution Limitations & Constraints]()
- [To-be Architecture]()
    - [High-level Architecture Goals]()
- [Funtional Analysis & Design]()
    - [Functional Requirements]()
    - [Non Functional Requirements]()
        - [Data Volumes & Traffic Projections]()
- [Solution Architecture]()
    - [Ingestion Subsystem Design & Components]()
        - [Techincal Architecture]()
        - [Scalability & Near real-time Analytics]()
    - [Experience Subsystem Desing & Components]()
        - [Technical Architecture]()
            - [Microfrontents]()
            - [Business/Domain Services]()
            - [Data Analytics & Insights]()
- [Deployment Architecture]()
- [Security Architecture]()
- [References]()


#### Assumptions

#### Out of Scope

Due to time constraintes, folloiwng topics are considered as out of scope,

1. Only high-level migration strategy has ebee captured, but not includes Data Migration and component by component cut-over strategy.
2. ?
3. ?

#### Current Solution Limitations & Constraints

#### To-Be Architecture & Solution

Re-engineer & refactor existing components to pave-a-way for a true multi-tenant solution which is resilient, crash & fault tolerant and extremely scalable.

### 🚩 High-level Architecture Goals

The overaching goals of re-architected solution are,

1. **Multi-Tenant Model**: All customers (aka. tenants) shared infrastrucutre with strong ```Tenant Isolation``` with guardrails to deal with noisy neighbours while keeping their data isolated.
2. **Scalablity & Elasticity**: Solution components should be horizontally scalable and leverage elasticity provided by underlying cloud platform. Should withstand bursty workloads during peak usage hours.
4. **Event-driven Interactions**: Solution components should be loosely coupled for resiliency and independently deployable with different frequencies. Also should enable parallel development with multiple teams working across
5. Resilient: Solution component should be resilient to network glitches, hardware failure with 'no single-point failue' and be crash-tolerant wit recoverability & fault-tolerant.

Leverage mix of cloud agnostic & could-specific services 

3. **Security, Governance and compliance**: Able to 

### 🌈 Functional Analysis & Design

The main actors of the system could be,
1. Organization employees
2. IT Help Desk Staff
3. IT Ops.
4. Privacy Officer & InfoSec Teams
5. Device & Peripheral Providers
6. System Administrators

#### 🚞 Functional Requirements

Only architecure significant system use cases and features are analyzed,

The solution has belwo feature for IT Help Desk and Ops. teams,

**Digital Employee Experience Features**: 
- Track a rich set of metrics like device health, OS, app performance, users, and network. Proactively identify issues, troubleshoot and remediate with automation. 
- Insight into employee experience across installed apps and OS. Quickly surface users, apps and devices with poor experience that need your attention.
- Gather employee sentiment through customized and contextual surveys. Get timely insights into overall employee experience beyond quantitative performance metrics, and set up workflows based on survey responses.

System Administrators should be able to,

**Workflow Orchestration**
- Orchestrate and automate IT tasks, resolve issues, and send user notifications with Freestyle Orchestrator, a powerful, no/low-code orchestration platform. Extend workflows to third-party tools across your environment via REST API.
- Automate incident management with contextual dashboards that surface diagnostic information relevant to the specific issue. 

**Actionable Insights**
Aggregate and correlate data from multiple sources across your digital workspace to visualize environment KPIs, understand trends and gain meaningful insights.

#### ♨️ Non Functional Requirements

Following non-fucntional requiremnts have been highlighted as critical to to-be solution [Few assumed by nature of the solution],

- Availablity - System components should be highly available across several geographies.
- Performance - Services should have low-latency and support high-throuput. Should accomodate burst workloads during peak hours. 
- Resiliency - System component should be resilient to temporary glitiches and self-healing. Components should recover from crash
- Scalabiliyt & Elasiticity - Components should be auto-scalable based on traffic patterns
- Privacy & Data Localization - Should complaint to GDPR and other privacy governance rules.
- Isolation - Data of each tenant is isolated.

RTO & RPO of the system services not specified, however it is assumed thety will be stringent as critical to businesses.

#### ✈️ Data Volumes & Traffic Projections 🎢

Below is quick estimate of capacity and projected traffic volumes. This information will help Infra & DevOps teams to size the infrastructure capacity to coup peak traffic scenarios. Also acts as inputs to Performance and Volume testing aka. Load Testing.

- Each collector captures, aggregates, and broadcasts daily about 1-2000 events totaling 10MB from each device.
- Our customers have between 10K and 500K installed collectors.
- 1000 customers for a total of 15 Million endpoints

```
Data volume per day ~ (Data size per day by a collector) * (# of collectors) * (# no. of customers)
                    ~ 10 MB * 500 K * 1000 Customers
					~ 👊 4,768 TB (Or) 4.6 PB
```

> Note: It is unclear that data capture is compressed or not. 

**🚖 Traffic Estimates**

It is assumed that employees work 8 hours a day employees. Also assumed several employees start their work at regular interval of the day, resulting peak traffic.

Assumption: 2000 events in a day ~ 2000/8 ~ 5

| Device | Traffic per **min** | Y1 Growth |
| --- | --- | --- |
| 1 collector | 5 rps | 6 rps/min | 
| 500K Collectors | 👊 2.5 million rps/min | ? |
| 1000 customers Collectors | 🚀🚀🚀 2.5 billion rps/min | ? |

## 🏁 Solution Architecture

Solution architecture borken down into two streams, namely,

1. Ingestion subsystem
2. Experiences subsystem 

### 🚀 Ingestion subsystem components & design

The subsystem components are designed to,
- Handle **write-heavy traffic** with **high concurrency**
- Ensure very **low-latency** and high-throughput
- Follows **Pub/Sub model** for scalability and handle **backpressure**
- Processing of events should be idempotent and **crash-tolerant**
- Resiliencey when service crashes

Ingestion mechanism supports in-steam trends/analytics for SRE & Tech Ops teams to spot any anomolies and take corrective action.

<img src="docs/images/Ingestion.jpg" width="100%" height="100%" alt="Ingestion Subsystem Architecture" />

Can't see diagram, click [Miro](https://miro.com/app/board/uXjVMsKyGeM=/?share_link_id=177577594401) to view diagram.

### Critical Components Role & Responsibilities

#### 🎌 Ingestion Gateway

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

### 🏇 Streaming Apps & Near-realtime Analytics

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

## 🌎 Portal Subsystem Architecture

<img src="docs/images/portal.jpg" width="100%" height="100%" alt="Portal & Business service Components" />

### SPA & Microfrontents

Refer to section '' for Layered Techincal Architecture.

### Business/Domain Services

Reactor existing 'Engine' functionality into multiple domain-specific microservices aka. Cloud-Native apps. Cloud native apps can exploit scale, elasticity, resiliency, and flexibility provided by in public clouds. Inviddual teams can work on these microservices and rollout new functionality quickly.

- The services should be designed as a self contained services or microservices, packed as containers for portability, deployed to immutable infrastructure.
- Microservices communicate with each other via APIs and use event-driven architecture, which makes them loosely coupled, serves to enhance the overall performance of each application.

| Microservice | Role & Responsibilities|
| --- | --- |
| Digital Experience API | ? |
| Remote Actions | ? |
| Query Engine | ? |
| Integration Platform Services | ? |

Each of these services will have their own databases where process state-machine informaiton and metadata is stored. The insights are sourced from Clickhouse database.

#### Internal Communincaitons

Services are communicate through event-driven mechanism over a pub/sub channel. Each each service emits events which are subscribed by other services to perform the actions. For example, digital experience service can emit notification events which are subsribed by Remote Actions service to delevier to user. 

##### Peer-to-Peer Choregraphy & Centralized Workflow/Orchestration Engine

Peer to peer task choreography using Pub/sub model works for simplest flows, but this approach has following issues:
- Process flows are “embedded” within the code of multiple microservices
- As the number of microservices grow and the complexity of the processes increases, getting visibility into these distributed workflows becomes difficult without a central orchestrator.
- Cannot answer "How much are we done with process X"?

Hence a centralized Orchestration Engine is also needed to orchestrate microservices-based process flows.
- Each task in process or business flows are implemented as microservices.

### Technical Architecture

### Technology Choices & Tech Stack


### 📊 Data Analytics & Insights

Turn raw data which is a collection of facts into actionable insights. Analyse raw data for data-driven insights in the form of patterns, trends, groups, segments to answer certain types of questions. 

Follow below 5-step process to derive insights, metrics aka. KPIs.

1. Data cleaning
2. Establishing relationships and trends
3. Statistics calculation
4. Build advanced analytics models 
5. Constitute this process.

### Data Modeling

A shared database & shared schema approach would be ideal for given use cases. Wherein tenants' data is separated by a column in each table (could be TenantId), that shows the owner of the row.

Every domain entity information includes three classes of columns **time, dimensions and metrics**.
- Combination of **tenant-id & timestamp** column is the primary partition mechanism. 
- **Dimensions** are values that can be used to filter, query or group-by.
- **Metrics** are values that can be aggregated, and are nearly always numeric.

Entities are ```modeled by data source``` over ```model by metrics```

Modeling by Metrics - Measurements of all metrics of the same data source at a certain time point are stored in the same row.

Modeling by Metrics - odeling by metrics, where each row of data represents a measurement of a certain metric of a data source at a certain time point.

Below ER diagram depicts few critical entitites in the solution,

<img src="docs/images/data-model.jpg" width="35%" height="35%" alt="data model" />

Build Data Processing Jobs which perform SQL & MapReduce tasks to analyze data patterns, trends, groups, segments to answer certain types of questions.

Performance Tips: Downsampling through rollups were converting high-resolution time series data into low-resolution time series data.

### Performance Assurance

> Due to time constraints, could not document, how services meet non-functional requirments such as Reliability, Throughput, Availability & Resiliency.

### Security & Privacy

#### Authentication & Authorization

> Due to time constraints, could not come up with a diagram that depicts, how Confidentiality, Integrity, Availablity (CIA) among all comunicating involoved in entire solution.

**Collector Authentication**

Collector & Ingestion Gateway will follow mutual authentication based on PKI certifcates. During provisioning of a collector on end-device, an identity and PKI certificates are injected.  

Certficates can be rotated when employeed logged on to network through end-device management mechanisms. Identity & Access management module has to block any comprmised devices where intruder can take over identity and PKI certificates.

All internal and external communciations will be done through secure channel mostly TLS.

**Experience Portal & Admin Console Authentication Mechanism**

A multi-factor authentication (MFA) should be established for accessing SaaS application & services.

**API Communcation**
- For Public APIs, OAuth based client & secret based mechnism would be ideal.
- Fore internal APIs, mTLS is right option along with Tenant ID propagation through (X-Tenant-ID) and other mechanisms.

#### Privacy & Data Residency



