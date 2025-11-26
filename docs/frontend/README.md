🎨 Frontend Documentation — OpenRelief Jamaica

The frontend of OpenRelief Jamaica is built using Base44’s component-based UI builder, delivering a fast, mobile-first interface designed for real emergency conditions such as hurricanes, outages, and low-connectivity zones.

This documentation explains the full user experience, UI decisions, page flows, and how the frontend integrates with the backend API.

1. Overview

The frontend delivers three core user flows:

1. Citizens

Submit emergency needs quickly and safely.

2. Relief Workers / NGOs

View real-time reports, filter incidents, and coordinate responses.

3. Admins

Review reports, validate organisations, and oversee activity.

Every screen is designed for clarity, speed, and emergency usability.

2. Home Page

The home screen introduces the platform and gives instant access to key actions.

Screenshots:

home-1.png

home-2.png

home-3.png

Key elements:

Hero banner with branding

Quick actions:

Report a Need

View Reports

Link for NGOs / Relief Workers to log in

Minimal, emergency-safe colour palette (red, amber, navy)

3. Report a Need

This is the most important screen for citizens.

Screenshots:

report-need.png

report-form.png

Functionality:

Fast mobile-friendly form

Structured fields:

Parish

Community

Category (water, food, shelter, medical, etc.)

Description

Household size

Reporter name (optional)

Phone number

Automatic API submission to:

POST /entities/Report


Real-time success confirmation

UI principles:

Speed: minimal scrolling

Clarity: each field clearly labelled

Security: no personal info exposed publicly

4. View Reports (Public Timeline)

Screenshots:

view-reports-1.png

view-reports-2.png

Features:

Real-time list of reports

Filters by category, region, urgency

Mobile-first cards showing:

Parish

Description

Timestamp

Household size

This page gives transparency to citizens and responders.

5. NGO / Relief Worker Section

Screenshots:

ngo-section-1.png

ngo-section-2.png

Features:

List of active NGOs

Registration form for new organisations

Integration with backend approval system

Email verification + admin approval

Role-based visibility for restricted fields

6. UI / UX Principles

The frontend follows four core principles:

1. Clarity

Simple layouts

Minimal actions per screen

Emergency-friendly colours

2. Speed

Optimised for unstable mobile networks

Lightweight UI components

Fast API calls with caching patterns

3. Safety

No sensitive information shown publicly

Anonymous reporting option

Only NGOs with approval can see detailed data

4. Consistency

Reusable UI components

Global colour + typography system

Predictable navigation

7. Components Used

Reusable components built in Base44:

ReportCard — displays incident

NGOCard — displays organisation

StatusBadge — pending / active / resolved

FormInput / Select — structured UI forms

NavSidebar — NGO dashboard navigation

Loader / Empty States — feedback on slow connections

These components reduce friction and maintain consistency across the interface.

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

All frontend actions connect directly to Base44’s Backend API:

Submit report

Register NGO

View report list

Fetch organisations

Update report status (NGOs only)

The frontend never accesses the database directly, ensuring a secure separation between UI and backend logic.

10. Summary

This frontend represents:

A real mobile-first emergency interface

A functional disaster reporting workflow

Real API integration

Live data synchronization

Professional UI/UX decisions

Clear evidence of complete product development
