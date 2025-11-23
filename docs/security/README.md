Security Model — OpenRelief Jamaica

The platform includes a basic but effective role-based access control system to ensure only authorised users can view, edit, or administer sensitive information.

User Roles

Admin (Owner)

Full control over the platform

Can approve organisations

Can view all reports

Can manage security and settings

Can invite/remove users

Public User

Can submit disaster reports

No access to backend or dashboards

Organisation / NGO

Can view only their assigned parish or focus area

Can update or respond to relevant reports

Authentication & Access Layers
1. UI Layer Security

Buttons (delete, approve, admin tools) only show if isAdmin === true.

2. Handler Validation

Every critical operation checks isAdmin before running.

Prevents unauthorised users from modifying or deleting data.

3. Backend Enforcement

Even if someone bypasses the UI, the backend rejects unauthorised actions.

Ensures full protection against API abuse.

Screenshots Included

roles-and-users.png — Shows admin role setup

App-Level Security Overview

The OpenRelief Jamaica platform includes a centralised App Security dashboard where entity-level access policies can be configured.

Current Entity Access (Development Phase)

During early development, the following data entities are set to Public for testing and validation:

Report

Organisation

EmailLog

For each entity, Base44 shows a warning:
“All users have full access.”

This is deliberate during testing so that:

The frontend can be developed without permission blocks

Data models can be validated quickly

API examples can be tested with real entities

System flows (email, registration, NGO onboarding) can be verified end-to-end

Future Access Policies (Production Phase)

In production, the platform is designed to enforce strict access controls:

Public Users: Can submit reports but cannot view or edit any backend data

Organisations/NGOs: Can only view reports in their assigned parish or focus area

Admins: Full access to all data entities + security configuration

Security Tools

The platform includes a Security Scan feature that checks for misconfigurations, missing rules, or over-exposed data.
This is run before final deployment to ensure no sensitive information is publicly accessible.  



Additional screenshots will cover policies and access rules
