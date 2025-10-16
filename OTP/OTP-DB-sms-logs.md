# Properties of `OTP-DB-sms-logs.md` document

| Property | Value |
|----------|-------|
| Document type | SQL Database Info |
| Document title | DRAFT PostgreSQL DB: sms_logs table / Таблиця бази даних PostgreSQL |
| Guideline ID | GUI-0017 |
| Author | @Maksym Sokhatskyi |
| Document version | v010 |
| Document status | DRAFT |
| Date of creation | 21.01.2025 |
| Date of update | 30.01.2025 |
| Table name | otp_verification.sms_logs |
| Purpose | The `sms_logs` table stores records of SMS messages sent as part of the OTP verification process, including message content, provider details, and status information. |
| DB ID | PostgreSQL.otp_verification |
| Primary key (PK) | id |
| HL7 version | N/A |

## Table fields

| Nesting level | Attribute name | Description EN | Description UA | M/O | Type | HL7 vs eHealth comparison result |
|---------------|----------------|----------------|----------------|-----|------|---------------------------------|
| 1 | id | Unique identifier for the SMS log record | Унікальний ідентифікатор запису логу SMS | M | uuid | N/A |
| 1 | phone_number | Phone number to which the SMS was sent | Номер телефону, на який відправлено SMS | M | text | N/A |
| 1 | body | Content of the SMS message | Вміст SMS-повідомлення | M | text | N/A |
| 1 | type | Type of SMS (e.g., verification, undefined) | Тип SMS (наприклад, верифікація, невизначений) | M | text | N/A |
| 1 | provider | SMS provider used (e.g., mouth_twilio, mouth_sms2ip, vodafone) | Провайдер SMS (наприклад, mouth_twilio, mouth_sms2ip, vodafone) | O | text | N/A |
| 1 | gateway_id | Identifier of the SMS in the provider's system | Ідентифікатор SMS у системі провайдера | O | text | N/A |
| 1 | gateway_status | Status of the SMS in the provider's system (e.g., accepted, enroute, terminated) | Статус SMS у системі провайдера (наприклад, прийнято, в дорозі, завершено) | O | text | N/A |
| 1 | status_changed_at | Timestamp when the SMS status was last updated | Мітка часу останнього оновлення статусу SMS | O | timestamp | N/A |
| 1 | inserted_at | Timestamp when the record was created | Мітка часу створення запису | M | timestamp | N/A |
| 1 | updated_at | Timestamp when the record was last updated | Мітка часу останнього оновлення запису | M | timestamp | N/A |
| 1 | verification_id | Identifier of the associated verification record | Ідентифікатор пов'язаного запису верифікації | O | uuid | N/A |

## Indexes (optional)

| Name | Index attributes |
|------|------------------|
| sms_logs_phone_number_idx | phone_number |
| sms_logs_verification_id_idx | verification_id |

## Foreign indexes (optional)

| Name | Type |
|------|------|
| sms_logs_verification_id_fkey | Foreign Key (references otp_verification.verifications(id)) |

## Triggers (optional)

| Name | Description |
|------|-------------|
| N/A | N/A |

## Procedures (optional)

| Name | Description |
|------|-------------|
| N/A | N/A |

## Replications (optional)

| Database.Table | List of attributes (fields) |
|----------------|----------------------------|
| N/A | N/A |

## Related tables

| Attribute (field) of the current table | Attribute (field) of the target table | Relationship type | Database.Target table |
|---------------------------------------|--------------------------------------|-------------------|-----------------------|
| verification_id | id | ∞:1 | otp_verification.verifications |
| phone_number | phone_number | ∞:1 | otp_verification.verified_phones |

## Links to documentation that can create or modify a database object
- [OTP Verification RPC Methods](https://e-health-ua.atlassian.net/wiki/)
- [OTP Verification Scheduler Job](https://e-health-ua.atlassian.net/wiki/)

### Database type
PostgreSQL

### List of tables
- otp_verification.verifications
- otp_verification.verified_phones
- otp_verification.sms_logs

### System component (repository)
otp_verification_api

### http API endpoint
- [POST /sms/send](https://e-health-ua.atlassian.net/wiki/)
- [GET /verifications/:phone_number](https://e-health-ua.atlassian.net/wiki/)
- [POST /verifications](https://e-health-ua.atlassian.net/wiki/)
- [PATCH /verifications/:phone_number/actions/complete](https://e-health-ua.atlassian.net/wiki/)

### Business processes that are associated with the table, components, access points
- [Phone Number Verification Process](https://e-health-ua.atlassian.net/wiki/)
- [SMS Sending and Status Update Process](https://e-health-ua.atlassian.net/wiki/)