# Enterprise Event Taxonomy for Banking Modernization

## 1. Introduction

This document defines the enterprise-wide event taxonomy used across Customer 360, Fraud & AML, Loan Origination, Real-Time Payments, and Core Banking.  
It establishes a unified, canonical event model that enables interoperability, real-time analytics, and event-driven orchestration across all banking domains.

The taxonomy ensures:
- Consistent event naming
- Standardized schemas
- Clear producer–consumer relationships
- Replayability and auditability
- Regulatory alignment
- Cross-domain integration

---

## 2. Event Naming Standards

### 2.1 Naming Convention
Events follow the pattern:

<Domain><Entity><Action>Event


Examples:
- CustomerProfileUpdatedEvent  
- PaymentInitiatedEvent  
- FraudAlertRaisedEvent  
- LoanApplicationSubmittedEvent  
- AccountCreatedEvent  

### 2.2 Event Categories
- **Business Events** – customer actions, payments, applications  
- **Risk Events** – fraud alerts, AML flags, sanctions hits  
- **Lifecycle Events** – approvals, settlements, postings  
- **System Events** – retries, failures, timeouts  

---

## 3. Canonical Event List (Cross‑Domain)

### 3.1 Customer 360 Events
| Event | Description |
|-------|-------------|
| CustomerProfileUpdatedEvent | Customer data updated |
| CustomerIdentityVerifiedEvent | KYC verification completed |
| CustomerRiskScoreUpdatedEvent | Risk score recalculated |
| CustomerRelationshipCreatedEvent | New relationship established |

---

### 3.2 Fraud & AML Events
| Event | Description |
|-------|-------------|
| FraudAlertRaisedEvent | Fraud engine flags a transaction |
| FraudScoreUpdatedEvent | Real-time risk score generated |
| AMLScreeningCompletedEvent | Sanctions/AML checks completed |
| CaseCreatedEvent | Case management workflow triggered |

---

### 3.3 Real-Time Payments Events
| Event | Description |
|-------|-------------|
| PaymentInitiatedEvent | Payment request received |
| PaymentValidatedEvent | Validation completed |
| FundsAvailabilityCheckedEvent | Balance check performed |
| PaymentReleasedEvent | Payment sent to RTP/FedNow |
| PaymentSettledEvent | Settlement confirmed |
| PaymentFailedEvent | Payment rejected or timed out |

---

### 3.4 Loan Origination Events
| Event | Description |
|-------|-------------|
| LoanApplicationSubmittedEvent | Application received |
| CreditDecisionGeneratedEvent | Automated decision created |
| DocumentVerifiedEvent | OCR/verification completed |
| UnderwritingCompletedEvent | Manual underwriting done |
| LoanApprovedEvent | Final approval |
| LoanFundedEvent | Funds disbursed |

---

### 3.5 Core Banking Events
| Event | Description |
|-------|-------------|
| AccountCreatedEvent | New account opened |
| AccountUpdatedEvent | Account attributes changed |
| LedgerPostedEvent | Debit/credit posted |
| BalanceUpdatedEvent | Balance recalculated |

---

## 4. Canonical Event Schema

### 4.1 Standard Fields
All events share a common envelope:

```json
{
  "eventId": "UUID",
  "eventType": "string",
  "eventTimestamp": "ISO-8601",
  "correlationId": "string",
  "sourceSystem": "string",
  "payloadVersion": "v1",
  "payload": {}
}
{
  "transactionId": "string",
  "customerId": "string",
  "amount": 125.50,
  "currency": "USD",
  "channel": "Mobile",
  "destinationBank": "string",
  "paymentType": "RTP"
}


sequenceDiagram
    participant C360 as Customer 360
    participant Fraud as Fraud Engine
    participant RTP as Real Time Payments
    participant Core as Core Banking

    C360->>Fraud: CustomerProfileUpdatedEvent
    Fraud->>RTP: FraudScoreUpdatedEvent
    RTP->>Core: PaymentReleasedEvent
    Core->>RTP: PaymentSettledEvent


sequenceDiagram
    participant App as Loan Application
    participant LOS as Loan Origination System
    participant Fraud as Fraud Engine
    participant Core as Core Banking

    App->>LOS: LoanApplicationSubmittedEvent
    LOS->>Fraud: FraudCheckRequestedEvent
    Fraud->>LOS: FraudScoreUpdatedEvent
    LOS->>Core: LoanFundedEvent
