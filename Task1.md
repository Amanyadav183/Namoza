# Task 1 – GTM Event Tracking Schema

## Objective

The primary objective of this tracking strategy is to measure user engagement throughout the consultation booking journey, identify drop-off points, and optimize lead generation campaigns for Google Ads and GA4.

---

# GTM Event Schema

| Event Name | Trigger | Parameters | Purpose |
|------------|----------|------------|---------|
| page_view | Page Load | page_title, page_location | Track page visits |
| consultation_form_view | Element Visibility | form_name, page_name | Measure form impressions |
| consultation_form_started | User focuses on first input | form_name | Track form starts |
| consultation_form_submitted | dataLayer.push() | patient_name, clinic_location, source | Primary lead conversion |
| booking_step_complete | dataLayer.push() | step_number, step_name | Funnel analysis |
| clinic_selected | Dropdown Change | clinic_location | Measure clinic preference |
| call_button_clicked | Click Trigger | phone_number | Measure phone enquiries |
| scroll_50 | Scroll Depth | scroll_percentage | Engagement measurement |
| scroll_90 | Scroll Depth | scroll_percentage | Deep engagement |
| testimonial_viewed | Element Visibility | testimonial_section | Trust content visibility |
| thank_you_page_view | Custom Event | conversion_status | Successful booking |

---

# Booking Funnel Events

## Step 1 – User Opens Consultation Form

```javascript
window.dataLayer.push({
    event: "booking_step_complete",
    step_number: 1,
    step_name: "consultation_started"
});
```

---

## Step 2 – User Enters Details

```javascript
window.dataLayer.push({
    event: "booking_step_complete",
    step_number: 2,
    step_name: "patient_details_entered",
    clinic_location: "Bengaluru"
});
```

---

## Step 3 – Booking Completed

```javascript
window.dataLayer.push({
    event: "consultation_form_submitted",
    patient_name: "John Doe",
    clinic_location: "Bengaluru",
    source: "Google Ads",
    form_name: "consultation_landing_page"
});
```

---

# GA4 Funnel

The booking funnel would consist of three sequential events:

1. consultation_form_started
2. booking_step_complete
3. consultation_form_submitted

This funnel enables identification of user drop-offs between viewing the form, entering their information, and successfully submitting a consultation request. Funnel Exploration in GA4 can then be used to optimize the booking journey.

---

# Google Ads Conversion Recommendation

Recommended Conversion:

consultation_form_submitted

Reason:

This event represents a completed lead submission and directly aligns with the business objective of generating consultation bookings. Optimizing Google Ads using completed consultation requests provides a stronger optimization signal than clicks or page views and helps Smart Bidding focus on high-quality leads.