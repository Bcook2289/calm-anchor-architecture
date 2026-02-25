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

## Tech Stack
### Client
![JavaScript](https://img.shields.io/badge/javascript-%23323330.svg?style=for-the-badge&logo=javascript&logoColor=%23F7DF1E)
![React](https://img.shields.io/badge/react-%2320232a.svg?style=for-the-badge&logo=react&logoColor=%2361DAFB)
![Capacitor](https://img.shields.io/badge/Capacitor.js-6.2.1-brightgreen?style=for-the-badge&logo=capacitor)

### Backend / Infrastructure
![Firebase](https://img.shields.io/badge/firebase-ffca28?style=for-the-badge&logo=firebase&logoColor=black)

## System Architecture
Calm Anchor follows a client-driven architecture built on Firebase-managed infrastructure. 

The React client application is resoponsible for:
- UI rendering and state management
- Routing and navigation logic
- Authentication state monitoring via Firebase SDK

Firebase Authentication manages secure user identity and session persistence across web and mobile environments.

Firestore serves as the primary data store. At the current stage, the database contains a `users` collection composed of authenticated user documents and associated metadata. The schema is intentionally minimal while core authentication and platform stability are being solidified.

The application is configured as:
- A Firebase Web App for browser deployment
- A Capacitor-wrapped Android application for mobile deployment

This architeccture enables rapid iteration without maintaining a dedicated backend server while preserving scalability through managed infrastructure.

## Current Architectural Phase
During early integration testing, an authentication state persistence issue was identified affecting returing users with existing RevenueCat-linked accounts. Users were being redirected to account creation rather than recognized as authenticated.

Investigation identified an architectural boundary issue between Firebase Authentication state resolution and RevenueCat session initialization.

Before addressing subscription-layer logic, the system was refactored to:
- Improve React state structure and authentication flow handling
- Simplify Firebase configuration by properly registering the application as a Web App.
- Separate authentication gating logic from subscription logic
- Ensure platform configuration consistency between web and Android builds

This staged approach prioritizes system stability before reintroducing subscription logic.

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
