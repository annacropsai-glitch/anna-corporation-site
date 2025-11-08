# Welcome to Your Miaoda Project
Miaoda Application Link URL
    URL:https://medo.dev/projects/app-7eqagciz514x

# Anna Corporation - Cinematic 3D Landing Page

> **Halal. Ethical. Automated. Limitless.**

A production-ready landing page with full lead generation capabilities using Sender.ai and n8n automation.

---

## 🎉 What's Included

 **Cinematic 3D Landing Page** - Professional design with Islamic geometric influences  
 **Lead Generation System** - Automatic capture with Sender.ai + n8n  
 **Contact Form** - Fully functional with validation  
 **Newsletter Subscription** - Integrated with email automation  
 **6 AI Service Features** - Showcasing your offerings  
 **Pricing Section** - 3 pricing tiers  
 **Testimonials** - Customer reviews carousel  
 **100% Free Tools** - Sender.ai + n8n free tiers  

---

## 🚀 Quick Start (15 Minutes)

### 1. Install Dependencies
```bash
pnpm install
```

### 2. Set Up Lead Generation
Follow the **15-minute setup guide**: `docs/INTEGRATION_QUICKSTART.md`

Quick steps:
1. Create Sender.ai account (5 min)
2. Set up n8n instance (5 min)
3. Import workflow (3 min)
4. Update .env file (2 min)

### 3. Configure Environment
```bash
# Copy example environment file
cp .env.example .env

# Edit .env and add your webhook URLs
VITE_N8N_WEBHOOK_URL=https://your-n8n-instance.com/webhook/anna/lead
```

### 4. Run Development Server
```bash
pnpm run dev
```

### 5. Build for Production
```bash
pnpm run build
```

---

## 📚 Documentation

### For Quick Setup
- **15-Minute Integration Guide** (`docs/INTEGRATION_QUICKSTART.md`) - Get lead generation working fast
- **Quick Reference Card** (`docs/QUICK_REFERENCE.md`) - Common tasks and commands

### For Developers
- **Setup Guide** (`docs/SETUP.md`) - Technical setup and customization
- **Deployment Guide** (`docs/DEPLOYMENT.md`) - Deploy to Vercel, GitHub Pages, Netlify
- **Sender.ai + n8n Integration** (`docs/SENDER_N8N_INTEGRATION.md`) - Complete integration guide
- **n8n Workflows** (`docs/N8N_WORKFLOWS.md`) - Automation workflow details

### For Business Users
- **CEO Quickstart** (`docs/CEO_QUICKSTART.md`) - Non-technical management guide
- **Launch Checklist** (`docs/LAUNCH_CHECKLIST.md`) - Pre-launch and post-launch tasks
- **Project Summary** (`docs/PROJECT_SUMMARY.md`) - Complete project overview

### Complete Deliverables
- **DELIVERABLES.md** - Full list of what's included

---

## 🎨 Features

### Landing Page Sections
- **Hero** - Cinematic 3D globe with parallax effects
- **Features** - 6 AI service cards with hover animations
- **Demo Video** - Video showcase section
- **Testimonials** - Customer reviews carousel
- **Pricing** - 3 pricing tiers comparison
- **Contact Form** - Lead capture with validation
- **Footer** - Newsletter subscription + links

### Lead Generation
- ✅ Automatic lead capture to Sender.ai
- ✅ Welcome email automation
- ✅ Newsletter management
- ✅ Google Sheets integration
- ✅ Admin notifications
- ✅ Error handling

### Design
- ✅ Cinematic 3D effects
- ✅ Islamic geometric patterns
- ✅ Smooth animations
- ✅ Fully responsive
- ✅ Brand colors (Sapphire Blue, Gold, Emerald Green)

---

## 🛠️ Technology Stack

- **Frontend**: React 18 + TypeScript
- **Styling**: Tailwind CSS + shadcn/ui
- **Build Tool**: Vite
- **Email Marketing**: Sender.ai (free tier)
- **Automation**: n8n (free tier)
- **Hosting**: Vercel / GitHub Pages / Netlify

---

## 📁 Project Structure

```
anna-corporation-site/
 src/
   ├── components/
   │   ├── landing/          # Landing page components
   │   │   ├── Hero.tsx
   │   │   ├── Features.tsx
   │   │   ├── ContactForm.tsx
   │   │   └── ...
   │   └── ui/               # shadcn/ui components
   ├── pages/
   │   └── Index.tsx         # Main landing page
   └── index.css             # Design system
 docs/                     # Documentation
   ├── INTEGRATION_QUICKSTART.md
   ├── SENDER_N8N_INTEGRATION.md
   ├── DEPLOYMENT.md
   └── ...
 .env.example              # Environment variables template
 package.json
```

---

## 🔧 Configuration

### Update Contact Information
Edit `src/components/landing/Footer.tsx`:
- Email: `info@annacorp.com`
- Phone: `+1 (234) 567-890`

### Update Cal.com Booking Link
Edit `src/components/landing/Hero.tsx` (line 71):
```typescript
onClick={() => window.open('YOUR_CAL_COM_LINK', '_blank')}
```

### Update Pricing
Edit `src/components/landing/Pricing.tsx` (line 6):
```typescript
const pricingPlans = [
  { name: "One-time", price: "$2,999", ... }
]
```

---

## 🚀 Deployment

### Deploy to Vercel (Recommended)
```bash
# 1. Push to GitHub
git add .
git commit -m "Initial commit"
git push

# 2. Connect to Vercel
# - Go to vercel.com
# - Import GitHub repository
# - Add environment variables
# - Deploy automatically
```

### Deploy to GitHub Pages
```bash
pnpm run build
# Deploy dist folder to GitHub Pages
```

See `docs/DEPLOYMENT.md` for detailed instructions.

---

## 🧪 Testing

### Test Contact Form
```bash
curl -X POST https://your-n8n-instance.com/webhook/anna/lead \
  -H "Content-Type: application/json" \
  -d '{
    "name": "Test User",
    "email": "test@example.com",
    "message": "Testing"
  }'
```

### Verify in Sender.ai
1. Go to Sender.ai dashboard
2. Check Audience → Subscribers
3. Verify new subscriber appears

---

## 📊 Lead Generation Setup

### Sender.ai (Free Tier)
- 2,500 subscribers
- 15,000 emails/month
- Unlimited automation
- Sign up: https://www.sender.net

### n8n (Free Tier)
- 5,000 workflow executions/month
- Unlimited workflows
- Sign up: https://n8n.io

### Total Cost: $0/month

---

## 🎯 Success Metrics

Track these KPIs:
- Daily visitors
- Demo bookings
- Trial signups
- Email open rates
- Conversion rate

---

## 🐛 Troubleshooting

### Build Fails
```bash
rm -rf node_modules pnpm-lock.yaml
pnpm install
pnpm run build
```

### Forms Not Working
1. Check .env file has correct webhook URL
2. Verify n8n workflow is active
3. Test with curl command

### More Help
See `docs/SENDER_N8N_INTEGRATION.md` (Troubleshooting section)

---

## 📞 Support

### Documentation
- Quick Setup: `docs/INTEGRATION_QUICKSTART.md`
- Full Guide: `docs/SENDER_N8N_INTEGRATION.md`
- CEO Guide: `docs/CEO_QUICKSTART.md`

### External Resources
- React: https://react.dev
- Tailwind CSS: https://tailwindcss.com
- shadcn/ui: https://ui.shadcn.com
- Sender.ai: https://www.sender.net
- n8n: https://n8n.io

---

## ✅ Checklist

- [ ] Install dependencies (`pnpm install`)
- [ ] Set up Sender.ai account
- [ ] Set up n8n instance
- [ ] Import n8n workflow
- [ ] Update .env file
- [ ] Update contact information
- [ ] Update Cal.com link
- [ ] Test contact form
- [ ] Build for production
- [ ] Deploy to hosting
- [ ] Test live site

---

## 🎊 Ready to Launch!

Your Anna Corporation landing page is complete with full lead generation capabilities.

**Next Steps:**
1. Follow the 15-minute setup guide (`docs/INTEGRATION_QUICKSTART.md`)
2. Deploy using the deployment guide (`docs/DEPLOYMENT.md`)
3. Start capturing leads!

---

## 📝 License

 2025 Anna Corporation - Halal. Ethical. Automated. Limitless.

---

## 🙏 Acknowledgments

Built with:
- React + TypeScript
- Tailwind CSS + shadcn/ui
- Sender.ai for email marketing
- n8n for workflow automation

---

**Questions?** Check the documentation in the `docs/` folder.

**Ready to launch?** Follow the launch checklist (`docs/LAUNCH_CHECKLIST.md`).

**Need help?** See the CEO quickstart guide (`docs/CEO_QUICKSTART.md`).
