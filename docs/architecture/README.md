README.md for /docs/architecture/

System Architecture — OpenRelief Jamaica

This folder contains the high-level architecture for the OpenRelief Jamaica platform.
It explains how all major parts of the system work together — frontend, backend, security, database, and external services.

Architecture Overview

OpenRelief Jamaica is built on three core layers:

1. Frontend Layer (Base44 UI)

Accepts report submissions

Displays public reports

Provides NGO login + admin dashboard

Communicates with backend over secure HTTPS (JSON)

2. Backend API (Base44 API Engine)

Handles incoming requests

Validates all submitted data

Applies role-based access control (Citizen / NGO / Admin)

Sends email notifications

Reads + writes database entities

3. Database Layer (Base44 Data Tables)

Report Table — stores citizen-submitted needs

Organisation Table — stores verified NGOs

EmailLog Table — tracks all outgoing email notifications

Email Service

Automatic emails are triggered by the backend:

Report confirmations

NGO account approval

Status update notifications

Security Layer

Security is enforced at multiple levels:

Role-based access

Admin-only actions protected

Limited public read access

All calls require API key authentication

No direct access to underlying tables

Diagram

See: system-architecture.png
This image provides a visual map of the system, showing how users, frontend, backend, emails, and data layers interact.

Purpose of This Folder

This directory exists to:

Document technical architecture

Support visa evidence requirements

Provide clarity for developers, grant reviewers, and contributors

Show professional system design standards
