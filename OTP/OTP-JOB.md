# Properties of a `OTP-JOB.md` document

| Property | Value |
|----------|-------|
| Document type | Job |
| Document title | DRAFT JOB OTP Verification Scheduler |
| Guideline ID | GUI-0037 |
| Author | @Maksym Sokhatskyi |
| Document version | v010 |
| Document status | DRAFT |
| Date of creation | 21.01.2025 |
| Date of update | 30.01.2025 |
| Microservices (namespace) | otp_verification_scheduler |
| ID JOB | JOB-010(otp_verification_scheduler-010) |

## Purpose
This job is designed to manage and automate the verification processes for OTP (One-Time Password) verifications.
It handles tasks such as updating SMS statuses, deactivating expired verifications,
terminating outdated verifications, and performing database maintenance through vacuum operations.
The job addresses technical challenges related to timely verification management, ensuring system reliability,
and optimizing database performance.

## Key points
- The job operates on a predefined schedule, managed by the Quantum scheduler, to execute tasks like SMS status updates, verification deactivation, and database cleanup.
- It interacts with multiple providers (e.g., Twilio, SMS2IP, Vodafone) to check SMS statuses, ensuring accurate updates to the system.
- Expired verifications are canceled or deleted based on configurable timeout parameters to maintain data consistency.
- The job uses ETS for counting SMS updates and logs operations for debugging and monitoring.
- Database vacuum operations are performed conditionally based on configuration to optimize database performance.

## Configuration
- [SMS Status Updater Configuration](https://e-health-ua.atlassian.net/wiki/spaces/DOCS/pages/17565614105)
- [Deactivator Configuration](https://e-health-ua.atlassian.net/wiki/spaces/DOCS/pages/17565614105)
- [Terminator Configuration](https://e-health-ua.atlassian.net/wiki/spaces/DOCS/pages/17565614105)
- [Vacuum Job Configuration](https://e-health-ua.atlassian.net/wiki/spaces/DOCS/pages/17565614105)

## Job logic

### Diagram (Optional)
A sequence diagram illustrating the job's workflow is available in SVG format at [LINK VIEW](https://e-health-ua.atlassian.net/wiki/spaces/EN/pages/17566859320). The diagram shows the interactions between the Scheduler.Worker, SmsStatusUpdater, Deactivator, Terminator, and VacuumJob modules, along with data flows to the database and external providers. The original diagram file is available in XML format at [draw.io link].

### Step description
| Step № | Step | Description | API methods used in the process |
|--------|------|-------------|-------------------------------|
| 1 | Initialize Scheduler | Starts the Scheduler.Application, which initializes the Supervisor with child processes (Counter and Worker). The Worker creates jobs based on configured schedules. | N/A |
| 2 | SMS Status Update | Collects SMS logs within the configured expiration time and updates their statuses by querying providers (Twilio, SMS2IP, Vodafone). Updates are logged, and a counter tracks processed SMS. | Primary.status/1, Secondary.status/1, Vodafone.status/1 |
| 3 | Deactivate Expired Verifications | Cancels expired verifications in the database based on predefined criteria. Logs the number of canceled records. | Verifications.cancel_expired_verifications/0 |
| 4 | Terminate Old Verifications | Deletes verifications older than the configured timeout period from the database. Logs the number of deleted records. | Repo.delete_all/1 |
| 5 | Vacuum Database | Performs VACUUM ANALYZE on specified OTP tables if enabled in the configuration to optimize database performance. Logs any errors encountered. | SQL.query/2 |

## Additional info
- Logs for SMS status updates can be filtered in Elastic using `request_id` to track specific operations, e.g., `request_id: 5539b7df-644b-410b-9bda-ef6c754036b9` for a specific verification.
- SMS status updates are filtered by gateway status (`accepted`, `enroute`, `unknown`, `pending`) and expiration time to avoid processing outdated records.
- The job ensures that SMS updates are only applied if the SMS record's insertion time is within the configured update timeout to prevent redundant updates.
- Errors during vacuum operations or datetime parsing are logged for debugging, with details including the table name or SMS ID.
- The job relies on configuration parameters fetched from the `:otp_verification_scheduler` application environment, such as `sms_statuses_expiration`, `sms_collect_timeout`, and `validations_expired_timeout`.

