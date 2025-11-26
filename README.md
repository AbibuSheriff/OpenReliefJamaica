OpenRelief Jamaica — National Emergency Reporting Platform

Founder: Abibu Sheriff
Category: Emergency Response • GovTech • Crisis Communication
Tech Stack: Base44 • Firebase • JavaScript • REST API • Geolocation

OpenRelief Jamaica is a national disaster-reporting system built to modernise Jamaica’s emergency response during hurricanes, floods, and island-wide crises. It connects citizens, NGOs, and emergency teams in real time through a fast, mobile-first interface.

The system is designed to operate in low-connectivity environments and provide a scalable model that can be replicated across developing countries without strong 911/112/999 infrastructures.

1. Purpose of the Platform

During Jamaica’s recent hurricane, communication systems broke down, response times collapsed, and vulnerable communities struggled to get help. There was no unified reporting channel.

OpenRelief Jamaica was built to solve exactly that.

The platform:

Enables real-time emergency reporting

Displays live incidents for responders

Helps NGOs coordinate resources

Reduces delays during national disasters

Provides transparency for citizens and authorities

This is a free public tool designed to strengthen Jamaica’s national resilience and support emergency workers.

2. Key Features
2.1 Citizen Tools

Submit emergency reports

Share location, needs, and household data

Report anonymously if required

Fast mobile-first design

2.2 NGO / Responder Tools

Live timeline of all reports

Filter by parish, category, urgency

Dashboard for approved organisations

Real-time updates and status changes

2.3 Admin Tools

Approve new NGOs

Review incoming reports

Access email logs and system activity

Oversee responder coordination

3. System Architecture Overview

OpenRelief Jamaica is structured into three core layers:

3.1 Frontend

Base44 component-driven UI

Mobile-first design

Real-time form submission

Public and role-based pages

3.2 Backend

Base44 API engine

Validates all incoming data

Handles logic, permissions, and workflows

Sends automated email notifications

3.3 Database

Report table

Organisation table

EmailLog table

Secure, role-gated storage

The full architecture diagram is in:
/docs/architecture/system-architecture.png

4. Documentation Structure

All documentation is included inside the /docs/ directory.

/docs
   /frontend      ← Full UI documentation + screenshots
   /backend       ← API, roles, triggers, lifecycle behaviour
   /database      ← Table structures + field definitions
   /security      ← Role-based access + permission rules
   /api           ← High-level API summary + examples
   /architecture  ← System architecture diagram


Each folder contains a dedicated README.md explaining its functionality.

5. Technology Breakdown
5.1 Frontend

Built entirely using Base44 UI builder

Reusable components (ReportCard, NGOCard, StatusBadge, etc.)

Real-time API calls

Optimised for unstable mobile networks

5.2 Backend

Base44 API endpoints

Request validation

Role-based access control

Email triggers for registration and approvals

Logging via EmailLog entity

5.3 Database

Firebase + Base44 tables

Structured entries for reports, organisations, email logs

Secure separation between public and admin data

6. Future Roadmap

(Not required to be completed — roadmap for vision and planning)

6.1 Phase 1 — Platform Enhancements

SMS reporting

Offline reporting mode

Enhanced admin dashboard

6.2 Phase 2 — Regional Expansion

Rollout to other Caribbean and African countries

Multi-country backend support

Multi-language versions

6.3 Phase 3 — Intelligence Layer

AI-powered report classification

Hotspot prediction using environmental data

Integration with government and NGO networks

7. Screenshots

All screenshots for the frontend, backend, database, and security can be found in the respective documentation folders within /docs.

8. Status

MVP complete

Backend and frontend documentation complete

Architecture published

Code and API structure documented

Ready for further scaling and deployment

9. Contribution & Contact

OpenRelief Jamaica is actively open to collaboration with:

NGOs

Emergency response teams

Local government units

International disaster groups

For collaboration or inquiry:
Founder: Abibu Sheriff

Summary

OpenRelief Jamaica is a fully documented, working emergency reporting system designed for real-world national crisis response. The platform demonstrates clear technical design, real API integration, and a scalable model that can be extended across multiple countries.

This repository serves as evidence of:

Full-stack system architecture

Backend engineering capability

UI/UX design

Real production-ready workflows

End-to-end product ownership
