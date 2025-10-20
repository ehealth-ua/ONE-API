# Properties of `OTP-RPC.md` document

| Property | Value |
|----------|-------|
| Document type | RPC Method |
| Document name | DRAFT RPC OTP Verification |
| Guideline ID | GUI-0023 |
| Author | @Maksym Sokhatsky |
| Document version | v010 |
| Document status | DRAFT |
| Date of creation | 21.01.2025 |
| Date of update | 30.01.2025 |
| API ID | RPC-OTP-001 |
| Microservices (namespace) | otp_verification_api |
| Resource | Verification, SMSLog, VerifiedPhone |
| Scope | Init, Verify, Complete, Send |

## Purpose
The RPC methods in the OTP Verification service facilitate phone number verification and SMS management.
They provide functionality to initialize verification processes, complete verifications with OTP codes,
send SMS messages, and retrieve verified phone numbers. These methods ensure secure and
reliable OTP-based authentication, addressing business needs for user verification and communication.

## Logic
The RPC methods operate by interacting with the Core.Verification and Core.SMSLogs modules to
manage verification records and SMS logs. Each method performs specific operations:

- `verification_phone/1`: Retrieves a verified phone number from the database.
- `initialize/3`: Creates a new verification record for a phone number, optionally with a provider and SMS template.
- `complete/3`: Validates an OTP code against a phone number and updates the verification status.
- `send_sms/4`: Sends an SMS to a phone number with specified content, type, and provider, and logs the operation.

The methods validate inputs, interact with the database, and render responses in JSON format using dedicated views.

## Relationship between RPC Methods and API Methods

| API Method | Call Context | RPC Call Type |
|------------|--------------|---------------|
| GET /verifications/:phone_number | Retrieve verified phone number details | By Specific Condition |
| POST /verifications | Initialize a new verification for a phone number | By Specific Condition |
| PATCH /verifications/:phone_number/actions/complete | Complete verification with OTP code | By Specific Condition |
| POST /sms/send | Send an SMS to a phone number | By Specific Condition |

## Input parameters

| Input parameter | Values | Type | Description | Example |
|-----------------|--------|------|-------------|---------|
| phone_number | Valid phone number with country code | Binary | The phone number to verify or send SMS to | "+380960000000" |
| provider | Name of SMS provider (e.g., mouth_twilio, mouth_sms2ip, vodafone) | Binary | Optional provider for SMS sending or verification initialization | "mouth_twilio" |
| sms_template | Template identifier for SMS content | Binary | Optional template for initializing verification SMS | "welcome_template" |
| code | 4-digit OTP code | Integer | The OTP code to validate for verification completion | 1234 |
| content_hash | Hash of content for verification | Binary | Optional hash to validate verification context | "hash123" |
| body | SMS message content | Binary | The content of the SMS to be sent | "Your OTP is 123456" |
| type | SMS type identifier | Binary | The type of SMS (e.g., undefined, verification) | "undefined" |

## Output parameters

| Output parameter | Values | Type | Description | Example |
|------------------|--------|------|-------------|---------|
| phone_response | JSON object with phone number | Map | Contains the verified phone number | `%{phone_number: "+380960000000"}` |
| verification | JSON object with verification details | Map | Contains verification id, status, code expiration, and active state | `%{id: "53982ced-ed95-48a9-bab7-78247ec7259f", status: "new", code_expired_at: "2019-05-02T21:58:51.902086Z", active: true}` |
| sms | JSON object with SMS details | Map | Contains SMS id, phone number, body, and type | `%{id: "08600dea-f366-44e4-ad44-7111368f2209", phone_number: "+380960000000", body: "foo", type: "undefined"}` |

## Request structure
```elixir
# Example for initialize/3
OtpVerification.Rpc.initialize("+380960000000", "mouth_twilio", "welcome_template")

# Example for complete/3
OtpVerification.Rpc.complete("+380960000000", 123456, "hash123")

# Example for send_sms/4
OtpVerification.Rpc.send_sms("+380960000000", "Your OTP is 123456", "verification", "mouth_twilio")

# Example for verification_phone/1
OtpVerification.Rpc.verification_phone("+380960000000")
```

## Response structure
```elixir
# Example for initialize/3
{:ok, %{
  id: "53982ced-ed95-48a9-bab7-78247ec7259f",
  status: "new",
  code_expired_at: ~U[2019-05-02 21:58:51.902086Z],
  active: true
}}

# Example for complete/3
{:ok, %{
  id: "448c7356-1b69-4f4f-be70-d7e558b7cb09",
  status: "verified",
  code_expired_at: ~U[2019-08-07 00:00:00.000000Z],
  active: false
}}

# Example for send_sms/4
{:ok, %{
  id: "08600dea-f366-44e4-ad44-7111368f2209",
  phone_number: "+380960000000",
  body: "foo",
  type: "undefined"
}}

# Example for verification_phone/1
{:ok, %{phone_number: "+380960000000"}}
```

## Error Handling
- `:not_found` (404): Returned when a verified phone number or verification record is not found.
- `:too_many_requests` (429): Returned when the request rate limit is exceeded, with message "too many requests".
- `:service_unavailable` (503): Returned when the service is temporarily unavailable.
- `:forbidden` (403): Returned with a specific message when access is restricted.
- `:unprocessable_entity` (422): Returned when input validation fails, including JSON schema errors or invalid Ecto changeset, with details about the validation errors.

