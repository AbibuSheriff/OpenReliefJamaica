System Architecture — OpenRelief Jamaica

This document provides a full technical overview of the OpenRelief Jamaica system architecture. It explains how the frontend, backend, database, security model, and automation layers interact to deliver a real-time, reliable emergency reporting platform.

The architecture is intentionally lightweight, scalable, and optimised for disaster scenarios where internet connectivity may be limited.

1. Architecture Overview

The OpenRelief architecture follows a modular three-layer model:

1.1 Frontend Layer (Presentation)

Built using Base44’s UI builder

Mobile-first design

Real-time form submission

Public and role-restricted views

1.2 Backend Layer (Application Logic)

Base44 API engine

Handles all validation and request processing

Executes system logic (e.g., report creation, NGO approval)

Runs email automation triggers

Manages role-based access enforcement

1.3 Data Layer (Storage & Logging)

Report table

Organisation table

EmailLog table

Secure access rules per entity

Together, these layers form a clean, predictable, and secure workflow suitable for large-scale emergency communication.

2. High-Level Architecture Diagram
Citizen User ──────┐
NGO Worker ─────────┼───> [ Frontend UI ] ───> [ Backend API ] ───> [ Database ]
Admin User ─────────┘

                                  ↓
                         [ Email Trigger System ]
                                  ↓
                            [ SMTP Service ]
                                  ↓
                           [ EmailLog Table ]

Security Layer (RBAC)
- Citizens: submit/view public data
- NGOs: region-limited access
- Admins: full system access


This diagram illustrates the end-to-end flow from user action to backend processing and email automation.

3. Component Breakdown
3.1 Frontend Components

The UI interacts with the backend exclusively through HTTPS JSON requests.

Key responsibilities:

Render forms and incident lists

Collect structured information

Display filtered NGO and report data

Provide a clean UX under emergency conditions

Frontend documentation:
/docs/frontend/README.md

3.2 Backend Components

The backend is the operational centre of the system.

Key responsibilities:

Validate incoming data

Apply role-based access rules

Save entities to the database

Trigger automated emails

Return clean JSON responses

Log all email activity

Backend documentation:
/docs/backend/README.md

3.3 Database Layer

This layer stores all persistent data.

Entities:

Report

Organisation

EmailLog

All access to the database is tightly controlled and routed through the backend API.

Database documentation:
/docs/database/README.md

4. Security Architecture

OpenRelief uses strict Role-Based Access Control (RBAC):

4.1 Citizen

Submit reports

View non-sensitive data

Cannot access internal tools

4.2 NGO

Must be approved

Can view reports in their region

Can update report statuses

4.3 Admin

Full system control

Approves NGOs

Views all email logs

Manages triggers and internal configurations

Security documentation:
/docs/security/README.md

5. API Architecture

All interactions happen through Base44’s secure API layer.

5.1 API Responsibilities

Authentication using API keys

JSON request handling

CRUD actions on entities

Error handling

Enforcement of permissions

API documentation:
/docs/api/README.md

6. Data Flow (Request Lifecycle)

A typical request follows this lifecycle:

6.1 Report Creation (Citizen)

User submits a report via frontend

Frontend sends POST request

Backend validates fields

Backend writes record to Report table

Backend returns success JSON

Report appears instantly in public list

6.2 NGO Registration

NGO submits registration form

Backend creates Organisation record

Backend triggers:

Confirmation email

Admin notification

EmailLog records both emails

Admin approves the organisation

NGO receives approval email

6.3 Report Status Update (NGO)

NGO updates report status

Backend checks role + permissions

Status updated

Updates visible in real time

7. Email Automation Architecture

Email automation is handled internally through Base44 triggers.

Primary automations:

NGO registration confirmation

Admin notification of new NGO

NGO approval email

All emails:

Route through SMTP

Are logged in EmailLog

Include timestamps and status markers

This provides a complete audit trail.

8. Scalability & Expansion

The architecture is designed for replication across other countries.

8.1 Multi-Country Support

Same core database

Multiple frontends

Country-specific configuration

8.2 AI Layer (Future)

Automated classification

Risk scoring

Duplicate detection

Predictive analytics

8.3 Integrations

Government alert systems

NGO networks

SMS gateways

Weather APIs

9. Summary

The OpenRelief Jamaica architecture is:

Modular

Secure

Scalable

Documented

Real-world tested

Ready for national deployment

It provides a robust foundation for emergency communication, demonstrating full-stack system design, backend engineering, API integration, and production-ready UX.

This documentation is suitable for technical review, investors, and innovation/GTI visa assessment.
