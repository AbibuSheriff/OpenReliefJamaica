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

Additional screenshots will cover policies and access rules
