# Properties of a Job document

## Document type
Job

## Document title
DRAFT JOB Person Updates Publisher

## Guideline ID
GUI-0037

## Author
@Kateryna Yakovleva

## Document version
v010

## Document status
DRAFT

## Date of creation
21.01.2025

## Date of update
30.01.2025

## Microservices (namespace)
person_updates_producer

## ID JOB
JOB-010(person_updates_producer-010)

## Purpose
This job is designed to publish updates to person records in the MPI to a Kafka topic for synchronization and event-driven processing. It addresses the need for real-time notification of changes in person data, ensuring consistency across systems and enabling downstream services to react to updates.

## Key points
- The job runs on a scheduled basis using Quantum scheduler to fetch and publish person updates.
- It queries the database for person updates and publishes events to Kafka with details like status, verification status, and death date.
- Dependencies include Kafka producer and the MPI database.
- Configurable parameters include the Kafka topic and schedule.
- Logs the publication of events for monitoring.

## Configuration
- [Person Updates Publisher Configuration](https://e-health-ua.atlassian.net/wiki/spaces/DOCS/pages/17565614105)

## Job logic

### Diagram (Optional)
A sequence diagram illustrating the job's workflow is available in SVG format at [LINK VIEW](https://e-health-ua.atlassian.net/wiki/spaces/EN/pages/17566859320). The diagram shows interactions between the Worker, Publisher, and Kafka. The original diagram file is available in XML format at [draw.io link].

### Step description
| Step № | Step | Description | API methods used in the process |
|--------|------|-------------|-------------------------------|
| 1 | Initialize Scheduler | Starts the application and creates scheduled jobs using Quantum. | N/A |
| 2 | Fetch Person Updates | Queries the database for person updates based on criteria like updated_date. | Repo.all/1 |
| 3 | Publish Events | For each update, constructs an event map and produces it to the Kafka topic. | Producer.produce_sync/4 |
| 4 | Log Publication | Logs the successful publication of events. | Logger.info/1 |

## Additional info
- Events are published to the 'person_events' Kafka topic.
- The job handles optional preperson data in the event.
- Configuration is fetched from the :person_updates_producer application environment.
- Errors in publishing are handled by the Kafka producer.