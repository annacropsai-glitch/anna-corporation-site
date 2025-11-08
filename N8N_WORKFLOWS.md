# N8N Workflow Automation Guide

## Overview
This guide provides detailed instructions for setting up n8n workflows to automate Anna Corporation's business processes.

## Prerequisites
- n8n account (cloud or self-hosted)
- Google Sheets access
- Email service (Gmail, SendGrid, etc.)
- Cal.com account
- Telegram bot (optional, for notifications)

## Workflow 1: Lead Intake & Management

### Purpose
Capture leads from website forms, validate data, store in Google Sheets, and send notifications.

### Workflow Steps

1. **Webhook Trigger**
   - Node: Webhook
   - Method: POST
   - Path: `/webhook/anna/lead`
   - Response: JSON success message

2. **Data Validation**
   - Node: Function
   - Validate required fields: name, email, phone, message
   - Check email format
   - Sanitize inputs

3. **Duplicate Check**
   - Node: Google Sheets
   - Action: Lookup
   - Search by email in Leads sheet
   - If exists, update; if not, create new

4. **Add to Google Sheets**
   - Node: Google Sheets
   - Action: Append Row
   - Sheet: Leads
   - Columns: LeadID, CreatedAt, Name, Email, Phone, Source, Niche, Status, Notes

5. **Send Auto-Response Email**
   - Node: Gmail / SendGrid
   - To: Lead's email
   - Subject: "Thank you for your interest in Anna Corporation"
   - Body: Welcome message with next steps

6. **Admin Notification**
   - Node: Telegram / Email
   - To: Admin
   - Message: "New lead: [Name] - [Email]"
   - Include link to Google Sheet

### Webhook URL Format
```
https://your-n8n-instance.com/webhook/anna/lead
```

### Sample Payload
```json
{
  "name": "Ahmed Khan",
  "email": "ahmed@example.com",
  "phone": "+1234567890",
  "region": "Middle East",
  "businessType": "E-commerce",
  "message": "Interested in AI Receptionist",
  "source": "website"
}
```

---

## Workflow 2: Demo Booking → Trial Activation

### Purpose
Automatically set up trial accounts when demos are booked via Cal.com.

### Workflow Steps

1. **Cal.com Webhook Trigger**
   - Node: Webhook
   - Method: POST
   - Path: `/webhook/anna/demo-booked`
   - Receives booking data from Cal.com

2. **Extract Booking Data**
   - Node: Function
   - Parse: name, email, booking time, timezone
   - Generate unique trial ID

3. **Create Trial Record**
   - Node: Google Sheets
   - Action: Append Row
   - Sheet: Trials
   - Columns: TrialID, UserEmail, StartDate, EndDate (7 days), Status, DemoDate

4. **Send Confirmation Email**
   - Node: Gmail
   - To: Customer
   - Subject: "Your Anna Corporation Demo is Confirmed"
   - Include: Demo time, trial activation details, preparation tips

5. **Create Calendar Event**
   - Node: Google Calendar
   - Add demo to admin calendar
   - Set reminder 1 hour before

6. **Notify Sales Team**
   - Node: Slack / Telegram
   - Message: "New demo booked: [Name] on [Date]"
   - Include customer details

---

## Workflow 3: Trial Management & Reminders

### Purpose
Monitor trial periods, send reminders, and manage trial-to-paid conversions.

### Workflow Steps

1. **Schedule Trigger**
   - Node: Cron
   - Schedule: Daily at 9:00 AM
   - Checks all active trials

2. **Fetch Active Trials**
   - Node: Google Sheets
   - Action: Read
   - Sheet: Trials
   - Filter: Status = "Active"

3. **Check Trial Status**
   - Node: Function
   - Calculate days remaining
   - Categorize: Day 1, Day 3, Day 5, Day 7 (expiring)

4. **Send Day 3 Reminder**
   - Node: Gmail
   - Condition: 3 days into trial
   - Subject: "You're halfway through your Anna Corporation trial"
   - Include: Usage tips, feature highlights

5. **Send Day 5 Reminder**
   - Node: Gmail
   - Condition: 5 days into trial
   - Subject: "2 days left in your trial"
   - Include: Pricing options, upgrade CTA

6. **Send Expiring Notice**
   - Node: Gmail
   - Condition: Trial expires today
   - Subject: "Your trial expires today - Upgrade now"
   - Include: Special offer, payment link

7. **Update Trial Status**
   - Node: Google Sheets
   - Action: Update
   - Set Status to "Expired" if trial ended
   - Set Status to "Converted" if payment received

8. **Admin Dashboard Update**
   - Node: Google Sheets
   - Update Metrics sheet
   - Track: Active trials, conversions, churn rate

---

## Workflow 4: Payment Processing & Activation

### Purpose
Handle payment confirmations and activate paid accounts.

### Workflow Steps

1. **Payment Webhook**
   - Node: Webhook
   - Method: POST
   - Path: `/webhook/anna/payment`
   - Receives payment confirmation from Wise/Bank

2. **Verify Payment**
   - Node: Function
   - Validate payment amount
   - Check transaction ID
   - Verify customer email

3. **Update Customer Record**
   - Node: Google Sheets
   - Action: Update
   - Sheet: Clients
   - Set Status to "Active"
   - Add payment date and plan

4. **Activate Services**
   - Node: HTTP Request
   - Call your service activation API
   - Enable all AI agents for customer

5. **Send Welcome Email**
   - Node: Gmail
   - To: Customer
   - Subject: "Welcome to Anna Corporation!"
   - Include: Login credentials, getting started guide

6. **Create Invoice**
   - Node: Function / PDF Generator
   - Generate invoice PDF
   - Store in Google Drive
   - Send copy to customer

7. **Update Financial Records**
   - Node: Google Sheets
   - Sheet: Payments
   - Record: Amount, Date, Plan, Customer, Status

---

## Workflow 5: System Monitoring & Alerts

### Purpose
Monitor system health, log errors, and send alerts for critical issues.

### Workflow Steps

1. **Schedule Trigger**
   - Node: Cron
   - Schedule: Every 15 minutes
   - Checks system health

2. **Check Website Status**
   - Node: HTTP Request
   - URL: Your website
   - Method: GET
   - Timeout: 10 seconds

3. **Log Response**
   - Node: Google Sheets
   - Sheet: AgentLogs
   - Record: Timestamp, Status, Response Time

4. **Error Detection**
   - Node: IF
   - Condition: Status code != 200
   - Or: Response time > 5 seconds

5. **Send Alert**
   - Node: Telegram / Email
   - To: Admin
   - Message: "⚠️ Website issue detected"
   - Include: Error details, timestamp

6. **Log Error**
   - Node: Google Sheets
   - Sheet: Errors
   - Record: Timestamp, Error Type, Details, Status

---

## Google Sheets Structure

### Leads Sheet
| Column | Type | Description |
|--------|------|-------------|
| LeadID | Text | Unique identifier |
| CreatedAt | Date | Timestamp |
| Name | Text | Full name |
| Email | Text | Email address |
| Phone | Text | Phone number |
| Source | Text | Traffic source |
| Niche | Text | Business type |
| Status | Text | Lead status |
| TrialStart | Date | Trial start date |
| TrialEnd | Date | Trial end date |
| LastContacted | Date | Last contact date |
| Notes | Text | Additional notes |

### Trials Sheet
| Column | Type | Description |
|--------|------|-------------|
| TrialID | Text | Unique identifier |
| UserEmail | Text | User email |
| StartDate | Date | Trial start |
| EndDate | Date | Trial end |
| Status | Text | Active/Expired/Converted |
| DemoDate | Date | Demo booking date |
| Plan | Text | Selected plan |

### Clients Sheet
| Column | Type | Description |
|--------|------|-------------|
| ClientID | Text | Unique identifier |
| Name | Text | Full name |
| Email | Text | Email address |
| Plan | Text | Subscription plan |
| Status | Text | Active/Inactive |
| StartDate | Date | Subscription start |
| NextBilling | Date | Next billing date |
| MRR | Number | Monthly recurring revenue |

### Payments Sheet
| Column | Type | Description |
|--------|------|-------------|
| PaymentID | Text | Unique identifier |
| Date | Date | Payment date |
| ClientID | Text | Customer reference |
| Amount | Number | Payment amount |
| Plan | Text | Plan purchased |
| Method | Text | Payment method |
| Status | Text | Success/Failed |

---

## Email Templates

### Lead Auto-Response
```
Subject: Thank you for your interest in Anna Corporation

Dear [Name],

Thank you for reaching out to Anna Corporation. We're excited to help transform your business with our halal-compliant AI automation solutions.

What happens next:
1. Our team will review your inquiry within 24 hours
2. We'll schedule a personalized demo at your convenience
3. You'll receive a 7-day free trial to experience our AI agents

In the meantime, feel free to explore our website and learn more about our services.

Best regards,
Anna Corporation Team

---
100% Halal • Shariah Compliant • Ethically Operated
```

### Trial Day 3 Reminder
```
Subject: You're halfway through your Anna Corporation trial

Hi [Name],

You're 3 days into your Anna Corporation trial! We hope you're enjoying the power of AI automation.

Here are some tips to get the most out of your trial:
• Explore all 6 AI agents
• Test the halal finance module
• Try the auto-booking feature
• Review your analytics dashboard

Need help? Reply to this email or book a support call.

Best regards,
Anna Corporation Team
```

---

## Testing Workflows

### Test Lead Intake
```bash
curl -X POST https://your-n8n-instance.com/webhook/anna/lead \
  -H "Content-Type: application/json" \
  -d '{
    "name": "Test User",
    "email": "test@example.com",
    "phone": "+1234567890",
    "message": "Test message"
  }'
```

### Test Demo Booking
```bash
curl -X POST https://your-n8n-instance.com/webhook/anna/demo-booked \
  -H "Content-Type: application/json" \
  -d '{
    "name": "Test User",
    "email": "test@example.com",
    "bookingTime": "2025-01-15T10:00:00Z"
  }'
```

---

## Troubleshooting

### Workflow Not Triggering
- Check webhook URL is correct
- Verify n8n instance is running
- Check firewall settings
- Review n8n logs

### Emails Not Sending
- Verify email credentials
- Check spam folder
- Review email service limits
- Test with different email provider

### Google Sheets Not Updating
- Check Google Sheets permissions
- Verify sheet names match exactly
- Review API quotas
- Test with manual execution

---

## Best Practices

1. **Always test workflows** before going live
2. **Set up error notifications** for critical workflows
3. **Monitor execution logs** regularly
4. **Keep credentials secure** using n8n's credential system
5. **Document custom changes** for future reference
6. **Backup workflows** regularly
7. **Use staging environment** for testing

---

## Support Resources

- n8n Documentation: https://docs.n8n.io
- Community Forum: https://community.n8n.io
- Video Tutorials: https://www.youtube.com/c/n8n-io

---

© 2025 Anna Corporation
