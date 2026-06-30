# Calm Anchor - Architectural Overview
Calm Anchor is a cross-platform web and mobile application designed to support structured behavioral reinforcement strategies through games and guided workflows.

This repository documents the system architecture and engineering decisions. The production source code remains private.

## My Role
Full-stack developer responsible for:
- System architecture design
- React application structure and state management
- Firebase authentication integration
- Firestore data modeling and document schema design
- Capacitor mobile configuration and build process
- Deployment configuration
- CI/CD pipeline design and implementation with GitHub Actions
- Automated testing strategy and coverage

## Tech Stack
### Client
![JavaScript](https://img.shields.io/badge/javascript-%23323330.svg?style=for-the-badge&logo=javascript&logoColor=%23F7DF1E)
![React](https://img.shields.io/badge/react-%2320232a.svg?style=for-the-badge&logo=react&logoColor=%2361DAFB)
![Capacitor](https://img.shields.io/badge/Capacitor.js-6.2.1-brightgreen?style=for-the-badge&logo=capacitor)

### Backend / Infrastructure
![Firebase](https://img.shields.io/badge/firebase-ffca28?style=for-the-badge&logo=firebase&logoColor=black)

### Testing and CI/CD
![Vitest](https://img.shields.io/badge/vitest-%236E9F18.svg?style=for-the-badge&logo=vitest&logoColor=white)
![GitHub Actions](https://img.shields.io/badge/github%20actions-%232671E5.svg?style=for-the-badge&logo=githubactions&logoColor=white)

## System Architecture
Calm Anchor follows a client-driven architecture built on Firebase-managed infrastructure.

The React client application is responsible for:
- UI rendering and state management
- Routing and navigation logic
- Authentication state monitoring via Firebase SDK

Firebase Authentication manages secure user identity and session persistence across web and mobile environments.

Firestore serves as the primary data store. At the current stage, the database contains a `users` collection composed of authenticated user documents and associated metadata. The schema was intentionally left minimal while core authentication and platform stability was solidified.

The application is configured as:
- A Firebase Web App for browser deployment
- A Capacitor-wrapped Android application for mobile deployment

This architecture enables rapid iteration without maintaining a dedicated backend server while preserving scalability through managed infrastructure.

## Testing & Deployment Pipeline
With core authentication stabilized, the project has moved into a quality-and-release phase, establishing a CI/CD pipeline via GitHub Actions to support reliable and repeatable builds across platforms.

### Automated Testing
- 38 passing unit tests across 9 files, built with Vitest and React Testing Library
- Coverage focused on authentication flow, state management, and core UI logic

### CI/CD Pipeline
- GitHub Actions workflow handling build, test and signing steps
- Resolved a series of environment configuration, Android signing, and version code issues during pipeline construction
- Automated build pushes to Google Play for Android distribution

This phase reflects a broader architectural principle: stabilize and verify before layering on additional product features.

## Current Architectural Phase
During early integration testing, an authentication state persistence issue was identified affecting returning users with existing RevenueCat-linked accounts. Users were being redirected to account creation rather than recognized as authenticated.

Investigation identified an architectural boundary issue between Firebase Authentication state resolution and RevenueCat session initialization.

To address this, the system was refactored to:
- Improve React state structure and authentication flow handling
- Simplify Firebase configuration by properly registering the application as a Web App
- Separate authentication gating logic from subscription logic
- Ensure platform configuration consistency between web and Android builds

This staged approach prioritized system stability before reintroducing subscription logic, and the application has since reached MVP status with CI/CD and automated testing in place (see Testing & Deployment Pipeline above).

### Open Items
A small number of known issues remain tracked for future iteration:
- A race condition in the `usePaywall` hook related to RevenueCat readiness timing; a fix using an `isRCReady` flag has been identified and is pending merge
- General design and formatting issues 

Future iterations will expand Firestore schema design to support structured behavioral tracking, progress persistence, and subscription management.

## Security Considerations (Planned)
Future iterations will include:
- Firestore security rules enforcing user-scoped document access
- Validation constraints to prevent unauthorized data mutation
- Role-based access logic as feature set expands

## Architectural Principles
- Stabilize core authentication before expanding feature scope
- Maintain clear separation between authentication and subscription layers
- Prefer managed infrastructure to reduce backend operational overhead
- Design for incremental schema expansion
- Verify behavior through automated testing before layering on new features
