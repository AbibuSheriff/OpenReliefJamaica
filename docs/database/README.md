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

Table feeds the map API and admin dashboard.

Validated through Base44 data model configuration.
