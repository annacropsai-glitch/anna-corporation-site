# Sender.ai + n8n Integration Guide

## Overview
This guide shows you how to connect Anna Corporation's landing page with Sender.ai for email marketing and n8n for workflow automation - completely free and open source.

---

## 🎯 What This Integration Does

### Lead Capture Flow
1. **Visitor fills form** on website (Contact Form or Newsletter)
2. **Data sent to n8n** via webhook
3. **n8n processes data** and validates
4. **Lead added to Sender.ai** automatically
5. **Welcome email sent** via Sender.ai
6. **Data stored** in Google Sheets
7. **Admin notified** via email/Telegram

---

## 📋 Prerequisites

### 1. Sender.ai Account (Free)
- Sign up at: https://www.sender.net
- Free plan includes:
  - 2,500 subscribers
  - 15,000 emails/month
  - Unlimited automation
  - Email templates

### 2. n8n Instance (Free)
Choose one option:
- **n8n Cloud** (free tier): https://n8n.io
- **Self-hosted** (Docker): Free forever
- **Railway/Render**: Free hosting options

### 3. Google Sheets (Free)
- For lead storage and dashboard

---

## 🚀 Quick Setup (30 Minutes)

### Step 1: Set Up Sender.ai

1. **Create Account**
   - Go to https://www.sender.net
   - Sign up for free account
   - Verify your email

2. **Get API Key**
   - Go to Settings → API
   - Click "Generate API Key"
   - Copy and save your API key

3. **Create Email List**
   - Go to Audience → Lists
   - Click "Create New List"
   - Name it "Anna Corporation Leads"
   - Copy the List ID

4. **Create Welcome Email Template**
   - Go to Campaigns → Email Templates
   - Create new template
   - Use the template below

---

### Step 2: Set Up n8n

#### Option A: n8n Cloud (Easiest)

1. **Sign Up**
   - Go to https://n8n.io
   - Create free account
   - Activate your instance

2. **Create Workflow**
   - Click "New Workflow"
   - Name it "Anna Corp - Lead Capture"

#### Option B: Self-Hosted (Docker)

```bash
# Install n8n with Docker
docker run -it --rm \
  --name n8n \
  -p 5678:5678 \
  -v ~/.n8n:/home/node/.n8n \
  n8nio/n8n

# Access at: http://localhost:5678
```

---

### Step 3: Create n8n Workflow

#### Workflow 1: Lead Capture → Sender.ai

1. **Add Webhook Node**
   - Drag "Webhook" node to canvas
   - Method: POST
   - Path: `anna/lead`
   - Response: JSON
   - Copy webhook URL

2. **Add Function Node** (Data Processing)
   - Name: "Process Lead Data"
   - Code:
   ```javascript
   const data = $input.item.json;
   
   return {
     json: {
       email: data.email,
       firstname: data.name.split(' ')[0],
       lastname: data.name.split(' ').slice(1).join(' '),
       phone: data.phone || '',
       company: data.company || '',
       message: data.message || '',
       source: data.source || 'website',
       timestamp: new Date().toISOString()
     }
   };
   ```

3. **Add Sender.ai Node**
   - Search for "HTTP Request" node
   - Method: POST
   - URL: `https://api.sender.net/v2/subscribers`
   - Headers:
     - `Authorization`: `Bearer YOUR_SENDER_API_KEY`
     - `Content-Type`: `application/json`
   - Body:
   ```json
   {
     "email": "={{$json.email}}",
     "firstname": "={{$json.firstname}}",
     "lastname": "={{$json.lastname}}",
     "groups": ["YOUR_LIST_ID"],
     "fields": {
       "phone": "={{$json.phone}}",
       "company": "={{$json.company}}",
       "source": "={{$json.source}}"
     }
   }
   ```

4. **Add Google Sheets Node**
   - Action: Append Row
   - Sheet: "Leads"
   - Columns: Map all fields from previous node

5. **Add Email Node** (Admin Notification)
   - Use Gmail or SMTP
   - To: your-admin@email.com
   - Subject: "New Lead: {{$json.firstname}} {{$json.lastname}}"
   - Body: Include all lead details

6. **Add Sender.ai Trigger Email Node**
   - Method: POST
   - URL: `https://api.sender.net/v2/campaigns/trigger`
   - Body:
   ```json
   {
     "email": "={{$json.email}}",
     "campaign_id": "YOUR_WELCOME_EMAIL_ID"
   }
   ```

7. **Save and Activate**
   - Click "Save"
   - Toggle "Active" switch

---

#### Workflow 2: Newsletter Subscription

1. **Add Webhook Node**
   - Path: `anna/newsletter`
   - Method: POST

2. **Add Sender.ai Node**
   - Same as above but simpler
   - Only email field required

3. **Add Confirmation Email**
   - Trigger welcome series

---

### Step 4: Configure Website

1. **Create .env File**
   ```bash
   cp .env.example .env
   ```

2. **Add Webhook URLs**
   ```env
   VITE_N8N_WEBHOOK_URL=https://your-n8n-instance.com/webhook/anna/lead
   VITE_N8N_NEWSLETTER_WEBHOOK=https://your-n8n-instance.com/webhook/anna/newsletter
   ```

3. **Rebuild Application**
   ```bash
   pnpm run build
   ```

---

## 📧 Sender.ai Email Templates

### Welcome Email Template

```html
<!DOCTYPE html>
<html>
<head>
  <style>
    body {
      font-family: Arial, sans-serif;
      line-height: 1.6;
      color: #333;
    }
    .container {
      max-width: 600px;
      margin: 0 auto;
      padding: 20px;
    }
    .header {
      background: linear-gradient(135deg, #06204a, #0a3068);
      color: white;
      padding: 30px;
      text-align: center;
      border-radius: 10px 10px 0 0;
    }
    .content {
      background: white;
      padding: 30px;
      border: 1px solid #ddd;
    }
    .button {
      display: inline-block;
      background: #d4af37;
      color: white;
      padding: 12px 30px;
      text-decoration: none;
      border-radius: 5px;
      margin: 20px 0;
    }
    .footer {
      text-align: center;
      padding: 20px;
      color: #666;
      font-size: 12px;
    }
  </style>
</head>
<body>
  <div class="container">
    <div class="header">
      <h1>Welcome to Anna Corporation!</h1>
      <p>Halal. Ethical. Automated. Limitless.</p>
    </div>
    
    <div class="content">
      <p>Dear {{firstname}},</p>
      
      <p>Thank you for your interest in Anna Corporation! We're excited to help transform your business with our halal-compliant AI automation solutions.</p>
      
      <h3>What Happens Next?</h3>
      <ol>
        <li>Our team will review your inquiry within 24 hours</li>
        <li>We'll schedule a personalized demo at your convenience</li>
        <li>You'll receive a 7-day free trial to experience our AI agents</li>
      </ol>
      
      <p>In the meantime, explore what we offer:</p>
      
      <ul>
        <li>🤖 AI Receptionist - 24/7 customer service</li>
        <li>📅 Auto Booking - Intelligent scheduling</li>
        <li>📋 Complaint Agent - Automated issue resolution</li>
        <li>📱 Social Manager - Content automation</li>
        <li>💰 Halal Finance - Shariah-compliant transactions</li>
        <li>🤲 Donation Agent - Zakat management</li>
      </ul>
      
      <center>
        <a href="https://your-website.com" class="button">Explore Our Services</a>
      </center>
      
      <p>Have questions? Simply reply to this email - we're here to help!</p>
      
      <p>Best regards,<br>
      The Anna Corporation Team</p>
    </div>
    
    <div class="footer">
      <p>✓ 100% Halal Certified • Shariah Compliant • Ethically Operated</p>
      <p>© 2025 Anna Corporation. All rights reserved.</p>
      <p><a href="{{unsubscribe_url}}">Unsubscribe</a></p>
    </div>
  </div>
</body>
</html>
```

### Newsletter Template

```html
<!DOCTYPE html>
<html>
<head>
  <style>
    /* Same styles as above */
  </style>
</head>
<body>
  <div class="container">
    <div class="header">
      <h1>Thank You for Subscribing!</h1>
    </div>
    
    <div class="content">
      <p>Dear {{firstname}},</p>
      
      <p>Welcome to the Anna Corporation newsletter! You're now part of our community of forward-thinking businesses embracing halal AI automation.</p>
      
      <h3>What You'll Receive:</h3>
      <ul>
        <li>📰 Weekly industry insights</li>
        <li>💡 AI automation tips</li>
        <li>🎁 Exclusive offers</li>
        <li>📊 Case studies and success stories</li>
        <li>🚀 Product updates and new features</li>
      </ul>
      
      <center>
        <a href="https://your-website.com/blog" class="button">Read Our Blog</a>
      </center>
      
      <p>Stay tuned for valuable content!</p>
      
      <p>Best regards,<br>
      The Anna Corporation Team</p>
    </div>
    
    <div class="footer">
      <p>© 2025 Anna Corporation</p>
      <p><a href="{{unsubscribe_url}}">Unsubscribe</a></p>
    </div>
  </div>
</body>
</html>
```

---

## 🔄 Complete n8n Workflow JSON

### Import This Workflow

```json
{
  "name": "Anna Corp - Lead to Sender.ai",
  "nodes": [
    {
      "parameters": {
        "httpMethod": "POST",
        "path": "anna/lead",
        "responseMode": "responseNode",
        "options": {}
      },
      "name": "Webhook",
      "type": "n8n-nodes-base.webhook",
      "typeVersion": 1,
      "position": [250, 300]
    },
    {
      "parameters": {
        "functionCode": "const data = $input.item.json;\n\nreturn {\n  json: {\n    email: data.email,\n    firstname: data.name.split(' ')[0],\n    lastname: data.name.split(' ').slice(1).join(' '),\n    phone: data.phone || '',\n    company: data.company || '',\n    message: data.message || '',\n    source: data.source || 'website',\n    timestamp: new Date().toISOString()\n  }\n};"
      },
      "name": "Process Data",
      "type": "n8n-nodes-base.function",
      "typeVersion": 1,
      "position": [450, 300]
    },
    {
      "parameters": {
        "method": "POST",
        "url": "https://api.sender.net/v2/subscribers",
        "authentication": "genericCredentialType",
        "genericAuthType": "httpHeaderAuth",
        "sendHeaders": true,
        "headerParameters": {
          "parameters": [
            {
              "name": "Authorization",
              "value": "Bearer YOUR_API_KEY"
            }
          ]
        },
        "sendBody": true,
        "bodyParameters": {
          "parameters": [
            {
              "name": "email",
              "value": "={{$json.email}}"
            },
            {
              "name": "firstname",
              "value": "={{$json.firstname}}"
            },
            {
              "name": "lastname",
              "value": "={{$json.lastname}}"
            }
          ]
        }
      },
      "name": "Add to Sender.ai",
      "type": "n8n-nodes-base.httpRequest",
      "typeVersion": 3,
      "position": [650, 300]
    },
    {
      "parameters": {
        "values": {
          "string": [
            {
              "name": "success",
              "value": "true"
            },
            {
              "name": "message",
              "value": "Lead captured successfully"
            }
          ]
        }
      },
      "name": "Response",
      "type": "n8n-nodes-base.respondToWebhook",
      "typeVersion": 1,
      "position": [850, 300]
    }
  ],
  "connections": {
    "Webhook": {
      "main": [[{"node": "Process Data", "type": "main", "index": 0}]]
    },
    "Process Data": {
      "main": [[{"node": "Add to Sender.ai", "type": "main", "index": 0}]]
    },
    "Add to Sender.ai": {
      "main": [[{"node": "Response", "type": "main", "index": 0}]]
    }
  }
}
```

**To Import:**
1. Copy the JSON above
2. In n8n, click "..." → "Import from JSON"
3. Paste and import
4. Update API keys and URLs
5. Activate workflow

---

## 🧪 Testing the Integration

### Test Contact Form

```bash
curl -X POST https://your-n8n-instance.com/webhook/anna/lead \
  -H "Content-Type: application/json" \
  -d '{
    "name": "Ahmed Khan",
    "email": "ahmed@example.com",
    "phone": "+1234567890",
    "company": "Test Company",
    "message": "Interested in AI services",
    "source": "website_contact_form"
  }'
```

### Test Newsletter

```bash
curl -X POST https://your-n8n-instance.com/webhook/anna/newsletter \
  -H "Content-Type: application/json" \
  -d '{
    "email": "subscriber@example.com",
    "source": "newsletter_footer"
  }'
```

### Verify in Sender.ai
1. Go to Audience → Subscribers
2. Check if new subscriber appears
3. Verify all fields are populated
4. Check if welcome email was sent

---

## 📊 Google Sheets Dashboard

### Create Dashboard

1. **Create New Sheet**
   - Name: "Anna Corp Leads"

2. **Add Columns**
   ```
   | Timestamp | Name | Email | Phone | Company | Message | Source | Status | Notes |
   ```

3. **Connect to n8n**
   - Add Google Sheets node after Sender.ai node
   - Action: Append Row
   - Map all fields

4. **Add Conditional Formatting**
   - New leads: Green
   - Contacted: Yellow
   - Converted: Blue

---

## 🎨 Sender.ai Automation Sequences

### Sequence 1: Welcome Series

**Email 1** (Immediate): Welcome + Overview
**Email 2** (Day 2): Feature Highlights
**Email 3** (Day 4): Case Study
**Email 4** (Day 7): Special Offer

### Sequence 2: Trial Nurture

**Email 1** (Day 1): Trial Activated
**Email 2** (Day 3): Tips & Tricks
**Email 3** (Day 5): Upgrade Reminder
**Email 4** (Day 7): Last Chance

### Sequence 3: Newsletter

**Weekly**: Industry insights, tips, updates

---

## 🔧 Advanced Configuration

### Sender.ai Segmentation

Create segments for:
- **New Leads**: Just subscribed
- **Trial Users**: Active trial
- **Paid Customers**: Converted
- **Inactive**: No engagement

### n8n Error Handling

Add error handling nodes:
```javascript
try {
  // Main workflow logic
} catch (error) {
  // Log error
  // Send admin alert
  // Return friendly error message
}
```

### Rate Limiting

Sender.ai limits:
- 120 requests/minute
- Add delay node if sending bulk

---

## 📈 Analytics & Tracking

### Track These Metrics

1. **Lead Capture Rate**
   - Form submissions / Page views

2. **Email Open Rate**
   - Opens / Emails sent

3. **Click-Through Rate**
   - Clicks / Opens

4. **Conversion Rate**
   - Trials / Leads

5. **ROI**
   - Revenue / Marketing spend

### Sender.ai Analytics

Access at: Dashboard → Analytics
- Email performance
- Subscriber growth
- Engagement metrics
- Revenue tracking

---

## 🐛 Troubleshooting

### Issue: Webhook Not Receiving Data

**Solution:**
1. Check webhook URL is correct
2. Verify n8n workflow is active
3. Check CORS settings
4. Test with curl command

### Issue: Sender.ai API Error

**Solution:**
1. Verify API key is correct
2. Check API rate limits
3. Ensure email format is valid
4. Check List ID exists

### Issue: Duplicate Subscribers

**Solution:**
1. Enable "Update if exists" in Sender.ai
2. Add deduplication in n8n
3. Check email validation

### Issue: Emails Not Sending

**Solution:**
1. Verify email template is published
2. Check automation is active
3. Verify subscriber is in correct list
4. Check spam folder

---

## 💰 Cost Breakdown (Free Tier)

### Sender.ai Free Plan
- ✅ 2,500 subscribers
- ✅ 15,000 emails/month
- ✅ Unlimited automation
- ✅ Email templates
- ✅ Analytics

### n8n Cloud Free Plan
- ✅ 5,000 workflow executions/month
- ✅ Unlimited workflows
- ✅ 200+ integrations
- ✅ Community support

### Total Cost: $0/month

**Upgrade When:**
- Sender.ai: >2,500 subscribers ($15/month)
- n8n: >5,000 executions ($20/month)

---

## 🎯 Best Practices

### Email Marketing
1. **Personalize** every email
2. **Segment** your audience
3. **A/B test** subject lines
4. **Mobile optimize** all emails
5. **Track** everything

### Workflow Automation
1. **Test** before activating
2. **Monitor** execution logs
3. **Handle errors** gracefully
4. **Document** workflows
5. **Backup** regularly

### Data Management
1. **Clean** data regularly
2. **Validate** inputs
3. **Deduplicate** subscribers
4. **Respect** privacy
5. **Comply** with GDPR

---

## 📚 Additional Resources

### Sender.ai
- Documentation: https://docs.sender.net
- API Reference: https://api.sender.net/docs
- Support: support@sender.net

### n8n
- Documentation: https://docs.n8n.io
- Community: https://community.n8n.io
- Templates: https://n8n.io/workflows

### Video Tutorials
- Sender.ai Setup: [YouTube Link]
- n8n Basics: [YouTube Link]
- Integration Guide: [YouTube Link]

---

## ✅ Setup Checklist

- [ ] Sender.ai account created
- [ ] API key obtained
- [ ] Email list created
- [ ] Welcome email template created
- [ ] n8n instance set up
- [ ] Webhook workflow created
- [ ] Sender.ai node configured
- [ ] Google Sheets connected
- [ ] .env file updated
- [ ] Website rebuilt
- [ ] Integration tested
- [ ] Error handling added
- [ ] Analytics configured
- [ ] Documentation reviewed

---

## 🎉 You're All Set!

Your Anna Corporation landing page is now connected to Sender.ai for professional email marketing and n8n for powerful automation - all completely free!

**Next Steps:**
1. Test the integration thoroughly
2. Create your email sequences
3. Monitor analytics
4. Optimize based on data
5. Scale as you grow

---

**Need Help?**
- Check troubleshooting section
- Review n8n execution logs
- Contact Sender.ai support
- Join n8n community

**Happy Automating! 🚀**

© 2025 Anna Corporation
