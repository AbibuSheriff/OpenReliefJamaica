# Backend — OpenRelief Jamaica

This folder documents how the **backend** of OpenRelief Jamaica works.

The backend is built using **Base44’s backend engine**.  
It handles:

- Receiving API requests from the frontend  
- Validating data before it is saved  
- Applying **role-based access control**  
- Writing data into the database tables  
- Triggering **email notifications**  
- Returning JSON responses to the frontend  

---

## 1. Overview

OpenRelief Jamaica is split into:

- **Frontend (UI)** – what citizens, relief workers and admins see  
- **Backend (API + logic)** – where all the rules, checks and saving happen  
- **Database** – where reports, organisations and emails are stored  

The backend exposes secure HTTP JSON endpoints using the Base44 API.  
The frontend never talks directly to the database – it always goes through the backend.

---

## 2. Main Responsibilities

The backend is responsible for:

1. **Report handling**
   - Accept new disaster reports from citizens
   - Validate required fields (parish, community, category, description, household_size, reporter_name, contact_phone)
   - Save valid reports to the **Report** table
   - Reject invalid or incomplete reports

2. **NGO / Relief organisation management**
   - Accept registration requests from NGOs
   - Store organisation details in the **Organisation** table
   - Notify admins when a new organisation registers
   - Allow admins to approve or reject organisations

3. **Email notifications**
   - Send confirmation emails to NGOs when they register
   - Send welcome / approval emails when NGOs are approved
   - Send notifications to the admin address for new activity
   - Log all sent / failed emails in the **EmailLog** table

4. **Security & roles**
   - Enforce different permissions for:
     - **Citizen user** (public)
     - **Relief worker / NGO**
     - **Admin**
   - Protect admin-only actions behind role checks
   - Limit what anonymous users can see and do

---

## 3. Data Entities Used by the Backend

The backend mainly works with three entities (see `/docs/database` for full detail):

- **Report**
  - Stores disaster / need reports created by citizens
  - Key fields: parish, community, category, description, household_size, reporter_name, contact_phone, status

- **Organisation**
  - Stores registered NGOs and relief organisations
  - Key fields: org_name, org_type, contact_name, contact_email, contact_phone, parish_focus, approved_status

- **EmailLog**
  - Stores every email the system attempts to send
  - Key fields: email_type, recipient_email, recipient_name, subject, status (sent / failed), related organisation or report

The backend reads and writes to these tables through the Base44 API.

---

## 4. Request Lifecycle Examples

### 4.1 Citizen Submits a Report

1. Citizen opens the **“Report a Need”** page on the frontend.
2. They fill in parish, community, category, description, household size, name, and contact phone.
3. Frontend sends a POST/PUT request to the Base44 backend API endpoint for **Report**.
4. Backend:
   - Validates required fields  
   - Ensures values are in allowed ranges (e.g. positive household size)  
   - Saves the report into the **Report** table  
5. Backend returns a JSON response like:
   - `{ "success": true, "report_id": "<id>" }`
6. Frontend shows a success message to the user.

### 4.2 NGO Registers on the Platform

1. NGO opens the **Register Your Organisation** form.
2. Frontend sends the details to the backend endpoint for **Organisation**.
3. Backend:
   - Validates email address and required fields  
   - Creates a new Organisation record with status like `pending_approval`  
4. Backend triggers:
   - An **admin notification email** (new organisation registered)  
   - A **registration confirmation email** to the NGO  
5. Both emails are stored in the **EmailLog** table with status `sent` or `failed`.

### 4.3 Admin Approves an Organisation

1. Admin logs in via the **Relief Worker / Admin** dashboard.
2. Admin changes organisation status from `pending_approval` to `approved`.
3. Backend:
   - Checks that the current user has **Admin** role  
   - Updates the Organisation record  
   - Sends an **approval email** to the NGO  
   - Writes the email entry into **EmailLog**

---

## 5. Security and Roles

The backend enforces role-based access.  
High-level rules:

- **Citizen (Public / Anonymous)**
  - Can submit new **Report** records
  - Can view **public** reports (e.g. location, category, status)
  - Cannot access admin actions or edit other people’s reports

- **Relief Worker / NGO**
  - Can view reports in their focus area (parish or region)
  - Can update status fields on reports they are responding to
  - Can manage their own organisation details

- **Admin**
  - Full access to all reports and organisations
  - Can approve / reject organisations
  - Can configure triggers and security rules
  - Can view all email logs and system activity

The Base44 security settings (see `/docs/security`) define which roles can:

- Read / create / update Report
- Read / create / update Organisation
- Read EmailLog

---

## 6. Email Triggers

Email sending is handled by Base44’s trigger system + external SMTP.

Typical triggers:

- **ngo_registration_confirmation**
  - When a new Organisation is created
  - Recipient: the NGO contact_email
  - Purpose: confirm registration

- **admin_notification_new_ngo**
  - When a new Organisation is created
  - Recipient: admin inbox (e.g. `admin@openreliefjamaica.org`)
  - Purpose: notify admin to review and approve

- **ngo_approval**
  - When Organisation status changes to `approved`
  - Recipient: NGO contact_email
  - Purpose: welcome and give next steps

Each email attempt is logged in **EmailLog** with:

- `status = sent` or `failed`
- `subject`
- `email_type`
- `recipient_email`
- Timestamp

This makes it easy to debug delivery issues.

---

## 7. API Endpoints (High-Level)

The backend uses Base44 API endpoints in this pattern:

```text
GET  /api/apps/<app_id>/entities/Report
POST /api/apps/<app_id>/entities/Report
PUT  /api/apps/<app_id>/entities/Report/{entityId}

GET  /api/apps/<app_id>/entities/Organisation
POST /api/apps/<app_id>/entities/Organisation
PUT  /api/apps/<app_id>/entities/Organisation/{entityId}

GET  /api/apps/<app_id>/entities/EmailLog
