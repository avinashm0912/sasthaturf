# Boundary Box Cricket Turf — Static Booking Website

## Files
- `index.html` — landing page and booking UI
- `style.css` — responsive design
- `script.js` — 14-day calendar, 30-minute slots and demo booking logic

## Run locally
Open `index.html` directly in a browser, or use VS Code Live Server.

## Current behavior
- Shows the next 14 days using the English/Gregorian calendar.
- Generates 30-minute slots from 06:00 to 23:00.
- Selecting a slot and confirming a booking stores the slot in browser `localStorage`.
- A booked slot is displayed as unavailable in that browser.
- This is NOT a production booking system because there is no shared database.

## Before AWS production deployment
Recommended architecture:

Browser
  -> Amazon CloudFront
  -> Amazon S3 (static website)
  -> Amazon API Gateway
  -> AWS Lambda
  -> Amazon DynamoDB

Optional:
- Amazon Cognito for customer login
- Amazon SES/SNS for email/SMS notifications
- Razorpay/Stripe for online payments
- CloudWatch for logs/monitoring

## Backend data model idea

Booking:
{
  "bookingId": "UUID",
  "turfId": "turf-001",
  "date": "2026-10-01",
  "startTime": "18:00",
  "endTime": "18:30",
  "customerName": "Customer",
  "customerPhone": "+91XXXXXXXXXX",
  "status": "CONFIRMED",
  "createdAt": "ISO-8601 timestamp"
}

Use a DynamoDB key strategy that prevents two customers from successfully booking the same turf/date/time slot. The backend must perform the final availability check atomically; do not rely on localStorage for real bookings.

## Customization
Edit these values at the top of `script.js`:
- `OPEN_TIME`
- `CLOSE_TIME`
- `SLOT_PRICE`

Replace the sample location, phone number, email, WhatsApp number and Google Maps link in `index.html`.
