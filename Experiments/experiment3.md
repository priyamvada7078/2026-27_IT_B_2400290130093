# Experiment 3 — Software Design Principles: Requirement Elicitation

## Aim

To identify stakeholders and perform requirement elicitation for the Weather-Based Crop Advisory System using suitable elicitation techniques, prepare user stories, and develop a Requirement Gathering Report.

---

## Objectives

- Identify key stakeholders of the Weather-Based Crop Advisory System.
- Apply requirement elicitation techniques.
- Gather functional and non-functional requirements.
- Prepare user stories with acceptance criteria.
- Document the Requirement Gathering Report.

---

## Introduction

Requirement elicitation is the process of discovering stakeholder needs and expectations. The quality of software depends on how accurately user requirements are captured. Common elicitation techniques include interviews, questionnaires, observation, workshops, and user personas.

---

## Selected Project

| Field             | Details                              |
|-------------------|--------------------------------------|
| **Project Title** | Weather-Based Crop Advisory System   |
| **Domain**        | Agriculture / AgriTech               |

---

## Stakeholder Identification

| Stakeholder        | Role                                          | Requirements                                               |
|--------------------|-----------------------------------------------|------------------------------------------------------------|
| Farmer             | Primary end-user of advisories and SMS alerts | Simple interface, timely and accurate crop advisories      |
| AgriTech Admin     | Manages system, users, and advisory rules     | Admin panel, monitoring dashboard, user management         |
| Weather Data Provider | Supplies real-time weather feeds           | Reliable API integration and data accuracy                 |
| AWS Cloud Platform | Hosts all backend services (Lambda, DynamoDB, SNS, etc.) | High availability, scalability, and secure data handling |

---

## Requirement Elicitation Techniques

| Technique      | Purpose                                           | Outcome                                          |
|----------------|---------------------------------------------------|--------------------------------------------------|
| Interview      | Discuss farming challenges with stakeholders      | Detailed functional requirements                 |
| Questionnaire  | Collect feedback from farmers across regions      | User expectations on alerts and usability        |
| Observation    | Observe how farmers use mobile/SMS-based tools    | Usability and workflow requirements              |
| User Persona   | Model representative farmer profiles              | User-centred, accessible design requirements     |

---

## Sample Requirement Gathering

### Interview Findings
- Farmers need advisories in simple, regional-language-friendly language.
- SMS alerts must be concise and actionable (e.g., "Irrigate tomorrow morning, rain expected by evening").
- Advisories should be crop-specific, not generic weather reports.
- Farmers want frost and heat-wave warnings at least 24 hours in advance.

### Observation Findings
- Most farmers use basic smartphones or feature phones — SMS delivery is essential.
- Dashboard navigation must be minimal with large text and icons.
- Farmers check advisories early morning before starting field work.

### Questionnaire Findings
- Over 80% of surveyed farmers cited unpredictable weather as their top challenge.
- Farmers expect alerts to arrive before 6:00 AM.
- Security of personal farm data is a concern for a significant portion of users.

---

## User Personas

| Persona           | Age | Goal                                           | Pain Point                                      |
|-------------------|-----|------------------------------------------------|-------------------------------------------------|
| Smallholder Farmer | 38 | Get daily irrigation and sowing advisories     | No internet access, relies only on SMS          |
| Progressive Farmer | 45 | Monitor weather trends via web dashboard       | Too much raw data, needs summarised advisories  |
| Senior Farmer      | 62 | Receive frost/heat warnings in simple language | Complex apps are difficult to navigate          |
| AgriTech Admin     | 30 | Monitor system health and manage advisory rules | Needs a clear admin panel with logs and alerts |

---

## User Stories

| ID  | User Story                                                                                               | Acceptance Criteria                                                                 |
|-----|----------------------------------------------------------------------------------------------------------|-------------------------------------------------------------------------------------|
| US1 | As a farmer, I want to register and log in securely so that only I can access my crop advisory profile. | Authentication via AWS Cognito works correctly and passes functional testing.        |
| US2 | As a farmer, I want to receive an SMS alert when frost or heat risk is detected for my location.         | SMS delivered via AWS SNS within 5 minutes of weather trigger; passes functional testing. |
| US3 | As a farmer, I want to view today's irrigation advisory on the web dashboard so I can plan my day.       | Dashboard displays correct advisory based on latest weather data; passes testing.   |
| US4 | As a farmer, I want to receive a sowing window recommendation based on upcoming rainfall forecast.       | Advisory engine generates sowing window correctly; passes functional testing.        |
| US5 | As a farmer, I want to update my crop type and location in my profile so advisories are relevant to me. | Profile update reflects in advisory engine immediately; passes functional testing.   |
| US6 | As an admin, I want to monitor active farmers and system health so I can ensure service availability.    | Admin panel shows real-time stats and alerts; passes functional testing.             |

---

## Requirement Gathering Report

The elicitation process identified the following as primary requirements for the Weather-Based Crop Advisory System:

**Functional Requirements:**
- Farmer registration, login, and profile management (crop type, location)
- Real-time weather data ingestion from external weather APIs
- Advisory engine to generate irrigation timing, sowing window, and weather warning advisories
- SMS alert delivery for frost, heat, and spray warnings via AWS SNS
- Web dashboard for farmers to view daily advisories
- Admin panel for user management and system monitoring

**Non-Functional Requirements:**
- Availability: 24×7 uptime ensured by serverless AWS infrastructure
- Performance: Advisory generation and SMS dispatch within 5 minutes of weather trigger
- Security: AWS Cognito for authentication; encrypted data in transit and at rest
- Scalability: Serverless architecture auto-scales to support thousands of farmers
- Usability: SMS-first design ensures accessibility for farmers without internet

Stakeholder feedback emphasised ease of use, timely alert delivery, crop-specific relevance, and reliability of cloud infrastructure.

---

## Observation

Using multiple elicitation techniques — interviews, questionnaires, observation, and user personas — improved requirement completeness and helped surface accessibility needs specific to the farming community, such as SMS-first delivery and early morning advisory timing.

---

## Result

Stakeholders were identified, requirements were elicited using suitable techniques, user stories were prepared, and the Requirement Gathering Report for the Weather-Based Crop Advisory System was successfully completed.
