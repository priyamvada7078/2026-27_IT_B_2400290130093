# Software Requirements Specification
## Weather-Based Crop Advisory System
**Version 1.0 Approved**

| Field          | Details                          |
|----------------|----------------------------------|
| Prepared by    | Priyamvada, Ishant, Naitik       |
| Organization   | IT Department — Batch B (2026–27)|
| Repository     | 2026-27_IT_B_2400290130093       |
| Date Created   | 2026                             |

---

## Revision History

| Name       | Date  | Reason For Changes      | Version |
|------------|-------|-------------------------|---------|
| Priyamvada | 2026  | Initial draft created   | 1.0     |

---

## Table of Contents

1. [Introduction](#1-introduction)
   - 1.1 Purpose
   - 1.2 Document Conventions
   - 1.3 Intended Audience and Reading Suggestions
   - 1.4 Product Scope
   - 1.5 References
2. [Overall Description](#2-overall-description)
   - 2.1 Product Perspective
   - 2.2 Product Functions
   - 2.3 User Classes and Characteristics
   - 2.4 Operating Environment
   - 2.5 Design and Implementation Constraints
   - 2.6 User Documentation
   - 2.7 Assumptions and Dependencies
3. [External Interface Requirements](#3-external-interface-requirements)
   - 3.1 User Interfaces
   - 3.2 Hardware Interfaces
   - 3.3 Software Interfaces
   - 3.4 Communications Interfaces
4. [System Features](#4-system-features)
5. [Other Nonfunctional Requirements](#5-other-nonfunctional-requirements)
6. [Other Requirements](#6-other-requirements)
- Appendix A: Glossary
- Appendix B: Analysis Models
- Appendix C: To Be Determined List

---

## 1. Introduction

### 1.1 Purpose

This Software Requirements Specification (SRS) document describes the functional and non-functional requirements for the **Weather-Based Crop Advisory System**, Version 1.0. The system provides farmers with localised, real-time, weather-driven crop advisories — including irrigation timing, sowing windows, and frost/heat/spray warnings — delivered via a web dashboard and SMS alerts on a fully serverless AWS architecture.

This document is intended to serve as the authoritative reference for design, development, testing, and validation of the system.

### 1.2 Document Conventions

- **SHALL** — indicates a mandatory requirement.
- **SHOULD** — indicates a recommended but non-mandatory requirement.
- **REQ-F-XX** — prefix used for functional requirements.
- **REQ-NF-XX** — prefix used for non-functional requirements.
- Higher-level requirements are inherited by their sub-requirements unless explicitly overridden.
- Priority levels used: **High**, **Medium**, **Low**.

### 1.3 Intended Audience and Reading Suggestions

| Reader              | Relevant Sections              |
|---------------------|-------------------------------|
| Developers          | All sections, especially 3 & 4 |
| Project Managers    | Sections 1, 2, 5               |
| Testers             | Sections 4, 5                  |
| Stakeholders/Farmers| Sections 1.4, 2.2, 2.3         |
| Documentation Writers | All sections                 |

It is recommended to read sections in order: Introduction → Overall Description → System Features → Nonfunctional Requirements.

### 1.4 Product Scope

The **Weather-Based Crop Advisory System** is a cloud-native AgriTech platform that addresses the challenge of unpredictable weather impacting farmer decisions. The system:

- Ingests real-time weather data via external weather APIs.
- Runs an advisory engine to generate crop-specific recommendations.
- Delivers advisories via a web dashboard (for smartphone users) and SMS (for feature-phone users).
- Provides administrators with a monitoring and management panel.

**Business Goal:** Reduce crop losses caused by poor weather-informed decisions, improve farm productivity, and make precision agriculture accessible to smallholder farmers.

### 1.5 References

| Document                          | Source                                      |
|-----------------------------------|---------------------------------------------|
| AWS Lambda Documentation          | https://docs.aws.amazon.com/lambda          |
| AWS Cognito Documentation         | https://docs.aws.amazon.com/cognito         |
| AWS SNS Documentation             | https://docs.aws.amazon.com/sns             |
| AWS DynamoDB Documentation        | https://docs.aws.amazon.com/dynamodb        |
| OpenWeatherMap API Documentation  | https://openweathermap.org/api              |
| Experiment 1 — Project Setup      | 2026-27_IT_B_2400290130093 GitHub Repo      |
| Experiment 2 — Feasibility Study  | 2026-27_IT_B_2400290130093 GitHub Repo      |
| Experiment 3 — Requirement Report | 2026-27_IT_B_2400290130093 GitHub Repo      |

---

## 2. Overall Description

### 2.1 Product Perspective

The Weather-Based Crop Advisory System is a new, self-contained product in the AgriTech domain. It integrates with:

- **External Weather APIs** (e.g., OpenWeatherMap) for real-time weather data ingestion.
- **AWS Cloud Services** for compute, storage, messaging, and authentication.
- **Farmer mobile devices** via SMS (AWS SNS) and a web browser dashboard hosted on S3/CloudFront.

The system is composed of four independently deployable microservices:

```
┌─────────────────────────────────────────────────────────┐
│                   Farmer / Admin (Browser / SMS)        │
└────────────────────────┬────────────────────────────────┘
                         │
              ┌──────────▼──────────┐
              │   API Gateway       │
              └──────────┬──────────┘
       ┌─────────────────┼──────────────────┐
       ▼                 ▼                  ▼
┌─────────────┐  ┌──────────────┐  ┌──────────────────┐
│ Farmer      │  │ Weather      │  │ Advisory         │
│ Service     │  │ Service      │  │ Engine           │
│ (Cognito,   │  │ (Lambda,     │  │ (Lambda,         │
│  DynamoDB)  │  │  EventBridge)│  │  DynamoDB)       │
└─────────────┘  └──────────────┘  └──────────────────┘
                                          │
                                   ┌──────▼──────┐
                                   │ Alert       │
                                   │ Service     │
                                   │ (SNS, Admin)│
                                   └─────────────┘
```

### 2.2 Product Functions

- **Farmer Authentication** — Secure registration and login via AWS Cognito.
- **Profile Management** — Farmers set crop type, location, and alert preferences.
- **Weather Ingestion** — Automated ingestion of real-time weather data via scheduled Lambda and EventBridge.
- **Advisory Generation** — Engine processes weather data and generates irrigation, sowing, frost, heat, and spray advisories.
- **SMS Alert Delivery** — Time-sensitive warnings delivered via AWS SNS to farmer mobile numbers.
- **Web Dashboard** — Farmers view daily advisories on a responsive web interface hosted on S3/CloudFront.
- **Admin Panel** — Administrators monitor system health, manage users, and configure advisory rules.

### 2.3 User Classes and Characteristics

| User Class          | Description                                                                                   | Technical Expertise |
|---------------------|-----------------------------------------------------------------------------------------------|---------------------|
| Smallholder Farmer  | Primary user; receives SMS advisories; may not have internet access; uses basic mobile phone  | Low                 |
| Progressive Farmer  | Uses web dashboard; comfortable with smartphones; wants detailed weather trends               | Medium              |
| Senior Farmer       | Needs simplified language; receives SMS alerts only; may need assistance with app             | Very Low            |
| AgriTech Admin      | Manages system, users, advisory rules; monitors AWS infrastructure                            | High                |

### 2.4 Operating Environment

| Component           | Environment                                                              |
|---------------------|--------------------------------------------------------------------------|
| Cloud Platform      | AWS (Lambda, DynamoDB, Cognito, SNS, S3, CloudFront, API Gateway, EventBridge) |
| Web Dashboard       | Any modern browser (Chrome, Firefox, Safari) on desktop or smartphone    |
| SMS Delivery        | Any mobile network; GSM-compatible devices                               |
| Backend Runtime     | Node.js / Python on AWS Lambda                                           |
| Database            | AWS DynamoDB (NoSQL)                                                     |
| CI/CD               | GitHub Actions                                                           |

### 2.5 Design and Implementation Constraints

- The system **SHALL** be fully serverless; no dedicated EC2 instances or on-premise servers.
- All backend services **SHALL** be implemented as AWS Lambda functions.
- Authentication **SHALL** use AWS Cognito only; no custom auth implementation.
- SMS delivery **SHALL** use AWS SNS; third-party SMS gateways are out of scope.
- The advisory engine **SHALL** process weather data and dispatch alerts within **5 minutes** of an event trigger.
- All data at rest **SHALL** be stored in DynamoDB; relational databases are out of scope.
- The frontend **SHALL** be a static web application hosted on S3 with CloudFront distribution.
- Development **SHALL** follow Git-based branching strategy with pull requests on GitHub.

### 2.6 User Documentation

| Document                  | Format        | Delivery Method        |
|---------------------------|---------------|------------------------|
| Farmer Quick-Start Guide  | PDF / Web     | Linked from dashboard  |
| SMS Alert Format Guide    | Plain text    | Delivered with first SMS |
| Admin Panel User Manual   | Web (HTML)    | Accessible in admin panel |
| API Documentation         | Markdown      | GitHub repository      |

### 2.7 Assumptions and Dependencies

**Assumptions:**
- Farmers have access to a mobile phone capable of receiving SMS messages.
- External weather API (e.g., OpenWeatherMap) remains available and provides accurate data.
- AWS services remain available in the selected deployment region.
- Advisory logic is rule-based for Version 1.0; ML-based advisories are a future enhancement.

**Dependencies:**

| Dependency             | Type      | Details                                             |
|------------------------|-----------|-----------------------------------------------------|
| OpenWeatherMap API     | External  | Real-time weather data source                       |
| AWS Cognito            | Cloud     | Farmer authentication and session management        |
| AWS SNS                | Cloud     | SMS alert delivery to farmer mobile numbers         |
| AWS EventBridge        | Cloud     | Scheduled triggering of weather ingestion Lambda    |
| GitHub Actions         | DevOps    | CI/CD pipeline for automated deployment             |

---

## 3. External Interface Requirements

### 3.1 User Interfaces

**Web Dashboard (Farmer):**
- Responsive single-page application (SPA) accessible via modern browsers.
- Home screen displays today's advisory cards: irrigation, sowing window, and active warnings.
- Profile page allows farmers to update crop type, location, and SMS preference.
- Navigation: minimal top bar with Home, Profile, and Logout.
- Error messages displayed inline, clearly worded in plain English.

**Admin Panel:**
- Separate secured web interface accessible only to admin users.
- Displays active farmer count, recent alerts dispatched, system health metrics.
- Allows administrators to add/remove advisory rules and manage users.

### 3.2 Hardware Interfaces

- No dedicated hardware components are required.
- The system operates entirely on AWS cloud infrastructure.
- Farmer-side: any GSM mobile phone (for SMS) or a device with a browser (for dashboard).

### 3.3 Software Interfaces

| Interface                  | Version / Details                        | Purpose                                          |
|----------------------------|------------------------------------------|--------------------------------------------------|
| OpenWeatherMap API         | Current v2.5 / v3.0                      | Fetch real-time and forecast weather data        |
| AWS Lambda                 | Node.js 18.x / Python 3.11 runtime       | Execute backend microservice logic               |
| AWS DynamoDB               | Latest                                   | Store farmer profiles, weather data, advisories  |
| AWS Cognito User Pools     | Latest                                   | Manage farmer registration and authentication    |
| AWS SNS                    | Latest                                   | Dispatch SMS alerts to farmer mobile numbers     |
| AWS EventBridge            | Latest                                   | Schedule periodic weather ingestion triggers     |
| AWS S3 + CloudFront        | Latest                                   | Host and serve the static web dashboard          |
| AWS API Gateway            | REST API / HTTP API                      | Expose backend Lambda functions as HTTP endpoints|

### 3.4 Communications Interfaces

- All API communication between the frontend and backend **SHALL** use **HTTPS** (TLS 1.2 or higher).
- Weather data is fetched from the external API over **HTTPS REST**.
- SMS messages are dispatched via **AWS SNS** using the E.164 phone number format.
- Authentication tokens issued by **AWS Cognito** use the **JWT (JSON Web Token)** standard.
- EventBridge schedules use **cron expressions** to trigger Lambda at defined intervals (e.g., every hour).

---

## 4. System Features

### 4.1 Farmer Authentication and Profile Management

#### 4.1.1 Description and Priority
Allows farmers to register, log in, and manage their profile including crop type, farm location, and SMS alert preferences. **Priority: High**

#### 4.1.2 Stimulus/Response Sequences
- Farmer opens the web dashboard → system displays login/registration page.
- Farmer registers with name, mobile number, and password → AWS Cognito creates account → confirmation SMS sent.
- Farmer logs in with credentials → Cognito issues JWT token → dashboard home loaded.
- Farmer updates profile → system saves to DynamoDB → advisory engine uses updated data on next run.

#### 4.1.3 Functional Requirements

| ID       | Requirement                                                                                   |
|----------|-----------------------------------------------------------------------------------------------|
| REQ-F-01 | The system SHALL allow farmers to register using name, mobile number, and password.           |
| REQ-F-02 | The system SHALL authenticate farmers using AWS Cognito with JWT-based session tokens.        |
| REQ-F-03 | The system SHALL allow farmers to update crop type, farm location, and SMS preference.        |
| REQ-F-04 | The system SHALL lock an account after 5 consecutive failed login attempts.                   |
| REQ-F-05 | The system SHALL allow farmers to reset their password via OTP sent to registered mobile.     |

---

### 4.2 Weather Data Ingestion

#### 4.2.1 Description and Priority
Automates periodic fetching of real-time and forecast weather data from the external weather API for all registered farm locations. **Priority: High**

#### 4.2.2 Stimulus/Response Sequences
- EventBridge triggers the Weather Ingestion Lambda every hour.
- Lambda fetches weather data for all active farm locations from OpenWeatherMap API.
- Fetched data is stored in DynamoDB.
- Advisory Engine Lambda is triggered upon successful ingestion.

#### 4.2.3 Functional Requirements

| ID       | Requirement                                                                                          |
|----------|------------------------------------------------------------------------------------------------------|
| REQ-F-06 | The system SHALL automatically ingest weather data every hour using EventBridge scheduled triggers.  |
| REQ-F-07 | The system SHALL fetch current weather and 24-hour forecast for each registered farm location.       |
| REQ-F-08 | The system SHALL store ingested weather data in DynamoDB with a timestamp and location key.          |
| REQ-F-09 | The system SHALL handle API failures gracefully and retry ingestion up to 3 times before logging error. |

---

### 4.3 Advisory Engine

#### 4.3.1 Description and Priority
Processes ingested weather data and generates crop-specific advisories for each farmer — covering irrigation timing, sowing windows, and weather warnings (frost, heat, spray). **Priority: High**

#### 4.3.2 Stimulus/Response Sequences
- Weather ingestion completes → Advisory Engine Lambda is triggered.
- Engine reads latest weather data from DynamoDB.
- Engine applies rule-based logic per crop type and location.
- Generated advisories are stored in DynamoDB and flagged for delivery.

#### 4.3.3 Functional Requirements

| ID       | Requirement                                                                                               |
|----------|-----------------------------------------------------------------------------------------------------------|
| REQ-F-10 | The system SHALL generate irrigation advisories based on soil moisture approximation and rainfall forecast.|
| REQ-F-11 | The system SHALL generate sowing window recommendations based on temperature and rainfall forecast.        |
| REQ-F-12 | The system SHALL generate frost warnings when forecast temperature drops below 2°C.                       |
| REQ-F-13 | The system SHALL generate heat warnings when forecast temperature exceeds 40°C.                           |
| REQ-F-14 | The system SHALL generate spray advisories when wind speed is below 15 km/h and no rain is forecast.     |
| REQ-F-15 | Advisories SHALL be crop-type-specific based on the farmer's registered crop.                             |

---

### 4.4 SMS Alert Delivery

#### 4.4.1 Description and Priority
Delivers time-sensitive weather warnings and daily advisory summaries to farmers via SMS using AWS SNS. **Priority: High**

#### 4.4.2 Stimulus/Response Sequences
- Advisory Engine flags a warning advisory (frost/heat/spray) → Alert Service Lambda triggered.
- Lambda formats advisory as concise SMS message.
- SMS dispatched via AWS SNS to farmer's registered mobile number.
- Delivery status logged in DynamoDB.

#### 4.4.3 Functional Requirements

| ID       | Requirement                                                                                      |
|----------|--------------------------------------------------------------------------------------------------|
| REQ-F-16 | The system SHALL dispatch SMS alerts for frost, heat, and spray warnings within 5 minutes of detection. |
| REQ-F-17 | The system SHALL send a daily advisory summary SMS to each farmer before 6:00 AM local time.    |
| REQ-F-18 | SMS messages SHALL be concise (under 160 characters) and written in plain, actionable language. |
| REQ-F-19 | The system SHALL log SMS delivery status (delivered/failed) in DynamoDB.                        |
| REQ-F-20 | Farmers SHALL be able to opt out of SMS alerts from their profile settings.                     |

---

### 4.5 Web Dashboard

#### 4.5.1 Description and Priority
A responsive web interface where farmers can view their daily advisories, weather summary, and account profile. **Priority: Medium**

#### 4.5.2 Stimulus/Response Sequences
- Farmer logs in → dashboard loads advisory cards for today.
- Farmer clicks on an advisory card → expanded details shown.
- Farmer navigates to Profile page → updates crop type or location → changes saved.

#### 4.5.3 Functional Requirements

| ID       | Requirement                                                                                   |
|----------|-----------------------------------------------------------------------------------------------|
| REQ-F-21 | The dashboard SHALL display today's irrigation, sowing, and warning advisories as cards.      |
| REQ-F-22 | The dashboard SHALL display a 24-hour weather summary for the farmer's registered location.   |
| REQ-F-23 | The dashboard SHALL be responsive and usable on mobile browsers with screen widths ≥ 360px.  |
| REQ-F-24 | The dashboard SHALL load advisory data within 3 seconds on a standard mobile connection.      |

---

### 4.6 Admin Panel

#### 4.6.1 Description and Priority
A secured interface for administrators to monitor system health, manage farmers, and configure advisory rules. **Priority: Medium**

#### 4.6.2 Stimulus/Response Sequences
- Admin logs in with admin credentials → admin panel dashboard loaded.
- Admin views active farmer count, SMS alerts sent today, and system errors.
- Admin updates advisory threshold rules → changes saved and applied to next advisory run.

#### 4.6.3 Functional Requirements

| ID       | Requirement                                                                                       |
|----------|---------------------------------------------------------------------------------------------------|
| REQ-F-25 | The admin panel SHALL display the total number of registered farmers and active sessions.         |
| REQ-F-26 | The admin panel SHALL display a log of SMS alerts dispatched in the last 24 hours.               |
| REQ-F-27 | The admin panel SHALL allow administrators to enable or disable farmer accounts.                  |
| REQ-F-28 | The admin panel SHALL allow administrators to configure advisory threshold values (e.g., frost temperature trigger). |

---

## 5. Other Nonfunctional Requirements

### 5.1 Performance Requirements

| ID        | Requirement                                                                                        |
|-----------|----------------------------------------------------------------------------------------------------|
| REQ-NF-01 | Advisory generation and SMS dispatch SHALL complete within 5 minutes of a weather trigger event.  |
| REQ-NF-02 | The web dashboard SHALL load within 3 seconds on a 4G mobile connection.                          |
| REQ-NF-03 | The system SHALL support up to 10,000 registered farmers without degradation in performance.       |
| REQ-NF-04 | Weather ingestion Lambda SHALL complete execution within 30 seconds per invocation.               |

### 5.2 Safety Requirements

- The system SHALL NOT make irreversible decisions on behalf of farmers (all advisories are recommendations only).
- In case of weather API unavailability, the system SHALL notify the admin and SHALL NOT dispatch advisories based on stale data older than 3 hours.
- System errors SHALL be logged to AWS CloudWatch and SHALL trigger admin alerts for critical failures.

### 5.3 Security Requirements

| ID        | Requirement                                                                                         |
|-----------|-----------------------------------------------------------------------------------------------------|
| REQ-NF-05 | All API endpoints SHALL be protected by AWS Cognito JWT authentication.                            |
| REQ-NF-06 | All data in transit SHALL be encrypted using TLS 1.2 or higher.                                    |
| REQ-NF-07 | Farmer personally identifiable information (PII) SHALL be stored encrypted in DynamoDB.            |
| REQ-NF-08 | Admin panel access SHALL be restricted to users with the `admin` Cognito group role.               |
| REQ-NF-09 | The system SHALL enforce account lockout after 5 consecutive failed login attempts.                |

### 5.4 Software Quality Attributes

| Attribute       | Target                                                                               |
|-----------------|--------------------------------------------------------------------------------------|
| Availability    | 99.9% uptime ensured by serverless AWS infrastructure                                |
| Reliability     | Automatic Lambda retries on failure; DynamoDB multi-AZ replication                  |
| Maintainability | Modular microservices (farmer, weather, advisory, alert) — independent deployability |
| Scalability     | Serverless auto-scaling supports growth from hundreds to millions of farmers         |
| Usability       | SMS-first design ensures access for farmers with no internet; minimal dashboard UI   |
| Testability     | Each Lambda function is independently unit-testable; GitHub Actions runs CI tests    |

### 5.5 Business Rules

- A farmer MUST complete profile setup (crop type + location) before receiving advisories.
- Advisories are generated per registered farm location — one profile per mobile number.
- SMS alerts for warnings (frost/heat/spray) take priority over daily summary delivery.
- Admin users CANNOT receive crop advisories; their role is restricted to system management.
- Advisory data older than 30 days SHALL be archived and removed from active DynamoDB tables.

---

## 6. Other Requirements

- **Internationalisation:** Version 1.0 supports English only. Regional language support (Hindi, Marathi, etc.) is planned for Version 2.0.
- **Legal / Compliance:** Farmer mobile numbers and personal data SHALL be handled in compliance with applicable data protection regulations.
- **Cost Management:** All AWS resources SHALL be tagged with project and environment identifiers for cost tracking and billing allocation.
- **Logging:** All Lambda invocations SHALL produce structured logs in AWS CloudWatch for debugging and audit purposes.

---

## Appendix A: Glossary

| Term              | Definition                                                                           |
|-------------------|--------------------------------------------------------------------------------------|
| Advisory          | A crop-specific recommendation generated by the system based on weather data         |
| AWS Cognito       | AWS service for user authentication and access management                            |
| AWS DynamoDB      | AWS fully managed NoSQL database service                                             |
| AWS EventBridge   | AWS serverless event bus for scheduling and routing events                           |
| AWS Lambda        | AWS serverless compute service that runs code in response to events                  |
| AWS SNS           | Amazon Simple Notification Service; used for SMS delivery                            |
| CloudFront        | AWS content delivery network (CDN) for serving the web dashboard globally            |
| JWT               | JSON Web Token; used for stateless authentication                                    |
| SRS               | Software Requirements Specification                                                  |
| Serverless        | Cloud architecture where infrastructure management is abstracted away by the provider|
| Sowing Window     | Optimal period for planting a crop based on weather forecast                         |
| TLS               | Transport Layer Security; encryption protocol for data in transit                    |

---

## Appendix B: Analysis Models

**System Context Diagram (Text Representation):**

```
[Farmer] ──── SMS / Web Dashboard ────► [Weather-Based Crop Advisory System]
                                                        │
                               ┌────────────────────────┼──────────────────────┐
                               ▼                        ▼                      ▼
                    [OpenWeatherMap API]       [AWS Cloud Services]       [Admin Panel]
                    (External Weather Data)    (Lambda, DynamoDB,         (AgriTech Admin)
                                               Cognito, SNS, S3)
```

**Key Data Flows:**
- Weather API → Weather Ingestion Lambda → DynamoDB → Advisory Engine → Alert Service → SMS (Farmer)
- Farmer → Web Dashboard → API Gateway → Lambda → DynamoDB

---

## Appendix C: To Be Determined List

| TBD ID | Description                                                                 | Target Resolution |
|--------|-----------------------------------------------------------------------------|-------------------|
| TBD-01 | Final selection of weather API provider (OpenWeatherMap vs. WeatherAPI)     | Experiment 5      |
| TBD-02 | Regional language support specification for SMS advisories                  | Version 2.0       |
| TBD-03 | Specific DynamoDB table partition and sort key schema for advisory records  | Experiment 6      |
| TBD-04 | ML-based advisory model design (planned for future version)                 | Version 2.0       |
