# Integration Quick Start - 15 Minutes Setup

## 🚀 Get Your Lead Generation Running in 15 Minutes

This is the fastest way to connect your Anna Corporation landing page with Sender.ai and n8n.

---

## Step 1: Sender.ai Setup (5 minutes)

### 1.1 Create Account
```
1. Go to: https://www.sender.net
2. Click "Sign Up Free"
3. Enter email and password
4. Verify your email
```

### 1.2 Get API Key
```
1. Click Settings (gear icon)
2. Click "API" in left menu
3. Click "Generate API Key"
4. Copy the key (starts with "eyJ...")
5. Save it somewhere safe
```

### 1.3 Create Your First List
```
1. Click "Audience" in top menu
2. Click "Lists"
3. Click "Create New List"
4. Name: "Website Leads"
5. Click "Create"
6. Copy the List ID (you'll see it in the URL)
```

**✅ Done! You now have:**
- Sender.ai account
- API key
- List ID

---

## Step 2: n8n Setup (5 minutes)

### Option A: n8n Cloud (Recommended)

```
1. Go to: https://n8n.io
2. Click "Start Free"
3. Sign up with email
4. Wait for instance to activate (2-3 minutes)
5. Click "Open n8n"
```

### Option B: Quick Docker Install

```bash
# Run this one command
docker run -d --restart unless-stopped \
  --name n8n \
  -p 5678:5678 \
  -v ~/.n8n:/home/node/.n8n \
  n8nio/n8n

# Access at: http://localhost:5678
```

**✅ Done! Your n8n is ready**

---

## Step 3: Create Workflow (3 minutes)

### 3.1 Import Workflow

1. **Copy this workflow:**

```json
{
  "name": "Anna Corp Lead Capture",
  "nodes": [
    {
      "parameters": {
        "httpMethod": "POST",
        "path": "anna/lead",
        "responseMode": "lastNode",
        "options": {}
      },
      "name": "Webhook",
      "type": "n8n-nodes-base.webhook",
      "typeVersion": 1,
      "position": [240, 300],
      "webhookId": "anna-lead-webhook"
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
              "value": "=Bearer YOUR_SENDER_API_KEY"
            },
            {
              "name": "Content-Type",
              "value": "application/json"
            }
          ]
        },
        "sendBody": true,
        "contentType": "json",
        "body": "={\"email\": \"{{$json.email}}\", \"firstname\": \"{{$json.name}}\", \"groups\": [\"YOUR_LIST_ID\"]}",
        "options": {}
      },
      "name": "Add to Sender",
      "type": "n8n-nodes-base.httpRequest",
      "typeVersion": 3,
      "position": [460, 300]
    },
    {
      "parameters": {
        "respondWith": "json",
        "responseBody": "={\"success\": true, \"message\": \"Lead captured successfully\"}",
        "options": {}
      },
      "name": "Respond",
      "type": "n8n-nodes-base.respondToWebhook",
      "typeVersion": 1,
      "position": [680, 300]
    }
  ],
  "connections": {
    "Webhook": {
      "main": [[{"node": "Add to Sender", "type": "main", "index": 0}]]
    },
    "Add to Sender": {
      "main": [[{"node": "Respond", "type": "main", "index": 0}]]
    }
  }
}
```

2. **Import to n8n:**
   - Click "..." (three dots) in top right
   - Click "Import from JSON"
   - Paste the workflow
   - Click "Import"

3. **Update Credentials:**
   - Click on "Add to Sender" node
   - Replace `YOUR_SENDER_API_KEY` with your actual API key
   - Replace `YOUR_LIST_ID` with your list ID
   - Click "Execute Node" to test

4. **Get Webhook URL:**
   - Click on "Webhook" node
   - Click "Copy URL" button
   - Save this URL (looks like: `https://your-n8n.app.n8n.cloud/webhook/anna/lead`)

5. **Activate Workflow:**
   - Toggle the switch at top to "Active"
   - Workflow is now live!

**✅ Done! Your workflow is running**

---

## Step 4: Connect Website (2 minutes)

### 4.1 Update Environment Variables

1. **Create .env file:**
```bash
cd /workspace/app-7eqagciz514x
cp .env.example .env
```

2. **Edit .env file:**
```env
VITE_N8N_WEBHOOK_URL=https://your-n8n-instance.com/webhook/anna/lead
```
Replace with your actual webhook URL from Step 3.4

3. **Rebuild:**
```bash
pnpm run build
```

**✅ Done! Website is connected**

---

## Step 5: Test Everything (2 minutes)

### 5.1 Test from Terminal

```bash
curl -X POST https://your-n8n-instance.com/webhook/anna/lead \
  -H "Content-Type: application/json" \
  -d '{
    "name": "Test User",
    "email": "test@example.com",
    "phone": "+1234567890",
    "company": "Test Co",
    "message": "Testing integration"
  }'
```

**Expected Response:**
```json
{"success": true, "message": "Lead captured successfully"}
```

### 5.2 Verify in Sender.ai

1. Go to Sender.ai dashboard
2. Click "Audience" → "Subscribers"
3. You should see "test@example.com"

### 5.3 Test from Website

1. Open your website
2. Scroll to contact form
3. Fill out the form
4. Click "Send Message"
5. You should see success message

**✅ Done! Everything is working**

---

## 🎉 You're Live!

Your lead generation system is now fully operational:

- ✅ Contact form captures leads
- ✅ Newsletter subscription works
- ✅ Leads automatically added to Sender.ai
- ✅ Ready to send email campaigns

---

## 📧 Next Steps (Optional)

### Create Welcome Email (5 minutes)

1. **In Sender.ai:**
   - Go to "Automation"
   - Click "Create Automation"
   - Choose "Welcome New Subscribers"
   - Customize the email
   - Activate automation

2. **Test:**
   - Submit another test lead
   - Check if welcome email arrives

### Add Google Sheets (5 minutes)

1. **In n8n workflow:**
   - Add "Google Sheets" node after "Add to Sender"
   - Connect your Google account
   - Choose "Append Row"
   - Select your spreadsheet
   - Map fields
   - Save and activate

---

## 🐛 Quick Troubleshooting

### Problem: "Webhook not found"
**Solution:** Make sure workflow is activated (toggle switch is ON)

### Problem: "API key invalid"
**Solution:** 
1. Go to Sender.ai → Settings → API
2. Generate new API key
3. Update in n8n workflow

### Problem: "CORS error"
**Solution:** This is normal in development. Deploy to production to fix.

### Problem: Form not submitting
**Solution:**
1. Check .env file has correct webhook URL
2. Rebuild: `pnpm run build`
3. Clear browser cache

---

## 📊 Monitor Your Leads

### In Sender.ai
- Dashboard → See subscriber count
- Audience → View all leads
- Analytics → Track email performance

### In n8n
- Click "Executions" tab
- See all workflow runs
- Check for errors

---

## 💡 Pro Tips

1. **Test First**: Always test with your own email first
2. **Check Spam**: Make sure emails aren't going to spam
3. **Monitor Daily**: Check n8n executions daily
4. **Backup**: Export n8n workflow regularly
5. **Scale**: Upgrade plans as you grow

---

## 📞 Need Help?

### Common Issues
- Check SENDER_N8N_INTEGRATION.md for detailed guide
- Review n8n execution logs
- Test webhook with curl command

### Resources
- Sender.ai Docs: https://docs.sender.net
- n8n Docs: https://docs.n8n.io
- Community: https://community.n8n.io

---

## ✅ Final Checklist

- [ ] Sender.ai account created
- [ ] API key obtained
- [ ] List created in Sender.ai
- [ ] n8n instance running
- [ ] Workflow imported and activated
- [ ] Webhook URL copied
- [ ] .env file updated
- [ ] Website rebuilt
- [ ] Test lead submitted
- [ ] Lead appears in Sender.ai
- [ ] Welcome email created (optional)
- [ ] Google Sheets connected (optional)

---

## 🎊 Congratulations!

You've successfully set up a professional lead generation system in just 15 minutes!

**Your system now:**
- ✅ Captures leads automatically
- ✅ Stores them in Sender.ai
- ✅ Sends welcome emails
- ✅ Tracks everything
- ✅ Costs $0/month

**Start collecting leads and growing your business! 🚀**

---

© 2025 Anna Corporation - Halal. Ethical. Automated. Limitless.
