# Stage 03 – Data Persistence Layer

## 1. Overview

Stage 03 focuses on transforming the system from real-time AWS API fetching to a persistent, structured data architecture. 

In previous stages, AWS services were successfully integrated and data could be fetched dynamically. However, real-time retrieval alone is insufficient for analytics, forecasting, optimization, or sustainability modeling.

Therefore, a robust data persistence layer was introduced using PostgreSQL and SQLAlchemy ORM.

---

## 2. Problem Statement

In Stage 02, AWS services (EC2, CloudWatch, Cost Explorer) were integrated successfully. However:

- Data was not stored permanently.
- No historical dataset existed.
- Trend analysis was not possible.
- Forecasting was impossible.
- Optimization insights lacked context.
- System behavior was stateless.

To enable intelligence and automation, persistent storage of infrastructure, cost, and performance metrics was required.

---

## 3. Architectural Enhancement

The architecture evolved from:

AWS → FastAPI → JSON Response

To:

AWS → Sync Layer → PostgreSQL → Analytics APIs

This transition marks the system’s shift from API demonstration to data-driven backend architecture.

---

## 4. Database Design

PostgreSQL was used as the relational database system.

SQLAlchemy ORM was implemented to ensure:
- Structured models
- Clean schema management
- Type safety
- Scalability
- Maintainability

Three core tables were designed.

---

## 5. Database Schema

### 5.1 EC2 Instances Table (`ec2_instances`)

**Purpose:**  
Store infrastructure metadata for tracked EC2 instances.

**Columns:**
- `id` (Primary Key)
- `instance_id` (String, indexed)
- `instance_type` (String)
- `state` (String)

**Design Rationale:**
- Enables infrastructure tracking.
- Provides metadata for CPU and cost correlation.
- Supports state change monitoring (running/stopped).

---

### 5.2 Daily Cost Table (`daily_costs`)

**Purpose:**  
Store historical cost data retrieved from AWS Cost Explorer.

**Columns:**
- `id` (Primary Key)
- `date` (Date, unique, indexed)
- `amount` (Float)
- `unit` (String)

**Key Features:**
- 30-day historical retrieval.
- Duplicate prevention based on date.
- Time-series ready structure.

**Design Rationale:**
- Enables cost trend analysis.
- Enables forecasting.
- Enables sustainability modeling.
- Enables anomaly detection.

---

### 5.3 CPU Metrics Table (`cpu_metrics`)

**Purpose:**  
Store daily average CPU utilization per instance.

**Columns:**
- `id` (Primary Key)
- `instance_id` (String, indexed)
- `date` (Date, indexed)
- `average_cpu` (Float)

**Design Rationale:**
- Enables idle detection.
- Enables optimization suggestions.
- Supports sustainability scoring.
- Supports infrastructure efficiency modeling.

---

## 6. Sync Mechanism Implementation

To populate database tables, dedicated synchronization endpoints were created.

### 6.1 Infrastructure Sync
Endpoint: `POST /sync-ec2`

- Fetches EC2 instances.
- Inserts new instances.
- Prevents duplicate entries.

---

### 6.2 Cost Sync
Endpoint: `POST /sync-cost`

- Fetches last 30 days of cost data.
- Stores daily cost.
- Prevents duplicate date entries.
- Maintains clean historical dataset.

---

### 6.3 CPU Sync
Endpoint: `POST /sync-cpu`

- Fetches average CPU utilization from CloudWatch.
- Stores daily metric per instance.
- Prevents duplicate date + instance entries.

---

## 7. Analytics API Layer

To expose structured data for future dashboards and intelligence modules:

### 7.1 Cost Trend API
Endpoint: `GET /cost-trend`

Returns time-series daily cost data.

---

### 7.2 Cost Summary API
Endpoint: `GET /cost-summary`

Returns:
- Total cost (30 days)
- Average daily cost
- Highest cost day
- Lowest cost day
- Number of stored days

---

### 7.3 CPU Trend API
Endpoint: `GET /cpu-trend`

Returns daily CPU utilization per instance.

---

## 8. Data Integrity Measures

- Unique constraints on dates.
- Duplicate prevention logic.
- Session management using SQLAlchemy.
- Controlled commit operations.
- Exception handling during sync operations.

---

## 9. Outcome of Stage 03

After Stage 03 completion:

- Historical cost dataset available (30 days).
- CPU utilization dataset available.
- Infrastructure metadata persistently stored.
- Time-series APIs available.
- Foundation for forecasting and optimization established.

The system transitioned from stateless API integration to a structured, persistent, analytics-ready backend.

---

## 10. Architectural Impact

Stage 03 establishes:

- Data warehouse foundation
- Analytical readiness
- Intelligence preparation layer
- Production-grade backend design

This stage marks the transformation from integration project to scalable cloud intelligence system.
