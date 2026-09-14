# Experiment 2 — Problem Identification and Feasibility: Software Design Principles

## Aim

To identify the problem addressed by the selected software project and prepare its problem statement, objectives, scope, and technical and operational feasibility analysis.

---

## Objectives

- Identify the real-world problem addressed by the software project.
- Prepare a clear problem statement.
- Define project objectives and scope.
- Perform technical and operational feasibility analysis.
- Evaluate the viability of the proposed solution.

---

## Introduction

Problem identification is the first step in software engineering. A well-defined problem statement and feasibility study ensure that the proposed software solution is practical, achievable, and aligned with stakeholder requirements before development begins.

---

## Selected Project

| Field              | Details                               |
|--------------------|---------------------------------------|
| **Project Title**  | Weather-Based Crop Advisory System    |
| **Domain**         | Agriculture / AgriTech                |

---

## Problem Statement

Farmers in rural and semi-urban areas often lack access to timely, localised weather information, leading to poor decisions around irrigation, sowing, and crop protection. Unpredictable weather events such as frost, heat waves, and unseasonal rainfall cause significant crop losses that could be avoided with proper advance advisory. A **Weather-Based Crop Advisory System** addresses this by providing farmers with real-time, weather-driven advisories — including irrigation timing, sowing windows, and frost/heat/spray warnings — delivered through a web dashboard and SMS alerts, built on a fully serverless AWS cloud architecture.

---

## Project Objectives

- Provide farmers with localised, real-time weather-driven crop advisories.
- Deliver actionable alerts (irrigation timing, sowing window, frost/heat/spray warnings) via web dashboard and SMS.
- Implement secure farmer authentication and profile management.
- Automate weather data ingestion and advisory generation using cloud services.
- Build a scalable, serverless architecture on AWS (Cognito, API Gateway, Lambda, DynamoDB, EventBridge, SNS, S3, CloudFront).
- Provide an admin panel for system monitoring and management.

---

## Project Scope

### In Scope
- Farmer registration, authentication, and profile management (AWS Cognito)
- Real-time weather data ingestion and processing (Lambda, EventBridge)
- Advisory engine for irrigation timing, sowing windows, and weather warnings
- SMS alert delivery to farmers (AWS SNS)
- Web dashboard for farmers to view advisories (S3, CloudFront)
- Admin panel for monitoring and cloud operations
- Serverless backend services (API Gateway, Lambda, DynamoDB)

### Out of Scope
- Offline or on-premise deployment
- Crop disease detection or image-based analysis
- Market price advisory or supply chain management
- Direct hardware/IoT sensor integration

---

## Project Team

| Team Member  | Role                                        |
|--------------|---------------------------------------------|
| Priyamvada   | Identity, Frontend Shell & Farmer Profile   |
| Ishant       | Weather Ingestion & Advisory Engine         |
| Naitik       | Alerts, Admin Panel & Cloud Ops             |

---

## Technical Feasibility Analysis

| Factor         | Assessment  | Remarks                                                                         |
|----------------|-------------|---------------------------------------------------------------------------------|
| Technology     | ✅ Feasible  | AWS serverless stack (Lambda, DynamoDB, SNS, Cognito) is production-ready       |
| Hardware       | ✅ Feasible  | No dedicated hardware required; cloud infrastructure handles all compute        |
| Software Tools | ✅ Feasible  | VS Code, Git, GitHub, AWS Console, and open weather APIs are freely available   |
| Security       | ✅ Feasible  | AWS Cognito handles authentication; API Gateway enforces access control         |
| Scalability    | ✅ Feasible  | Serverless architecture auto-scales based on demand with no manual intervention |

---

## Operational Feasibility Analysis

| Factor           | Assessment | Remarks                                                              |
|------------------|------------|----------------------------------------------------------------------|
| User Acceptance  | ⭐ High     | SMS alerts and simple dashboard cater to low-tech farmer users       |
| Ease of Use      | ⭐ High     | Minimal training required; advisories delivered directly via SMS     |
| Availability     | ⭐ High     | Cloud-hosted, serverless system ensures 24×7 uptime                  |
| Maintainability  | ⭐ High     | Modular microservices (farmer, weather, advisory, alert) ease updates |
| Business Benefit | ⭐ High     | Reduces crop losses, improves farm productivity and farmer income     |

---

## Analysis

The feasibility study confirms that the Weather-Based Crop Advisory System is both technically and operationally viable. AWS serverless services eliminate infrastructure overhead, open weather APIs provide real-time data at low cost, and the SMS-based delivery model ensures accessibility even for farmers with basic mobile phones. The modular architecture allows independent development and future scaling.

---

## Observation

Clearly defining the problem, objectives, scope, and feasibility for the Weather-Based Crop Advisory System provides a strong foundation for subsequent software design activities such as requirements specification, system design, and cloud architecture planning.

---

## Result

The problem statement, objectives, project scope, and technical and operational feasibility analysis for the Weather-Based Crop Advisory System were successfully prepared.
