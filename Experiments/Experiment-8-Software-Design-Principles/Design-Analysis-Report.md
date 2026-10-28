# Experiment 8 — Software Design Principles: Design Analysis Report

## 1. Objective
To analyze the design of the Weather-Based Crop Advisory System using modularization, coupling, cohesion, function-oriented and object-oriented design, and top-down/bottom-up approaches.

## 2. Proposed modularization
The system is separated into four logical services, consistent with the SRS:
1. **Farmer Service:** profile-related operations and integration with Cognito.
2. **Weather Service:** scheduled weather ingestion and persistence.
3. **Advisory Engine:** applies rule-based crop/weather logic and stores advisories.
4. **Alert Service:** formats and dispatches SMS through SNS and records delivery outcomes.

The web dashboard and admin panel are client interfaces. API Gateway exposes backend operations. DynamoDB stores system records.

## 3. Coupling and cohesion analysis

### Coupling
Coupling describes the degree of dependency between modules. The design aims for **low coupling**:
- Weather Service provides validated weather records instead of exposing its internal implementation.
- Advisory Engine consumes weather/profile/rule data through defined interfaces.
- Alert Service receives an alert/advisory payload rather than independently re-running crop rules.
- AWS integrations are isolated behind service-level responsibilities.
- Shared data schemas and API contracts should be versioned and documented.

### Cohesion
Cohesion describes how closely related a module's responsibilities are. The design aims for **high cohesion**:
- Farmer Service focuses on farmer profile/account-related operations.
- Weather Service focuses on data ingestion and validation.
- Advisory Engine focuses on applying advisory rules.
- Alert Service focuses on message formatting, dispatch, and delivery logging.
- Admin functions focus on account management, configuration, and monitoring views.

### Summary

| Module | Main responsibility | Coupling goal | Cohesion goal |
|---|---|---|---|
| Farmer Service | Profile and account operations | Depend on Cognito/DynamoDB interfaces | High |
| Weather Service | Fetch, validate, and store weather | Depend on weather API and persistence interface | High |
| Advisory Engine | Apply rules and create advisories | Consume defined input contracts | High |
| Alert Service | Send SMS and record outcomes | Depend on SNS and delivery records | High |
| Dashboard | Present data and capture user input | Call API Gateway; avoid business rules in UI | High |
| Admin Panel | Admin operations and monitoring | Use authorized admin APIs | High |

## 4. Function-oriented vs object-oriented design

| Aspect | Function-oriented design | Object-oriented design |
|---|---|---|
| Main focus | Functions/processes and data flow | Domain objects with state and behavior |
| Decomposition | Break work into functions such as `fetchWeather()` and `generateAdvisories()` | Model `Farmer`, `WeatherRecord`, `Advisory`, `AdvisoryRule`, and `AlertRecord` |
| Strength | Clear processing pipeline | Clear domain model and responsibilities |
| Limitation | Data and behavior may become separated across many functions | Requires careful class boundaries and does not mean DynamoDB must be relational |
| Use in this system | Lambda handlers and workflow steps | Domain modeling and service-level design |

**Conclusion:** A hybrid approach is suitable. Use service-oriented functions/Lambda handlers for event-driven execution, with object-oriented domain models and clear data contracts where helpful.

## 5. Top-down vs bottom-up design

### Top-down design
Start from the overall business goal, decompose the system into services, then define each service's functions.
- System → Farmer, Weather, Advisory, Alert services
- Weather Service → fetch, validate, timestamp, store
- Advisory Engine → load inputs, evaluate rules, persist advisories
- Alert Service → format, send, log

**Benefit:** Supports requirement traceability and helps ensure all SRS features are covered.

### Bottom-up design
Start from reusable building blocks and combine them into larger components.
- Weather API client + validation + DynamoDB repository → Weather Service
- Rule evaluator + profile lookup + advisory repository → Advisory Engine
- SMS formatter + SNS publisher + delivery logger → Alert Service

**Benefit:** Supports unit testing and reuse of small, well-defined components.

### Recommended approach
Use **top-down design for initial architecture** and **bottom-up implementation/testing for individual components**. This balances requirement coverage with testable implementation units.

## 6. Design quality considerations
- **Maintainability:** Keep each service focused on one responsibility.
- **Scalability:** Serverless services can scale independently within AWS service limits.
- **Reliability:** Retry weather API calls up to three times and log failures.
- **Security:** Use Cognito JWT authentication, restrict admin functions to the admin group, and encrypt data in transit and at rest.
- **Testability:** Unit-test rule evaluation, weather validation, SMS formatting, and delivery-status handling independently.
- **Observability:** Emit structured logs to CloudWatch and alert administrators on critical failures.

## 7. Conclusion
The Weather-Based Crop Advisory System benefits from modular design, low coupling, high cohesion, and a hybrid function-oriented/object-oriented approach. Top-down decomposition should guide the architecture, while bottom-up implementation and unit testing should validate each component.

## 8. Deliverable
Design analysis report covering modularization, coupling, cohesion, function-oriented vs object-oriented design, and top-down vs bottom-up design.
