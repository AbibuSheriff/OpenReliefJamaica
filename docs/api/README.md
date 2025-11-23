API Integration — OpenRelief Jamaica

OpenRelief Jamaica uses secure HTTP API endpoints to communicate between the frontend and backend. These endpoints allow the system to:

- Fetch disaster reports  
- Update reports  
- Register organisations  
- Trigger email notifications  
- Handle admin workflows  

---

Authentication

All API calls require the following header:

```json
{
  "api_key": "REMOVED_FOR_SECURITY",
  "Content-Type": "application/json"
}
