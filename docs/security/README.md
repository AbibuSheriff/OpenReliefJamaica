Security Documentation — OpenRelief Jamaica

This document explains the full security model for OpenRelief Jamaica, including role-based access control (RBAC), data protection rules, endpoint security, and backend validation. It reflects how the platform protects sensitive information during disaster situations while ensuring fast access for legitimate responders.

The system uses Base44’s built-in security framework for permissions, access rules, and entity-level restrictions.

1. Overview

OpenRelief Jamaica handles sensitive emergency information.
To ensure safety, the entire platform is built around three pillars:

1.1 Role-Based Access Control (RBAC)

Different users see different information depending on their role.

1.2 Data Protection & Field-Level Security

Personal data is hidden from public users and anonymised where required.

1.3 Secure API Layer

All data access goes through Base44’s authenticated backend endpoints.

This creates a secure, auditable workflow from the moment a report is submitted to the moment a responder takes action.

2. User Roles

The platform uses three primary roles with strict separation of permissions.

2.1 Citizen (Public / Anonymous)

Can submit new emergency reports

Can view public fields of existing reports

Cannot edit or delete reports

Cannot access NGO dashboards or admin tools

Personal identifying information is hidden from citizens

2.2 NGO / Relief Worker

Must be approved by an admin

Can view reports within their parish or operation area

Can update report statuses (e.g., “in-progress”, “resolved”)

Can edit their organisation profile

Cannot access system-wide admin actions

2.3 Admin

Full access to all reports and organisations

Can approve or reject NGOs

Can view and manage EmailLog

Can change security rules

Can oversee all backend triggers and workflows

This structure ensures maximum transparency for the public, while reserving sensitive tools for trusted users.

3. Entity Security Rules

OpenRelief Jamaica uses entity-level permissions to control how each role interacts with the data.

3.1 Report Table Security

Citizen

Create: Yes

Read: Only public fields

Update/Delete: No

NGO

Create: No

Read: Allowed within their assigned region

Update: Yes (status field only)

Delete: No

Admin

Create/Read/Update/Delete: Yes

Sensitive fields (e.g., contact phone, name) are never exposed publicly.

3.2 Organisation Table Security

Citizen

Read: Only approved organisations

Create: Yes (registration form)

Update/Delete: No

NGO

Read: Own organisation only

Update: Yes

Create/Delete: No

Admin

Full access

Approves new NGOs

Controls activation status

3.3 EmailLog Table Security

Citizen

No access

NGO

No access

Admin

Full read access

Used for debugging email failures and delivery

This ensures internal logs are restricted only to trusted system administrators.

4. API Security

All API access goes through Base44’s backend engine, protected by:

4.1 API Key Authentication

Every request requires a valid API key:

{
  "api_key": "REMOVED_FOR_SECURITY"
}


Keys are never stored in the repository.
No request is processed without an authenticated key.

4.2 Input Validation

The backend validates:

Required fields

Email format

Phone number format

Allowed categories

Region/Parish names

Invalid or unsafe input is rejected with clear JSON errors.

4.3 Role Checks

Before any update, the backend verifies:

User role

Region access

Action permission (read / create / update / restricted fields)

5. Data Protection Measures

OpenRelief Jamaica follows strict data protection rules:

5.1 Personal Data Separation

Fields such as name and phone number are:

Never shown publicly

Only visible to approved NGOs and admins

Stored in restricted columns

5.2 Anonymous Mode

Citizens can submit reports without providing personal information.

5.3 No Direct Database Access

Frontend never connects directly to Firebase or Base44 tables.
All access flows through the backend API.

5.4 Email Safety

Outgoing emails are sent using safe templates and logged in EmailLog for auditing.

6. Threat Prevention

The platform includes safeguards against common attack vectors.

6.1 Spam / Fake Report Prevention

Required field validation

Region-based filtering

NGO/admin approval before responding

Automatic review workflows

6.2 Injection Prevention

Base44’s API engine sanitises input to prevent:

Script injection

Malformed data

API misuse

6.3 Abuse Prevention

Admins can:

Remove malicious organisations

Update security rules

Disable access within seconds

7. Summary

The OpenRelief security model ensures:

Citizens can report safely

NGOs only access what they need

Admins maintain full control

Sensitive data stays protected

Backend logic enforces strict permissions

All actions go through secure API endpoints

This provides a reliable, trust-based emergency communication platform that protects both citizens and responders while maintaining transparency and speed during national crises.
