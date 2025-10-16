# Properties of `OTP-DB-verified-phones.md` document

| Property | Value |
|----------|-------|
| Document type | SQL Database Info |
| Document title | DRAFT PostgreSQL DB: verified_phones table / Таблиця бази даних PostgreSQL |
| Guideline ID | GUI-0017 |
| Author | @Maksym Sokhatskyi |
| Document version | v010 |
| Document status | DRAFT |
| Date of creation | 21.01.2025 |
| Date of update | 30.01.2025 |
| Table name | otp_verification.verified_phones |
| Purpose | The `verified_phones` table stores phone numbers that have been successfully verified through the OTP verification process, ensuring secure user authentication. |
| DB ID | PostgreSQL.otp_verification |
| Primary key (PK) | phone_number |
| HL7 version | N/A |

## Table fields

| Nesting level | Attribute name | Description EN | Description UA | M/O | Type | HL7 vs eHealth comparison result |
|---------------|----------------|----------------|----------------|-----|------|---------------------------------|
| 1 | phone_number | Phone number that has been verified | Верифікований номер телефону | M | text | N/A |
| 1 | inserted_at | Timestamp when the record was created | Мітка часу створення запису | M | timestamp | N/A |
| 1 | updated_at | Timestamp when the record was last updated | Мітка часу останнього оновлення запису | M | timestamp | N/A |

## Indexes (optional)

| Name | Index attributes |
|------|------------------|
| verified_phones_phone_number_idx | phone_number |

## Foreign indexes (optional)

| Name | Type |
|------|------|
| N/A | N/A |

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
| phone_number | phone_number | 1:1 | otp_verification.verifications |
| phone_number | phone_number | 1:∞ | otp_verification.sms_logs |

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
- [GET /verifications/:phone_number](https://e-health-ua.atlassian.net/wiki/)
- [POST /verifications](https://e-health-ua.atlassian.net/wiki/)
- [PATCH /verifications/:phone_number/actions/complete](https://e-health-ua.atlassian.net/wiki/)
- [POST /sms/send](https://e-health-ua.atlassian.net/wiki/)

### Business processes that are associated with the table, components, access points
- [Phone Number Verification Process](https://e-health-ua.atlassian.net/wiki/)
- [SMS Sending and Status Update Process](https://e-health-ua.atlassian.net/wiki/)