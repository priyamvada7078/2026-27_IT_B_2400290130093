# Experiment 3

## Software Design Principles – Requirement Elicitation

### Aim

To identify the stakeholders of the ATM System, understand their needs using suitable requirement elicitation techniques, and prepare user stories and a Requirement Gathering Report.

---

## Objectives

- To identify the main stakeholders involved with the ATM System.
- To understand the requirements and expectations of different stakeholders.
- To use suitable techniques such as interviews, questionnaires, observation, and user personas.
- To identify functional and non-functional requirements.
- To prepare user stories based on the collected requirements.
- To define acceptance criteria for the user stories.
- To prepare a Requirement Gathering Report.

---

## Introduction

Requirement elicitation is the process of finding out what users and other stakeholders expect from a software system. It is one of the important stages of software development because the development team needs to understand the actual requirements before designing and building the system.

Requirements can be collected in different ways. Interviews allow us to discuss requirements directly with users, questionnaires help collect feedback from several people, and observation helps us understand how users actually interact with a system. User personas can also be created to represent different types of users and their needs.

For the ATM System, these techniques help us understand requirements related to security, transaction speed, ease of use, reliability, and availability.

---

## Selected Project

**Project Title:** ATM System  
**Domain:** Banking and Financial Services

---

# 1. Stakeholder Identification

A stakeholder is a person, group, or system that uses the software, manages it, or is affected by its operation.

The main stakeholders of the ATM System are:

| Stakeholder | Role | Main Requirements |
|---|---|---|
| Customer | Uses the ATM for banking transactions | Fast, simple and secure transactions |
| Bank Administrator | Monitors and manages ATM operations | Transaction monitoring, user management and system control |
| Maintenance Engineer | Maintains ATM hardware and software | Easy diagnostics, error reporting and maintenance |
| Bank Server | Processes account and transaction requests | Reliable communication, accurate data and secure processing |

### Customer

The customer is the main user of the ATM. Customers expect the system to be easy to understand and allow them to complete transactions quickly and securely.

### Bank Administrator

The bank administrator is responsible for monitoring ATM operations and checking transaction-related information. The administrator also needs to identify unusual activities and system issues.

### Maintenance Engineer

The maintenance engineer handles technical problems related to ATM hardware and software. The system should provide useful error information so that problems can be identified and fixed easily.

### Bank Server

The bank server communicates with the ATM and processes requests such as balance enquiry, withdrawal, deposit, and fund transfer. It must maintain accurate and secure account information.

---

# 2. Requirement Elicitation Techniques

Different techniques were considered to understand the requirements of the ATM System.

| Technique | How It Is Used | Expected Outcome |
|---|---|---|
| Interview | Discuss requirements directly with customers and bank staff | Detailed requirements and problems |
| Questionnaire | Ask multiple users about their expectations | General user preferences and feedback |
| Observation | Observe how users normally interact with ATMs | Usability and workflow requirements |
| User Persona | Create profiles of different types of users | Better understanding of different user needs |

Using multiple techniques is useful because one method may not provide all the required information.

---

# 3. Sample Requirement Gathering Findings

## 3.1 Interview Findings

Based on discussions with typical ATM users and banking staff, the following requirements were identified:

- Customers want the login process to be quick and simple.
- The system should clearly indicate whether a transaction was successful or unsuccessful.
- Customers should be able to choose whether they want a printed receipt.
- The ATM should not allow access after repeated incorrect PIN attempts.
- Customers should be informed if there is insufficient balance.
- Transactions should be completed without unnecessary steps.

---

## 3.2 Observation Findings

Observation of typical ATM usage showed that:

- Users prefer a simple menu with clearly visible options.
- Common options such as cash withdrawal and balance enquiry should be easy to find.
- Error messages should be simple and understandable.
- Users should be able to cancel a transaction easily.
- The system should clearly show the next step during a transaction.
- Senior users may need larger and simpler menu options.

---

## 3.3 Questionnaire Findings

A sample questionnaire was considered to understand common customer expectations.

The major findings were:

- Most users expect ATM services to be available 24×7.
- Security is considered one of the most important requirements.
- Users prefer quick transaction processing.
- Most users want the option to receive a receipt.
- Users prefer fewer steps for frequently used services.
- Clear error messages are important when a transaction fails.

---

# 4. User Personas

User personas represent different types of people who may use the ATM System. They help in designing the system according to different user needs.

| Persona | Age | Goal | Pain Point | Requirement |
|---|---:|---|---|---|
| Regular Customer | 35 | Withdraw cash quickly | Waiting time | Fast and simple withdrawal |
| Senior Citizen | 65 | Check balance easily | Complex navigation | Clear and simple interface |
| Business User | 42 | Transfer funds securely | Transaction delays | Secure and reliable fund transfer |

### Regular Customer

A regular customer generally wants to complete common transactions quickly. The system should therefore keep frequently used options easily accessible.

### Senior Citizen

A senior citizen may find complex menus difficult to use. Clear instructions, simple navigation, and readable text are important for this user.

### Business User

A business user may frequently transfer money and check account information. Security, accuracy, and reliable transaction processing are important for this user.

---

# 5. Functional Requirements

Functional requirements describe what the ATM System should actually do.

The ATM System should:

1. Allow customers to insert their ATM card and enter their PIN.
2. Validate the card and PIN before giving access.
3. Restrict access after multiple incorrect PIN attempts.
4. Display the available banking services after successful login.
5. Allow customers to check their account balance.
6. Allow customers to withdraw cash.
7. Check whether sufficient balance is available before withdrawal.
8. Allow customers to deposit cash.
9. Allow customers to transfer funds to another account.
10. Provide a mini statement of recent transactions.
11. Generate a receipt after a transaction if requested.
12. Display appropriate messages when a transaction succeeds or fails.
13. Allow customers to cancel a transaction.
14. End the session and return the ATM to the starting screen after the transaction.

---

# 6. Non-Functional Requirements

Non-functional requirements describe how well the system should work.

| Requirement | Description |
|---|---|
| Security | Customer information and transactions should be protected from unauthorized access. |
| Performance | The system should respond quickly to customer requests. |
| Availability | ATM services should be available 24×7 whenever the machine is operational. |
| Reliability | Transactions should be processed correctly without loss of data. |
| Usability | The interface should be simple and easy to understand. |
| Maintainability | The system should be easy to monitor, update, and repair. |
| Accuracy | Account balances and transaction records should always be correct. |

---

# 7. User Stories

User stories describe requirements from the point of view of the person using the system.

| ID | User Story | Acceptance Criteria |
|---|---|---|
| US1 | As a customer, I want to log in using my ATM card and PIN so that only an authorized user can access my account. | Valid card and PIN allow access. Invalid credentials are rejected and repeated failures are handled securely. |
| US2 | As a customer, I want to withdraw cash so that I can access my money when needed. | Withdrawal is allowed only when the account has sufficient balance and the requested amount is valid. |
| US3 | As a customer, I want to check my account balance so that I know how much money is available. | The current and correct account balance is displayed after authentication. |
| US4 | As a customer, I want to deposit cash so that my account balance is updated. | The deposited amount is verified and added correctly to the account balance. |
| US5 | As a customer, I want to transfer money to another account so that I can send funds securely. | The transfer is processed only after account validation and successful confirmation. |
| US6 | As a customer, I want to receive a transaction receipt so that I have a record of my transaction. | A receipt is generated when the customer chooses the receipt option. |
| US7 | As a customer, I want to view a mini statement so that I can see my recent transactions. | Recent transactions are displayed accurately after successful authentication. |

---

# 8. Requirement Gathering Report

The requirement gathering process was carried out by considering the needs of customers, bank administrators, maintenance engineers, and the bank server.

The main requirements identified for the ATM System are **secure authentication, balance enquiry, cash withdrawal, cash deposit, fund transfer, mini statements, and receipt generation**.

Customers mainly expect the system to be fast, simple, and secure. The observation and questionnaire findings also showed that users prefer clear navigation, fewer steps for common transactions, and understandable error messages.

Security is a major requirement because the ATM handles personal and financial information. The system should therefore validate users properly, protect transaction information, and handle incorrect PIN attempts securely.

The bank also requires the system to be reliable and easy to maintain. The ATM should communicate properly with the central banking server and should maintain accurate transaction records.

Based on the collected requirements, both functional and non-functional requirements were identified and converted into user stories.

---

# 9. Requirement Summary

| Category | Main Requirements |
|---|---|
| Authentication | Card and PIN validation |
| Transactions | Withdrawal, deposit and fund transfer |
| Account Information | Balance enquiry and mini statement |
| Security | PIN protection and unauthorized access prevention |
| Usability | Simple menus and clear instructions |
| Performance | Quick transaction response |
| Reliability | Accurate transaction processing |
| Availability | 24×7 service availability |
| Maintenance | Easy monitoring and error diagnosis |

---

# 10. Observation

Using different requirement elicitation techniques gives a better understanding of the system.

Interviews help collect detailed information directly from stakeholders, questionnaires provide feedback from multiple users, observation helps identify actual usability problems, and user personas help understand the needs of different types of customers.

Combining these techniques makes the requirements clearer and reduces the chances of missing important user needs.

---

# Result

The stakeholders of the **ATM System** were identified and their requirements were collected using suitable requirement elicitation techniques.

Functional and non-functional requirements were documented, user personas were prepared, and user stories with acceptance criteria were created.

The Requirement Gathering Report was successfully prepared and the major requirements of the ATM System were identified.
