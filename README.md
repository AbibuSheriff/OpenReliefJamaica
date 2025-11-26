🇯🇲 OpenRelief Jamaica — National Emergency Reporting Platform

Founder: Abibu Sheriff
Mission: A free, real-time disaster reporting system built to modernise Jamaica’s crisis response infrastructure.
Tech Stack: Base44 • Firebase • JavaScript • Geolocation • REST API

What the Platform Solves

Jamaica’s recent hurricane exposed massive communication gaps:

Slow emergency response

No single national reporting channel

Conflicting information

Vulnerable communities unable to get help

OpenRelief Jamaica fixes this.
It enables citizens → responders → NGOs to communicate instantly during emergencies.

Core Capabilities
For Citizens

Submit emergency reports instantly

Share location, needs, household size, contact info

Option to report anonymously

For NGOs & Relief Workers

Live map of all incidents

Filterable by category, parish, severity

See pending / in-progress / resolved cases

Internal dashboard for fast coordination

For Admins

Approve NGOs

Review and manage reports

Monitor email logs and system behaviour

Why I Built This

During the hurricane, Jamaica had zero unified disaster reporting system.
People were stranded. Lines were down. Help was delayed.

Instead of complaining, I built a solution.

OpenRelief was created to:

Save lives

Improve emergency coordination

Give Jamaica a digital disaster-response system it never had

Provide a scalable model for other developing countries

Technology Overview
Backend (Base44 API)

Secure API endpoints

Role-based access control (Citizen / NGO / Admin)

Data validation

Email triggers (NGO confirmation, admin alerts, approvals)

Logs + audit tracking

Database (Firebase + Base44 tables)

Report

Organisation

EmailLog

Frontend

Mobile-first UI

Real-time map using geolocation

Clean reporting form

NGO dashboard

Architecture

Frontend → Backend API → Database

Email service triggers & role enforcement

Secure workflow from report → validation → dispatch

(Full diagrams in /docs/architecture)

Key Features

Real-time emergency reporting

Live incident map

Anonymous submissions

NGO approval system

Automated email notifications

Region-based access for responders

Admin dashboard

Roadmap (Next 90 Days)
Phase 1 — Stability

Add SMS reporting

Offline mode

Auto-load testing for disaster spikes

Phase 2 — Expansion

Caribbean-wide deployment

Ministry + ODPEM integration

AI classification of incoming reports

Phase 3 — Intelligence Layer

Hotspot prediction

Automated risk scoring

Weather + flood API integrations

Screenshots

(Will be added after UI finalisation.)

Status

MVP complete • Backend documented • Architecture published • Currently preparing full deployment

Want to contribute?

OpenRelief is open to partnerships with NGOs, researchers, and disaster-response organisations.
