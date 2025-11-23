Database Schema — Report Table

Table Name: Report
Purpose: Stores all disaster and emergency reports submitted by users across Jamaica.
This table powers the real-time map view and the dashboard used by relief workers, NGOs, and administrators.

Fields:
Field	Description
parish	Geographic region of the report (e.g., Kingston, St. James)
community	Specific community or district
category	Type of emergency: water, shelter, food, medical, etc.
description	Context or details submitted by the citizen
household_size	Number of people affected
reporter_name	Name used by the submitter (can be anonymous or test)
Example Rows (Test Data)

Used for validation and system testing.

"Need water asap" – household size 5 – Ann Moore

"Need shelter, have 2 kids" – Desmond

"Need help" – test account

"Mountain Side Community needs food" – Aaron Hendricks

Notes:

All data shown is test data.

No real personal information is stored or displayed.


Organisation Table

Table Name: Organisation
Purpose: Stores information about NGOs, government bodies, charities, and relief agencies that are part of the emergency-response network.
This table is used to match incoming reports to the correct organisation for response.

Fields:
Field	Description
org_name	Name of the organisation (NGO, charity, government department)
org_type	Category of organisation: NGO, Government, Charity, etc.
contact_name	Main point of contact for emergency coordination
contact_email	Email address for receiving disaster alerts
contact_phone	Emergency phone contact
parish_focus	Region(s) where the organisation is active
Example Rows (Test Data)

Used for development and testing of routing-to-organisation logic.

Global Citizens Caribbean – NGO – St. Thomas

Red Cross (Government unit) – St. Mary

Oxfam (Charity) – St. James

Notes:

All entries are sample/test organisations for system validation.

Table is used to automatically route emergency categories to matching organisations.

Ensures structured coordination during disaster events.

No real contact details are stored.

Table feeds the map API and admin dashboard.

Validated through Base44 data model configuration.

EmailLog Table

Table Name: EmailLog
Purpose: Captures all system-generated email events for NGOs, admins, and new organisations. Allows debugging, auditing, and full visibility into communication flows.

This table is essential for tracking:

onboarding emails

approvals/rejections

admin notifications

confirmation messages

failed vs successful delivery

Fields
Field	Description
email_type	The type of email sent (registration confirmation, admin notification, NGO approval, etc.)
recipient_email	Email address of the user or organisation receiving the message
recipient_name	Name of the person or admin receiving the message
subject	Subject line of the outgoing email
status	Delivery status (sent, failed)
organ_id	Organisation identifier the email relates to
Notes

All emails shown are test data for development and validation.

No real user emails are stored or displayed.

This table helps ensure the platform’s communication system is working correctly.

Failed statuses are expected for test accounts and help validate the error-handling workflow.

This contributes to the platform’s audit trail, which is important in emergency systems.
