# Stage 04 – Automation Layer

## 1. Overview

Stage 04 introduces automation into the Cloud Intelligence Platform. 

Until Stage 03, data synchronization required manual API triggering. This limited the system’s autonomy and scalability.

The objective of Stage 04 was to build a self-operating backend capable of continuous data collection.

---

## 2. Problem Statement

Manual sync operations caused:

- Inconsistent dataset growth
- Human dependency
- Lack of scheduled monitoring
- Reduced realism in system behavior

Real cloud systems operate continuously and automatically. Therefore, automation was required.

---

## 3. Solution Approach

APScheduler (Advanced Python Scheduler) was integrated into the FastAPI backend to enable scheduled background execution.

---

## 4. Why APScheduler?

Alternative considered:
- Linux Cron Job

APScheduler was selected because:

- Native Python integration
- Works within FastAPI process
- Easier to document
- Better suited for research-grade backend
- Controlled lifecycle management
- Clean error handling

---

## 5. Automation Architecture

New flow:

AWS Services  
↓  
APScheduler (Background Job)  
↓  
Sync Layer  
↓  
PostgreSQL  
↓  
Analytics APIs  

---

## 6. Scheduler Configuration

Scheduler type:
- BackgroundScheduler

Configuration included:

- Interval trigger (24 hours)
- Misfire handling
- Single instance execution control
- Thread pool executor
- Grace time configuration
- UTC timezone standardization

---

## 7. Automated Tasks

The scheduled job performs:

1. EC2 synchronization
2. Cost synchronization (30-day window)
3. CPU metrics synchronization

All operations are wrapped in:
- Try-except blocks
- Controlled database sessions
- Graceful closure handling

---

## 8. Execution Strategy

For testing:
- Interval set to 1 minute.

For production:
- Interval configured to 24 hours.

This ensures:
- Continuous data growth
- Zero manual dependency
- Production-like backend behavior

---

## 9. Error Handling & Stability

- Misfire grace time configured.
- Max instance set to 1 to prevent overlap.
- Controlled database sessions.
- Console logging for monitoring.
- Scheduler started at application startup.

---

## 10. Outcome of Stage 04

After Stage 04 completion:

- System operates autonomously.
- Daily cloud telemetry is automatically stored.
- Historical dataset grows without intervention.
- Backend simulates production cloud monitoring system.

---

## 11. Architectural Significance

Stage 04 upgrades the system from:

Manual Data Platform

To:

Autonomous Cloud Intelligence Engine

This significantly increases system realism, scalability, and engineering depth.

---

## 12. Readiness for Next Stage

With automation complete, the system is now ready for:

- Dashboard layer
- Intelligence layer (forecasting)
- Optimization modeling
- Carbon estimation
- Sustainability scoring


So likewise Stage 04 completes the backend infrastructure foundation.

