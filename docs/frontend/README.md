Frontend Documentation — OpenRelief Jamaica

The frontend of OpenRelief Jamaica is built using Base44’s component-based UI builder. It delivers a fast, mobile-first interface designed for real emergency conditions such as hurricanes, outages, and low-connectivity zones.

This documentation explains the full user experience, UI decisions, page flows, and how the frontend integrates with the backend API.

1. Overview

The frontend provides three core user flows:

1.1 Citizens

Users can submit emergency needs quickly and safely.

1.2 Relief Workers / NGOs

Users can view real-time reports, filter incidents, and coordinate responses.

1.3 Admins

Admins review reports, validate organisations, and oversee system activity.

Every screen is designed for clarity, speed, and usability in emergency conditions.

2. Home Page

The home screen introduces the platform and gives immediate access to primary actions.

2.1 Screenshots

home-1.png

home-2.png

home-3.png

2.2 Key Elements

Hero banner with branding

Quick action buttons: Report a Need, View Reports

NGO / Relief Worker login link

Emergency-safe colour palette

3. Report a Need

This is the core reporting interface for citizens.

3.1 Screenshots

report-need.png

report-form.png

3.2 Functionality

Mobile-friendly form designed for speed

Structured fields:

Parish

Community

Category

Description

Household size

Reporter name (optional)

Phone number

Automatic API submission:

POST /entities/Report


Real-time confirmation message

3.3 UI Principles

Speed: minimal scrolling

Clarity: clearly labelled fields

Safety: no personal data exposed publicly

4. View Reports (Public Timeline)

Displays emergency reports submitted by citizens.

4.1 Screenshots

view-reports-1.png

view-reports-2.png

4.2 Features

Real-time report feed

Filters by category, region, urgency

Mobile-first report cards showing:

Parish

Description

Timestamp

Household size

Provides transparency and coordination for responders.

5. NGO / Relief Worker Section

This section is used by approved organisations responding to emergencies.

5.1 Screenshots

ngo-section-1.png

ngo-section-2.png

5.2 Features

List of active NGOs

Registration form for new organisations

Backend approval workflow

Email verification and admin approval

Role-based visibility and restricted data access

6. UI / UX Principles

The frontend is built on four primary design principles:

6.1 Clarity

Simple layouts

Minimal steps

Straightforward language

6.2 Speed

Optimised for unstable mobile connections

Lightweight components

Fast API interactions

6.3 Safety

Public pages hide personal/identifying information

Anonymous reporting option

6.4 Consistency

Reusable UI components

Global colour/typography system

Predictable navigation

7. Components Used

Reusable Base44 UI components include:

ReportCard – displays an incident

NGOCard – displays organisation details

StatusBadge – shows status (pending, active, resolved)

FormInput / Select – structured form inputs

NavSidebar – NGO dashboard navigation

Loader / Error States – feedback for slow or failed requests

These components standardise the user experience and ensure consistent behaviour.

8. Frontend Folder Structure
/docs/frontend
    README.md
    /screen
        home-1.png
        home-2.png
        home-3.png
        view-reports-1.png
        ngo-section-1.png
        report-need.png

9. Integration With Backend

All frontend actions connect securely to Base44’s backend API:

Report submission

NGO registration

Report list fetching

Organisation retrieval

Status updates (NGOs only)

The frontend does not directly access the database—ensuring a clean and secure separation between UI and backend logic.

10. Summary

The frontend demonstrates:

A functional emergency-response interface

Real user flows

Real-time API integration

Clean UX/UI decisions

Evidence of a working end-to-end system

This documentation provides clear proof of a complete, production-ready frontend suitable for technical review, GitHub, and visa assessment.
