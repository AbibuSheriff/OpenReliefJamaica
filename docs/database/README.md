Database Documentation — OpenRelief Jamaica

This document explains the full database structure used by OpenRelief Jamaica, including all entities, fields, relationships, and data-handling rules. The platform uses Base44’s internal database engine + Firebase for persistence and real-time syncing.

The database is designed to be simple, fast, and safe, optimised for emergency-response workflows and low-connectivity environments.

1. Overview

The database layer consists of three core entities:

Report — citizen-submitted emergency information

Organisation — registered NGOs and relief teams

EmailLog — logging system for all outbound email notifications

Each entity is tightly integrated with the backend API and governed by role-based access controls documented in /docs/security.

The database is fully managed through Base44 and is not directly accessible from the frontend for security reasons.

2. Entities and Field Definitions
2.1 Report Entity

Stores all citizen-submitted emergency reports.

Purpose:
Capture urgent needs during emergencies in a consistent and structured format.

Key Fields:

Field Name	Type	Description
parish	Text	Parish where the incident occurred
community	Text	Community or district
category	Text	Type of need (water, food, shelter, medical, etc.)
description	Text	Summary of the situation
household_size	Number	Number of people affected
reporter_name	Text	Optional citizen name
contact_phone	Text	Optional phone number
status	Text	pending / in-progress / resolved
created_at	DateTime	Timestamp of submission

Notes:

Personal details never appear on public pages

NGOs only see reports in their assigned region

Status is updated by verified responders only

2.2 Organisation Entity

Stores all NGOs, charities, and emergency units that register to respond to reports.

Purpose:
Provide a verified network of legitimate relief organisations.

Key Fields:

Field Name	Type	Description
org_name	Text	Organisation name
org_type	Text	NGO, government agency, community group
contact_name	Text	Main contact person
contact_email	Text	Email for verification
contact_phone	Text	Phone number
parish_focus	Text	Region where organisation operates
approved_status	Text	pending / approved / rejected
created_at	DateTime	Registration timestamp

Notes:

Organisations must be approved by an admin

Approved NGOs gain access to restricted data

Rejected NGOs cannot log in or view reports

2.3 EmailLog Entity

Tracks all outgoing email notifications.

Purpose:
Provide a transparent audit trail of system actions, including:

NGO registration confirmations

Admin alert notifications

NGO approval responses

Key Fields:

Field Name	Type	Description
email_type	Text	registration, admin_alert, approval
recipient_email	Text	Recipient’s email
recipient_name	Text	Optional name
subject	Text	Email subject line
status	Text	sent / failed
timestamp	DateTime	Sent time

Notes:

Only admins can view this table

Useful for diagnosing email failures or SMTP issues

3. Data Relationships

The system currently uses loose relational links between entities, managed at the application level:

3.1 Report → Organisation

NGOs can update the status of reports in their region

No hard foreign key enforced for simplicity

Application logic handles matching based on parish/operation area

3.2 Organisation → EmailLog

Emails with type registration and approval are linked by organisation email

3.3 Report → EmailLog (optional)

Email logs may reference report submissions if needed (e.g., future confirmation emails)

4. Data Handling Rules
4.1 Validation Rules

Required fields must be completed (parish, community, category, description, household size)

Phone numbers validated for digits

Email fields validated on organisation submission

Status fields restricted to allowed values

4.2 Sanitisation

Base44 sanitises all incoming input to prevent:

Script injection

Malformed fields

Invalid data types

4.3 Privacy Controls

Personal details are hidden from public views

NGOs only access data relevant to their region

Only admins access full records

4.4 Soft Security

No citizen-submitted data is ever publicly linked to an identity

Reporters may remain fully anonymous

5. Database Screenshots

Screenshots of the entities are stored in:

/docs/database/screen/
    report-table.png
    organisation-table.png
    email-log-table.png


These demonstrate the actual table structure inside Base44.

6. Future Data Enhancements
6.1 Additional Entities

ResponseLog

Attachment / media support

Location coordinates

6.2 Analytics Layer

Hotspot detection

Report clustering

Automated severity scoring

6.3 Multi-Country Extensions

Database can be expanded with:

country_code

region_code

multi-country report routing

7. Summary

The OpenRelief Jamaica database is:

Lightweight

Fast

Secure

Easy to scale

Built for emergency conditions

It provides a clean structure for report submission, NGO management, and email auditing, supporting a full end-to-end emergency reporting platform.
