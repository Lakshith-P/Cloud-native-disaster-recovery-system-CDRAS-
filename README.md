# ☁️ Cloud-Based Disaster Recovery Automation System (CDRAS)

## Project Overview

CDRAS is a robust, cloud-native system designed to **automate disaster detection, orchestration, and recovery** across cloud regions. It transitions business continuity from error-prone manual processes to a highly resilient, observable, and automated workflow.

The core objective is to ensure minimal disruption and **maximum data integrity** following a critical infrastructure failure.

---

## Key Technical Objectives (SLOs)

The system is engineered to meet strict **Service Level Objectives (SLOs)** that define recovery speed and data integrity:

| Metric | Target | Description |
| :--- | :--- | :--- |
| **Recovery Time Objective (RTO)** | **< 5 Minutes** | Time taken from failure detection to full system operational state in the secondary region. |
| **Recovery Point Objective (RPO)** | **< 1 Minute** | Maximum acceptable amount of data loss during a recovery event. |
| **Availability** | **99.99%** | Target system uptime for the CDRAS orchestration layer. |
| **Durability** | **99.999999999%** | Data durability for stored backup snapshots. |
| **Monitoring Latency** | **< 200 ms** | Speed of health check updates to the central monitoring service. |

---

## High-Level Architecture

CDRAS utilizes a microservices architecture to achieve resilience and high throughput:

### 1. Core Services
* **Monitoring Service:** Real-time health checks and outage detection.
* **Recovery Orchestrator:** Handles stateful failover runbooks and provisioning in the secondary region.
* **Notification Service:** Sends alerts (Email/SMS) based on recovery status.

### 2. Data Layer

| Component | Purpose | Consistency |
| :--- | :--- | :--- |
| **Data Stores** (PostgreSQL/S3) | Configurations and immutable backup snapshots. | **Strong** (for recovery status) |
| **Cache** (Redis) | Stores recent system status for low-latency dashboard access. | **Strong** |
| **Queues** (RabbitMQ) | Asynchronous task processing for long-running backup replication. | **Eventual** |
*The architecture utilizes **resiliency patterns** including Circuit Breakers and exponential backoff retries.*

---

## Technology Stack

| Category | Tools |
| :--- | :--- |
| **Cloud Platforms** | AWS / Azure / GCP (Targeted for deployment) |
| **Backend** | Python (Flask / FastAPI) |
| **Data & Storage** | PostgreSQL, S3/Blob Storage |
| **Messaging & Cache** | RabbitMQ / Azure Queue, Redis |
| **Observability** | Prometheus, Grafana, ELK (Logs), OpenTelemetry (Traces) |
| **Deployment** | Docker + Kubernetes / AKS |

---

## 🚀 Getting Started

### Prerequisites

The system assumes the following prerequisites are met:
1.  Pre-configured, active recovery regions on the target cloud platform (AWS or Azure).
2.  Secure network connectivity between primary and secondary regions.
3.  Base system images/templates for automated instance spinning.

### Architectural Diagrams
Diagrams providing visual context for the system are available in the repository's documentation directory, generated using **PlantUML**:
* `cdras_system_context.puml` (High-level boundary diagram)
* `cdras_failover_sequence.puml` (Step-by-step sequence of automated failover)
* `cdras_data_layer.puml` (Component view of the data persistence and caching layer)
