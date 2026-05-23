# Non‑Functional Requirements (NFR) Template  
A reusable accelerator for defining banking‑grade NFRs across modernization programs.

---

## 1. Performance
- **Latency:** Target <50 ms for real‑time interactions (fraud, RTP, C360).  
- **Throughput:** Minimum sustained throughput required (e.g., 10k–50k events/sec).  
- **Scalability:** Horizontal scaling for peak loads and seasonal spikes.

---

## 2. Availability & Resilience
- **Uptime:** 99.9%–99.99% depending on criticality.  
- **Failover:** Multi‑AZ deployment with automated recovery.  
- **Resilience Patterns:** Circuit breakers, retries, back‑pressure handling.

---

## 3. Security
- **Encryption:** TLS 1.2+ in transit, AES‑256 at rest.  
- **Access Control:** RBAC, least‑privilege, audit logging.  
- **Compliance:** PCI, SOX, FFIEC, GDPR (as applicable).

---

## 4. Data Quality & Integrity
- **Consistency:** Event ordering guarantees per key/domain.  
- **Validation:** Schema enforcement and backward‑compatible evolution.  
- **Lineage:** End‑to‑end traceability for audit and regulatory needs.

---

## 5. Observability
- **Monitoring:** Metrics for latency, throughput, lag, error rates.  
- **Logging:** Structured logs with correlation IDs.  
- **Alerting:** Threshold‑based alerts for SLA/SLO breaches.

---

## 6. Reliability & Durability
- **Message Durability:** Replication factor (e.g., RF=3).  
- **Retention:** Configurable retention aligned with business/regulatory needs.  
- **Replay:** Controlled replay for recovery and analytics.

---

## 7. Operational Excellence
- **Deployment:** Automated CI/CD pipelines with blue‑green or canary releases.  
- **Configuration:** Centralized configuration management.  
- **Runbooks:** Standardized operational procedures for incidents.

---

## 8. Regulatory & Risk Requirements
- **Auditability:** Immutable logs and event trails.  
- **Data Minimization:** Only essential PII/PCI included in events.  
- **Retention & Purging:** Policies aligned with regulatory mandates.

---

This template standardizes NFR definition across modernization programs and ensures consistent, banking‑grade delivery.

