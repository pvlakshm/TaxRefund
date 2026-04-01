# Functional Specification: Partial Refund Logic

## Overview
This document defines the mathematical and state-transition rules for partial refunds within the Enterprise Cloud platform.

## 1. Calculation Logic
When a partial refund is initiated, the system must calculate the tax portion to be returned to the user.

**Formula:**
$$Tax_{refund} = \left( \frac{Amount_{refund}}{Amount_{total}} \right) \times Tax_{total}$$

* **Rounding Rule:** Round to the nearest two decimal places (Half-Up).
* **Validation:** $Amount_{refund}$ cannot exceed the $Amount_{remaining}$ of the original transaction.

## 2. API Endpoints involved
| Method | Endpoint | Description |
| :--- | :--- | :--- |
| POST | `/v1/payments` | Create initial authorization |
| POST | `/v1/payments/{id}/capture` | Finalize funds |
| POST | `/v1/payments/{id}/refund` | Process refund (Partial/Full) |

## 3. Database State Mapping
* `Status: 1` -> Pending
* `Status: 2` -> Captured
* `Status: 3` -> Partially Refunded
* `Status: 4` -> Fully Refunded