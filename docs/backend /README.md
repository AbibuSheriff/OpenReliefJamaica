Backend — OpenRelief Jamaica

This folder documents how the backend of OpenRelief Jamaica works.
The backend is built using Base44’s backend engine and handles:

Receiving API requests

Validating submitted data

Applying security rules and roles

Writing to the database

Triggering automated email notifications

Returning JSON responses to the frontend

1. Overview

The backend powers all the logic behind the platform.
It connects:

Frontend (Base44 UI) — what citizens, NGOs, and admins interact with

Backend API — where all validation and processing happens

Database — where all final data is stored

Email service — sends confirmations and alerts

Security layer — controls who can do what

The backend exposes secure JSON endpoints through Base44’s API.
The frontend never accesses the database directly — only through the backend.

2. Main Backend Responsibilities
Report Handling

Accept new disaster reports from citizens

Validate required fields

Save reports to the Report table

Reject invalid submissions

NGO / Organisation Management

Accept new organisation registrations

Store them in the Organisation table

Notify admin for approval

Email NGO with confirmation and approval status

Email Notifications

Registration confirmation

NGO approval confirmation

Admin alerts

All email activity logged in EmailLog table

Security

Enforce role-based access (Citizen, NGO, Admin)

Protect sensitive actions

Limit public access

3. Entities Used by the Backend
Report

Stores disaster-related needs.

Key fields:
parish, community, category, description, household_size, reporter_name, contact_phone, status

Organisation

Stores registered NGOs.

Key fields:
org_name, org_type, contact_name, contact_email, contact_phone, parish_focus, approved_status

EmailLog

Stores all outgoing emails.

Key fields:
email_type, recipient_email, subject, status, timestamp

4. Request Lifecycle (How Backend Works)
4.1 Citizen Submits a Report

User fills in the form

Frontend sends POST → /entities/Report

Backend validates

Backend saves

Backend returns JSON response

Frontend shows confirmation

4.2 NGO Registers

NGO submits registration

Backend saves to Organisation

Backend triggers two emails:

NGO confirmation

Admin alert

Emails are logged in EmailLog

4.3 Admin Approves Organisation

Admin changes status → approved

Backend validates admin role

Backend updates the organisation

Backend triggers an approval email

Email is logged

5. Security & User Roles

OpenRelief uses Role-Based Access Control (RBAC).

Citizen (Anonymous / Public)

Can create reports

Can view public report fields

Cannot edit or access admin areas

NGO / Relief Worker

Can update reports assigned to them

Can edit their organisation details

Can view reports in their region

Admin User

Full access

Approves organisations

Views all reports

Manages triggers

Reads email logs

These access rules are enforced in Base44’s security configuration.

6. Email Triggers (Backend Automations)

Email sending is automated inside the backend logic using Base44 triggers.

Trigger: NGO Registration Confirmation

Event: new Organisation created

Recipient: NGO’s contact_email

Purpose: welcome message

Trigger: Admin Alert (New Organisation)

Notifies admin that an NGO is awaiting approval

Trigger: NGO Approval Email

Event: organisation status changes to approved

Recipient: NGO

Purpose: approval + instructions

Every email is logged to the EmailLog table with:

sent or failed

timestamp

subject

recipient

7. API Endpoints (High-Level)

All backend endpoints follow Base44’s API structure:

Report
GET  /api/apps/<app_id>/entities/Report
POST /api/apps/<app_id>/entities/Report
PUT  /api/apps/<app_id>/entities/Report/{entityId}

Organisation
GET  /api/apps/<app_id>/entities/Organisation
POST /api/apps/<app_id>/entities/Organisation
PUT  /api/apps/<app_id>/entities/Organisation/{entityId}

EmailLog
GET  /api/apps/<app_id>/entities/EmailLog

Authentication

All calls require:

{
  "api_key": "REMOVED_FOR_SECURITY"
}


Actual keys are not included in this repository.

8. Backend Architecture Diagram
Citizen User ─┐
NGO Worker ───┼──> [Frontend UI] → [Backend API] → [Database]
Admin User ───┘

              → Triggers → Email Service
              → Security → Role Enforcement
