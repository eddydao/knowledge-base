# Project Plan - Meal Planner App

## Project Vision

### Purpose
- Suggest daily meal plans for busy users who want to self-cook efficiently, avoiding time spent on planning.

### Target Audience
- Busy individuals, health-conscious home cooks.

### MVP Core Features
- Daily Automatic Menu Generation: A fresh menu is generated automatically every day.
- Manual Regeneration:
  - Full menu regeneration on demand.
  - Change a single dish within an existing menu.
- Exclude Ingredients: User can configure excluded ingredients.
- Ingredient List: Consolidated shopping list for the menu.
- Recipe Details: Full cooking instructions for each dish.
- Menu Settings:
  - Max cooking time per dish.
  - Number of dishes per meal.
  - Dish rotation frequency.

### Look & Feel
- Minimal, clean, modern UI.

---

## Technical Alignment

| Area | Decision |
|:----|:----|
| **Mobile Frontend** | React Native |
| **Backend** | Spring Boot (Java/Kotlin) |
| **Cloud Hosting** | Cloud-native (AWS, Azure, or GCP) |
| **Authentication** | Single Sign-On (Google, Apple, Facebook) via OAuth2 |
| **Notifications** | Real-time push notifications (e.g., Firebase, AWS SNS) |
| **Database** | PostgreSQL (or equivalent cloud-managed DB) |
| **Scheduler** | Automated daily menu generation (Spring Scheduler or cloud Cron) |
| **Offline Support** | No offline mode for MVP |

---

## Architecture Overview

```
[React Native Mobile App]
    |
    | - API Requests
    v
[Spring Boot Backend]
    - Authentication (OAuth2 SSO)
    - Menu Management APIs
    - Manual Menu/Dish Regeneration APIs
    - Ingredient List APIs
    - Recipe APIs
    - Push Notification Service
    - Scheduled Menu Generator (Daily)
    - Database (User Data, Recipes, Menus)
    |
    v
[Cloud Hosting Infrastructure]
    - Compute (App servers)
    - Database (PostgreSQL/RDS/Cloud SQL)
    - Notification System (Firebase, AWS SNS)
    - Identity Provider Integration
```

---

## Strategic Goals

### G01: Mobile App Development
- **Description**: Develop a React Native application offering daily meal plans, shopping lists, and recipes with minimal UI/UX.
- **Success Criteria**:
  - Fully functional mobile app on both iOS and Android.
  - Users can view daily menus, regenerate menus, view ingredients and recipes.
- **Dependencies**: Backend APIs, Authentication.

### G02: Backend Service Development
- **Description**: Build a Spring Boot backend with menu generation, user preferences, ingredient lists, and recipe APIs.
- **Success Criteria**: API readiness, automatic daily menu generation, manual regeneration.

### G03: Authentication and SSO Integration
- **Description**: Implement secure SSO using OAuth2 providers (Google, Apple, Facebook).
- **Success Criteria**: Smooth login flow and token management.

### G04: Push Notification System
- **Description**: Implement real-time notifications for menu updates.
- **Success Criteria**: Daily notifications and confirmation messages.

### G05: Cloud Hosting Infrastructure
- **Description**: Set up a scalable, secure cloud environment for hosting services.
- **Success Criteria**: Backend deployment, database setup, monitoring configured.

### G06: Recipe and Menu Content Management
- **Description**: Curate and tag an initial database of recipes.
- **Success Criteria**: Minimum 100 recipes with preparation metadata.

---

## Task Sequence

### G01: Mobile App Development
- G01-task-01: React Native project setup
- G01-task-02: Implement user authentication flow
- G01-task-03: Daily menu screen
- G01-task-04: Ingredient list screen
- G01-task-05: Recipe detail view
- G01-task-06: Settings screen (exclude ingredients, settings)
- G01-task-07: Manual menu/dish regeneration UI
- G01-task-08: Push notification handling

### G02: Backend Service Development
- G02-task-01: Spring Boot backend setup
- G02-task-02: User management and OAuth2 login
- G02-task-03: Daily menu scheduler
- G02-task-04: Ingredient list API
- G02-task-05: Recipe detail API
- G02-task-06: User preference management
- G02-task-07: Manual regeneration APIs
- G02-task-08: Notification triggers integration

### G03: Authentication and SSO Integration
- G03-task-01: OAuth2 backend server setup
- G03-task-02: Cloud identity provider configuration

### G04: Push Notification System
- G04-task-01: Backend notification service setup
- G04-task-02: Frontend notification integration

### G05: Cloud Hosting Infrastructure
- G05-task-01: Select cloud provider
- G05-task-02: Set up hosting and database
- G05-task-03: Configure CI/CD pipeline (optional)
- G05-task-04: Set up monitoring and logging

### G06: Recipe and Menu Content Management
- G06-task-00: Define Recipe Database Schema
- G06-task-01: Recipe dataset curation
- G06-task-02: Recipe tagging and metadata

---

## Gantt Chart

| Task                                          | Week 1-2 | Week 3-4 | Week 5-6 | Week 7-8 | Week 9-10 | Week 11-12 |
| :-------------------------------------------- | :------- | :------- | :------- | :------- | :-------- | :--------- |
| G05-task-01: Select Cloud Provider            | ███      |          |          |          |           |            |
| G06-task-00: Define Recipe Database Schema    | ███      |          |          |          |           |            |
| G06-task-01: Recipe Dataset Curation          |          | ███      | ███      |          |           |            |
| G02-task-01: Backend Setup                    |          | ███      | ███      |          |           |            |
| G03-task-01: Backend OAuth2 Setup             |          | ███      | ███      |          |           |            |
| G05-task-02: Cloud Environment Setup          |          |          | ███      |          |           |            |
| G01-task-01: React Native Setup               |          | ███      | ███      |          |           |            |
| G06-task-02: Recipe Tagging                   |          |          | ███      |          |           |            |
| G02-task-03: Daily Scheduler                  |          |          | ███      | ███      |           |            |
| G02-task-06: User Preferences API             |          |          | ███      | ███      |           |            |
| G01-task-03: Daily Menu Screen                |          |          | ███      | ███      |           |            |
| G01-task-06: Settings Screen                  |          |          | ███      | ███      |           |            |
| G04-task-01: Push Backend Setup               |          |          |          | ███      |           |            |
| G04-task-02: Push Frontend Integration        |          |          |          | ███      |           |            |
| G01-task-04: Ingredient List Screen           |          |          |          | ███      |           |            |
| G01-task-05: Recipe Detail View               |          |          |          | ███      |           |            |
| G02-task-08: Push Notification Trigger        |          |          |          | ███      |           |            |
| G01-task-07: Menu/Dish Regeneration UI        |          |          |          |          | ███       |            |
| G02-task-07: Manual Regeneration APIs         |          |          |          |          | ███       |            |
| G01-task-08: Final Push Notification Handling |          |          |          |          | ███       |            |
| G05-task-04: Monitoring & Logging             |          |          |          |          | ███       |            |
| Final Testing & Bug Fixing                    |          |          |          |          | ███       | ███        |
| MVP Launch                                    |          |          |          |          |           | ███        |

---

## Task List Corresponding with Gantt Chart

1. ~~G05-task-01: Select Cloud Provider:~~
	1. Use AWS EC2
2. G06-task-00: Define Recipe Database Schema
3. G06-task-01: Recipe Dataset Curation
4. G02-task-01: Backend Setup
5. G03-task-01: Backend OAuth2 Setup
6. G05-task-02: Cloud Environment Setup
7. G01-task-01: React Native Setup
8. G06-task-02: Recipe Tagging
9. G02-task-03: Daily Scheduler
10. G02-task-06: User Preferences API
11. G01-task-03: Daily Menu Screen
12. G01-task-06: Settings Screen
13. G04-task-01: Push Backend Setup
14. G04-task-02: Push Frontend Integration
15. G01-task-04: Ingredient List Screen
16. G01-task-05: Recipe Detail View
17. G02-task-08: Push Notification Trigger
18. G01-task-07: Menu/Dish Regeneration UI
19. G02-task-07: Manual Regeneration APIs
20. G01-task-08: Final Push Notification Handling
21. G05-task-04: Monitoring & Logging
22. Final Testing & Bug Fixing
23. MVP Launch

---

## Milestone Checklist for MVP Launch

| Milestone | Description | Owner | Due |
|:----------|:------------|:------|:----|
| M1: Cloud Provider Selected | AWS, Azure, or GCP chosen and basic infra designed | Project Owner | Week 2 |
| M2: Backend Project Setup Completed | Spring Boot project with modular structure | Backend Lead | Week 4 |
| M3: Authentication System Ready | OAuth2 backend + Mobile login working | Backend & Mobile | Week 6 |
| M4: Recipe Database Ready | Initial 100+ recipes curated and tagged | Content Team | Week 6 |
| M5: Cloud Environment Ready | Backend deployed to cloud, HTTPS enabled | DevOps | Week 7 |
| M6: Daily Menu Generation Working | Scheduler runs, menus created automatically | Backend | Week 8 |
| M7: Mobile App Core Screens Ready | Menu, Ingredients, Recipe, Settings | Mobile Team | Week 8 |
| M8: Push Notification System Working | New menu notifications and manual updates | Backend & Mobile | Week 10 |
| M9: Manual Regeneration Feature Done | Menu and dish regeneration working | Backend & Mobile | Week 10 |
| M10: Full System Integration Test | Frontend + Backend fully connected and tested | QA | Week 11 |
| M11: MVP Launch | Publish to App Stores (TestFlight, Google Play Internal Test) | Project Owner | Week 12 |

---

---

## Strategic Goals

### G01: Mobile App Development
- Develop React Native application with meal plan generation, shopping list, and recipes.
- Success: Core screens operational and linked to backend APIs.

### G02: Backend Service Development
- Build Spring Boot APIs and services supporting all app functions.
- Success: All endpoints secured, stable, and cloud-deployed.

### G03: Authentication and SSO Integration
- Implement OAuth2 login using Google and Apple IDs.
- Success: Seamless login with secure token management.

### G04: Push Notification System
- Enable real-time updates for menu generation.
- Success: User receives push notifications daily and on manual changes.

### G05: Cloud Hosting Infrastructure
- Host backend and database securely in cloud.
- Success: Scalable, monitored, production-ready infrastructure.

### G06: Recipe and Menu Content Management
- Curate and tag a recipe dataset aligned with menu generation logic.
- Success: Recipes ready, clean, and properly tagged.

---

## Task Sequence

(Already detailed earlier — so skipping here for brevity.)

---

## Gantt Chart

(Already detailed earlier — so skipping here for brevity.)

---

## Milestone Checklist for MVP Launch

(Already detailed earlier — so skipping here for brevity.)

---

## Task Details (Work Breakdown Structure)

### ~~G05-task-01: Select Cloud Provider~~
- ~~**Objective**: Choose AWS, Azure, or GCP.~~
- ~~**Subtasks**:~~
  - ~~Evaluate cloud options.~~
  - ~~Assess team experience.~~
  - ~~Confirm service compatibility.~~
  - ~~Make final decision.~~
- ~~**Owner**: Project Owner~~
- ~~**Deliverable**: Cloud provider decision memo.~~
Using AWS EC2 for the first service
---

### ~~G06-task-00: Define Recipe Database Schema~~
- ~~**Objective**: Create database structure for recipes.~~
- ~~**Subtasks**:~~
  - ~~Define tables and fields.~~
  - ~~Design ER diagram.~~
  - ~~Document schema.~~
- ~~**Owner**: Backend Developer~~
- ~~**Deliverable**: Schema document + migration scripts.~~

---

### G06-task-01: Recipe Dataset Curation
- **Objective**: Build initial recipe database.
- **Subtasks**:
  - Collect or scrape recipes.
  - Format to schema.
  - Validate and load data.
- **Owner**: Content Curator
- **Deliverable**: Seed dataset.

---

### ~~G02-task-01: Backend Setup~~
- ~~**Objective**: Initialize backend project.~~
- ~~**Subtasks**:~~
  - ~~Scaffold Spring Boot project.~~
  - ~~Setup database connection.~~
  - ~~Create health check API.~~
- ~~**Owner**: Backend Developer~~
- ~~**Deliverable**: Running backend project.~~

---

### G03-task-01: Backend OAuth2 Setup
- **Objective**: Secure backend login with OAuth2.
- **Subtasks**:
  - Configure OAuth2 clients.
  - Implement token management.
- **Owner**: Backend Developer
- **Deliverable**: OAuth2 integration.

---

### G05-task-02: Cloud Environment Setup
- **Objective**: Deploy backend to cloud.
- **Subtasks**:
  - Provision compute/database.
  - Set up firewall/security.
  - Deploy backend server.
- **Owner**: DevOps Engineer
- **Deliverable**: Cloud-hosted backend.

---

### G01-task-01: React Native Setup
- **Objective**: Initialize mobile app.
- **Subtasks**:
  - Scaffold project.
  - Set up navigation.
- **Owner**: Mobile Developer
- **Deliverable**: Running mobile skeleton app.

---

### G06-task-02: Recipe Tagging
- **Objective**: Apply metadata tags to recipes.
- **Subtasks**:
  - Define taxonomy.
  - Tag recipes consistently.
- **Owner**: Content Curator
- **Deliverable**: Tagged dataset.

---

### G02-task-03: Daily Scheduler
- **Objective**: Automate daily menu generation.
- **Subtasks**:
  - Implement scheduled tasks.
  - Persist generated menus.
- **Owner**: Backend Developer
- **Deliverable**: Scheduled menu generation.

---

### G02-task-06: User Preferences API
- **Objective**: Manage user settings backend.
- **Subtasks**:
  - Implement CRUD APIs.
  - Secure endpoints.
- **Owner**: Backend Developer
- **Deliverable**: Preferences API.

---

### G01-task-03: Daily Menu Screen
- **Objective**: Display daily menus.
- **Subtasks**:
  - Fetch daily menu.
  - Display dishes.
- **Owner**: Mobile Developer
- **Deliverable**: Menu screen.

---

### G01-task-06: Settings Screen
- **Objective**: Manage user menu preferences.
- **Subtasks**:
  - Build settings UI.
  - Save preferences.
- **Owner**: Mobile Developer
- **Deliverable**: Settings screen.

---

### G04-task-01: Push Backend Setup
- **Objective**: Send push notifications from backend.
- **Subtasks**:
  - Integrate FCM or SNS.
  - Store device tokens.
- **Owner**: Backend Developer
- **Deliverable**: Push service.

---

### G04-task-02: Push Frontend Integration
- **Objective**: Handle notifications on mobile.
- **Subtasks**:
  - Configure permissions.
  - Handle incoming messages.
- **Owner**: Mobile Developer
- **Deliverable**: Mobile notifications functional.

---

### G01-task-04: Ingredient List Screen
- **Objective**: Display ingredients list.
- **Subtasks**:
  - Fetch from API.
  - Display organized list.
- **Owner**: Mobile Developer
- **Deliverable**: Ingredient screen.

---

### G01-task-05: Recipe Detail View
- **Objective**: Show cooking instructions.
- **Subtasks**:
  - Fetch recipe details.
  - Layout information cleanly.
- **Owner**: Mobile Developer
- **Deliverable**: Recipe detail screen.

---

### G02-task-08: Push Notification Trigger
- **Objective**: Trigger notifications after events.
- **Subtasks**:
  - Fire after scheduler runs.
  - Fire after manual changes.
- **Owner**: Backend Developer
- **Deliverable**: Push triggers integrated.

---

### G01-task-07: Menu/Dish Regeneration UI
- **Objective**: Allow menu or dish replacement.
- **Subtasks**:
  - Build regenerate menu/dish actions.
  - Refresh views after regeneration.
- **Owner**: Mobile Developer
- **Deliverable**: Manual regeneration UI.

---

### G02-task-07: Manual Regeneration APIs
- **Objective**: Support menu/dish regeneration backend.
- **Subtasks**:
  - API to regenerate menu.
  - API to replace single dish.
- **Owner**: Backend Developer
- **Deliverable**: Regeneration APIs.

---

### G01-task-08: Final Push Notification Handling
- **Objective**: Polish notification UX.
- **Subtasks**:
  - Tune notification messages.
  - Redirect to correct screens.
- **Owner**: Mobile Developer
- **Deliverable**: Notification UX finalized.

---

### G05-task-04: Monitoring & Logging
- **Objective**: Enable system monitoring.
- **Subtasks**:
  - Set up logs.
  - Configure basic alerts.
- **Owner**: DevOps Engineer
- **Deliverable**: Monitoring system online.

---

### Final Testing & Bug Fixing
- **Objective**: Stabilize MVP build.
- **Subtasks**:
  - Perform integration, regression testing.
  - Fix all critical bugs.
- **Owner**: QA Team + Developers
- **Deliverable**: Launch-ready build.

---

### MVP Launch
- **Objective**: Soft launch to internal testers.
- **Subtasks**:
  - Submit to TestFlight & Google Play Console.
  - Collect tester feedback.
- **Owner**: Project Owner / Mobile Team
- **Deliverable**: Internal app release.

---