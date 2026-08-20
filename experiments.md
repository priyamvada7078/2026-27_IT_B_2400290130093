# Experiment Log — Weather-Based Crop Advisory System

## Experiment 1: Introduction to Software Engineering Tools and Project Setup

### Aim
To select a real-world software project, form a project team, create a GitHub repository, and demonstrate basic Git and GitHub version control operations.

### Objectives
1. Select an appropriate real-world software project.
2. Define project team roles and responsibilities.
3. Create a GitHub repository.
4. Create the initial project structure.
5. Perform basic Git operations such as add, commit, and push.
6. Understand collaborative software development using GitHub.

### Tools Required
- GitHub account
- Git / GitHub Desktop
- VS Code (or any code editor)
- Terminal (Git Bash / PowerShell)

### Problem Statement
Develop a Weather-Based Crop Advisory System using Software Engineering principles and AWS cloud services. Create a GitHub repository for the project, organise the project team, create the initial project structure, and demonstrate essential Git operations.

### Selected Project
- **Project Title:** Weather-Based Crop Advisory System
- **Domain:** Agriculture / AgriTech
- **Objective:** Develop a system that provides farmers with localized, weather-driven advisories (irrigation timing, sowing window, spray/frost/heat warnings) through a web dashboard and SMS alerts, built on a fully serverless AWS architecture (Cognito, API Gateway, Lambda, DynamoDB, EventBridge, SNS, S3, CloudFront).

### Project Team
| Team Member | Role |
|---|---|
| Member A | Identity, Frontend Shell & Farmer Profile |
| Member B | Weather Ingestion & Advisory Engine |
| Member C | Alerts, Admin Panel & Cloud Ops |

### Steps Performed

**Step 1: Create the GitHub repository.**
- Created a new repository on GitHub named `2026-27_IT_B_2400290130093`.
- Added a README.md file.
- Added a .gitignore file (Node template).
- Added all three team members as collaborators via Settings → Collaborators.

**Step 2: Clone the repository locally.**

git clone https://github.com/priyamvada7078/2026-27_IT_B_2400290130093.git
cd 2026-27_IT_B_2400290130093


**Step 3: Create the initial project folder structure.**

2026-27_IT_B_2400290130093/
├── README.md
├── .gitignore
├── docs/
│ ├── SRS/
│ └── UML/
├── frontend/
├── backend/
│ ├── farmer-service/
│ ├── weather-service/
│ ├── advisory-service/
│ └── alert-service/
└── test/

Created using:

mkdir -p docs/SRS docs/UML frontend backend/farmer-service backend/weather-service backend/advisory-service backend/alert-service test
touch docs/SRS/.gitkeep docs/UML/.gitkeep frontend/.gitkeep backend/farmer-service/.gitkeep backend/weather-service/.gitkeep backend/advisory-service/.gitkeep backend/alert-service/.gitkeep test/.gitkeep


**Step 4: Stage, commit, and push the project structure.**

git add .
git commit -m "Add project folder structure"
git push origin main


**Step 5: Verify collaboration.**
- Confirmed all three members could pull the updated structure using `git pull origin main`.
- Verified the repository on GitHub.com reflected the complete folder structure.
- Each member created their own feature branch (`feature/farmer-auth`, `feature/weather-advisory`, `feature/alerts-admin`).

### Expected Outcome
The GitHub repository should contain the initial project structure, README file, documentation folders, source-code folders for frontend and backend services, a testing folder, and a complete Git version history. All team members should be able to access and collaborate.

### Observation
Git and GitHub provided an effective mechanism for maintaining project structure and collaborating among team members. Creating the repository, defining the folder structure, and pushing it through basic Git operations established a shared foundation for independent, branch-based development.

### Result
The Weather-Based Crop Advisory System project was successfully selected and the project team was formed. A GitHub repository was created, the initial project structure was established, and all team members successfully cloned the repository and verified access for collaborative development.
