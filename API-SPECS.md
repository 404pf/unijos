# Unijos Portal API Specifications

## 1. System Context
The Unijos Portal operates as a "Black Box" system. All interactions are external, relying on public API endpoints for data exchange.

## 2. Key Payment Integration (Remita)
The Remita gateway handles student fee payments. The following endpoints are critical for monitoring transaction integrity:

### 2.1. Payment Initiation
- **Endpoint:** `POST /v2/order/create`
- **Function:** Initiates a new payment transaction for a student.
- **Data Fields:** `trans_id`, `email`, `amount`, `reference_number`
- **Potential Bug Focus:** Transaction synchronization delays and status reconciliation.

### 2.2. Transaction Status Verification
- **Endpoint:** `GET /v2/order/status/{ref_no}`
- **Function:** Retrieves the real-time status of a payment (e.g., Pending, Completed, Failed).
- **Data Fields:** `status_code`, `payment_date`, `gateway_reference`
- **Potential Bug Focus:** API latency and error handling during high-traffic periods.

### 2.3. Payment Reconciliation
- **Endpoint:** `POST /v2/order/reconcile`
- **Function:** Validates and updates the university's internal database with Remita's transaction logs.
- **Potential Bug Focus:** Data consistency checks to prevent orphaned records or duplicate payments.

## 3. Database Interaction Strategy
- **Schema Export:** Regular exports of the database schema (tables, relationships) to track structural integrity.
- **Data Archival:** Monitoring of student records and academic results for long-term storage.

## 4. Security & Compliance
- **Authentication:** OAuth 2.0 / API Token Management for secure access.
- **Data Privacy:** Ensuring all data transmissions comply with NDPR standards.
