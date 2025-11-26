API Documentation — OpenRelief Jamaica

This document provides a high-level overview of the API used by OpenRelief Jamaica.
The platform uses Base44’s backend API engine, which automatically exposes secure REST-style endpoints for all entities in the system.

The API handles communication between the frontend, backend logic, and database, ensuring that all requests follow strict validation, authentication, and role-based access rules.

1. Overview of the API Layer

The API serves as the core interface between:

Frontend forms and UI actions

Backend validation + triggers

Database storage

Email automation

All data moves through secure HTTPS JSON requests, and no client ever communicates directly with the database.

The Base44 API engine manages:

Input validation

Authentication

Role-based access control

Entity creation and updates

Error handling

Automatic response formatting

This ensures a predictable, secure, and scalable architecture.

2. Authentication

All API calls require a valid API key.

Example authentication header:

{
  "api_key": "REMOVED_FOR_SECURITY"
}


No active API keys are included in this repository.

Requests without authentication are rejected automatically by Base44.

3. API Endpoints by Entity

The OpenRelief system uses three key entities:

Report

Organisation

EmailLog

Base44 exposes standard endpoints for each entity using the following pattern:

3.1 Report Endpoints

Handles all citizen-submitted emergency reports.

GET  /api/apps/<app_id>/entities/Report
POST /api/apps/<app_id>/entities/Report
PUT  /api/apps/<app_id>/entities/Report/{entityId}


Use Cases:

Citizens submit new disaster reports

NGOs update the report status during response

Admins review all reports

3.2 Organisation Endpoints

Handles registration and management of NGOs.

GET  /api/apps/<app_id>/entities/Organisation
POST /api/apps/<app_id>/entities/Organisation
PUT  /api/apps/<app_id>/entities/Organisation/{entityId}


Use Cases:

NGOs register through the frontend

Admins approve or reject organisations

NGOs update their own organisation details

3.3 EmailLog Endpoints

Provides visibility into outbound email activity.

GET /api/apps/<app_id>/entities/EmailLog


Use Cases:

Admins audit email confirmations

Debugging email delivery failures

Tracking registration and approval emails

EmailLog cannot be updated via API — it is system-generated only.

4. Request & Response Format

All interactions use JSON.
Below are standard request examples.

4.1 Example: Create a Report
POST /api/apps/<app_id>/entities/Report

{
  "parish": "St Catherine",
  "community": "Portmore",
  "category": "Water",
  "description": "Family of 6 without clean water",
  "household_size": 6,
  "reporter_name": "John Doe",
  "contact_phone": "876-555-1234",
  "api_key": "REMOVED_FOR_SECURITY"
}


Sample response:

{
  "success": true,
  "entityId": "generated_id_here"
}

4.2 Example: NGO Registration
POST /api/apps/<app_id>/entities/Organisation

{
  "org_name": "Helping Hands",
  "org_type": "NGO",
  "contact_name": "Sarah Brown",
  "contact_email": "info@helpinghands.org",
  "parish_focus": "Kingston",
  "api_key": "REMOVED_FOR_SECURITY"
}


Backend automatically triggers:

NGO confirmation email

Admin notification email

EmailLog entry

4.3 Example: Update Report Status (NGO action)
PUT /api/apps/<app_id>/entities/Report/<entityId>

{
  "status": "in-progress",
  "api_key": "REMOVED_FOR_SECURITY"
}


Response indicates whether the update was successful.

5. Error Handling

The API uses standard HTTP error codes.

5.1 Validation Errors (400)

Triggered when:

Required fields missing

Invalid category/parish

Incorrect data types

Example response:

{
  "error": "Validation failed: community is required."
}

5.2 Unauthorized (401)

Occurs when:

API key missing

API key invalid

Role cannot access the resource

5.3 Forbidden (403)

Occurs when a user tries to perform an action they do not have permissions for.

Example:

Citizen tries to update report status

NGO tries to access admin-only resources

5.4 Internal Error (500)

Triggered by unexpected server issues.

Example:

Email service not responding

Database communication error

6. API Usage Screenshots

API screenshots are stored in:

/docs/api/screen/
    report-api.png
    organisation-api.png
    email-log-api.png


These screenshots show the actual Base44 API interface and live entity configurations.

7. Future API Enhancements
7.1 Additional Endpoints

ResponseLog endpoint for responder activity

Media upload endpoints

Multi-country routing

7.2 AI-Powered API Layer

Automatic severity scoring

Category auto-detection

Misinformation filtering

7.3 Integration APIs

Government disaster agencies

Caribbean regional alert systems

SMS gateway integrations

8. Summary

The OpenRelief API is:

Secure

Fast

Predictable

Fully documented

Easy to extend

Backed by strict validation and RBAC

It forms the backbone of the system, ensuring safe communication between frontend users, backend logic, and the core database.
