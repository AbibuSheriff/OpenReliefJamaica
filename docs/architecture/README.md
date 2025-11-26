System Architecture — OpenRelief Jamaica

This folder contains the complete technical architecture of the OpenRelief Jamaica platform.
It visually explains how every part of the system works together — from users on the frontend to the backend, database, security layer, and email services.

Architecture Diagram

Below is the official architecture diagram used to represent the system:

What This Diagram Shows
1. User Groups

The system supports three different roles:

Citizen User — submits disaster needs

Relief Worker / NGO — views, updates, and manages reports

Admin User — oversees all data, approvals, and system actions

These users interact exclusively through the frontend UI.

2. Frontend Layer (Base44 UI)

This is the public-facing web interface built with Base44.
It handles:

Submitting reports

Showing reports

Displaying NGO dashboards

Admin tools

All user actions trigger API calls to the backend.

3. Backend API (Base44 API)

This is the core application logic.
It:

Receives requests

Validates data

Applies role-based access

Sends emails

Updates database tables

It is the “brain” of the system.

4. Database Layer

The backend stores and retrieves information from three main tables:

Report Table – citizen-submitted needs

Organisation Table – registered NGOs

EmailLog Table – all outgoing emails

The backend controls access to protect sensitive data.

5. Email Service

Used for:

Confirmation emails to citizens

Alert emails to relief workers

NGO registration approvals

The backend triggers these emails based on user actions.

6. Security Layer

Security is enforced across the entire system:

Role-based access control

Limited access to sensitive reports

Protected admin features

Validation before every API call

Only authorised users can perform high-level actions.
