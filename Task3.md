# Task 3 – Integration Design

## Objective

The objective is to integrate the landing page with HubSpot CRM, Karix WhatsApp API, and Google Ads Conversion Tracking to automate lead management and improve marketing performance.

---

# System Flow

User
   │
   ▼
Landing Page
(HTML + JavaScript)
   │
   ▼
Backend API
(Node.js / Express)
   │
   ├──────────────► HubSpot CRM
   │                 Store Lead
   │
   ├──────────────► Karix API
   │                 Send WhatsApp Confirmation
   │
   └──────────────► Google Ads
                     Conversion Tracking

---

# Step 1 – Form Submission

The user fills in:

- Full Name
- Phone Number
- Preferred Clinic (optional)

The frontend validates the data and triggers:

```javascript
window.dataLayer.push({
    event: "consultation_form_submitted"
});
```

The validated data is then sent to the backend using a secure POST request.

---

# Step 2 – HubSpot CRM

The backend receives the request and creates a new contact in HubSpot.

Example fields:

- Name
- Phone Number
- Preferred Clinic
- Lead Source = Google Ads
- Submission Time

HubSpot stores the lead and makes it available to the sales team.

---

# Step 3 – Karix WhatsApp API

After HubSpot confirms successful lead creation, the backend calls the Karix API.

Karix sends an automated WhatsApp message such as:

"Thank you for booking a consultation with OrthoNow.
Our team will contact you shortly."

This provides immediate confirmation to the user.

---

# Step 4 – Google Ads

Once the lead has been successfully stored in HubSpot, a conversion event is recorded.

This conversion is imported into Google Ads.

Google Ads Smart Bidding uses these conversion signals to optimize future campaigns for users who are more likely to submit consultation requests.

---

# Preventing Duplicate Leads

To avoid duplicate records:

1. Search HubSpot using the submitted phone number.
2. If the phone number already exists:
   - Update the existing contact instead of creating a new one.
3. If no contact exists:
   - Create a new contact.

Since a phone number is generally unique for each patient, it serves as a reliable identifier for deduplication.

---

# Error Handling

If HubSpot is unavailable:

- Store the lead in a temporary database or queue.
- Retry the request automatically.
- Log the failure for monitoring.

If Karix fails:

- Do not fail the booking.
- Retry sending the WhatsApp notification.
- Record the error in application logs.

This ensures that lead capture is never lost due to temporary third-party service failures.