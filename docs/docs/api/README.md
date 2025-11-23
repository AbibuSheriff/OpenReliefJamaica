// JavaScript Example — Fetching Report Entities
async function fetchReportEntities() {
  const response = await fetch("https://app.base44.com/api/apps/6909b605ca9bd588edc945b4/entities/Report", {
    headers: {
      api_key: "REMOVED_FOR_SECURITY",
      "Content-Type": "application/json"
    }
  });

  const data = await response.json();
  console.log(data);
}

// JavaScript Example — Updating a Report Entity
async function updateReportEntity(entityId, updateData) {
  const response = await fetch(`https://app.base44.com/api/apps/6909b605ca9bd588edc945b4/entities/Report/${entityId}`, {
    method: "PUT",
    headers: {
      api_key: "REMOVED_FOR_SECURITY",
      "Content-Type": "application/json"
    },
    body: JSON.stringify(updateData)
  });

  const data = await response.json();
  console.log(data);
}
