# Anna Corporation - Quick Reference Card

## 🚀 Essential Commands

```bash
# Development
pnpm install          # Install dependencies
pnpm run dev          # Start dev server
pnpm run build        # Build for production
pnpm run lint         # Check code quality

# Deployment
git add .             # Stage changes
git commit -m "msg"   # Commit changes
git push              # Push to GitHub
```

## 📁 Key Files to Edit

| File | Purpose | What to Change |
|------|---------|----------------|
| `src/components/landing/Hero.tsx` | Hero section | Cal.com link, main text |
| `src/components/landing/Features.tsx` | Services | Feature descriptions |
| `src/components/landing/Testimonials.tsx` | Reviews | Customer testimonials |
| `src/components/landing/Pricing.tsx` | Pricing | Prices, features |
| `src/components/landing/Footer.tsx` | Footer | Contact info, links |
| `src/index.css` | Design | Colors, animations |
| `index.html` | Meta tags | Title, description |

## 🎨 Brand Colors (HSL)

```css
--sapphire: 215 88% 16%    /* #06204a - Main blue */
--gold: 45 69% 53%         /* #d4af37 - Accent gold */
--emerald: 152 94% 21%     /* #046a38 - Success green */
--background: 0 0% 100%    /* #ffffff - White */
```

## 🔗 Integration URLs

### Update These Links
- **Cal.com**: Line 71 in `Hero.tsx`
- **n8n Webhook**: Add to form handlers
- **Email**: Line 82 in `Footer.tsx`
- **Phone**: Line 89 in `Footer.tsx`

## 📊 Analytics Setup

### Google Analytics
```html
<!-- Add to index.html before </head> -->
<script async src="https://www.googletagmanager.com/gtag/js?id=GA_ID"></script>
<script>
  window.dataLayer = window.dataLayer || [];
  function gtag(){dataLayer.push(arguments);}
  gtag('js', new Date());
  gtag('config', 'GA_ID');
</script>
```

## 🐛 Common Issues & Fixes

### Issue: Build fails
```bash
# Solution
rm -rf node_modules pnpm-lock.yaml
pnpm install
pnpm run build
```

### Issue: Images not loading
```javascript
// Check image URL format
<img src="https://full-url-here.jpg" alt="description" />
```

### Issue: Styles not applying
```bash
# Clear cache and rebuild
pnpm run build
# Clear browser cache (Ctrl+Shift+R)
```

## 📱 Test URLs

### Local Development
```
http://localhost:5173
```

### Production (Update after deployment)
```
GitHub Pages: https://username.github.io/repo
Vercel: https://project.vercel.app
Netlify: https://project.netlify.app
```

## 🔧 Quick Customizations

### Change Hero Text
```typescript
// src/components/landing/Hero.tsx (line 54-56)
<h1 className="...">
  Your Company Name
</h1>
```

### Update Pricing
```typescript
// src/components/landing/Pricing.tsx (line 6)
const pricingPlans = [
  {
    name: "Plan Name",
    price: "$999",
    // ... rest of config
  }
];
```

### Add Testimonial
```typescript
// src/components/landing/Testimonials.tsx (line 6)
{
  name: "Customer Name",
  role: "Their Role",
  company: "Company Name",
  content: "Their review",
  rating: 5,
  avatar: "👨‍💼",
}
```

## 📞 Emergency Contacts

```
Technical Support: [Add contact]
Hosting Provider: [Add contact]
Domain Registrar: [Add contact]
CEO/Admin: [Add contact]
```

## 🎯 Daily Checklist

- [ ] Check website is live
- [ ] Review analytics
- [ ] Check demo bookings
- [ ] Respond to inquiries
- [ ] Monitor performance

## 📚 Documentation Links

- **Setup Guide**: `docs/SETUP.md`
- **CEO Guide**: `docs/CEO_QUICKSTART.md`
- **Deployment**: `docs/DEPLOYMENT.md`
- **Workflows**: `docs/N8N_WORKFLOWS.md`
- **Launch Checklist**: `docs/LAUNCH_CHECKLIST.md`

## 🆘 Quick Troubleshooting

| Problem | Solution |
|---------|----------|
| Site down | Check hosting status, DNS |
| Slow loading | Optimize images, check CDN |
| Forms not working | Verify webhook URLs |
| Broken links | Test all links, update URLs |
| Mobile issues | Test responsive design |

## 💡 Pro Tips

1. **Always backup** before making changes
2. **Test locally** before deploying
3. **Use staging** for major updates
4. **Monitor analytics** daily
5. **Respond quickly** to inquiries
6. **Keep content fresh** weekly
7. **Update testimonials** monthly
8. **Review security** quarterly

## 🔐 Security Reminders

- ✅ Never commit API keys
- ✅ Use environment variables
- ✅ Enable HTTPS
- ✅ Update dependencies monthly
- ✅ Monitor for vulnerabilities

## 📈 Success Metrics

### Track These
- Daily visitors
- Demo bookings
- Trial signups
- Conversion rate
- Customer satisfaction

### Goals (Month 1)
- 2,000+ visitors
- 100+ demos
- 50+ trials
- 20+ customers

## 🎉 Quick Wins

### Easy Improvements
1. Add more testimonials
2. Update pricing
3. Add blog posts
4. Improve SEO
5. A/B test CTAs
6. Add social proof
7. Optimize images
8. Speed up loading

## 📝 Notes Space

```
Quick Notes:
_________________________________________________
_________________________________________________
_________________________________________________
_________________________________________________
_________________________________________________
```

---

**Keep this card handy for quick reference!**

© 2025 Anna Corporation
