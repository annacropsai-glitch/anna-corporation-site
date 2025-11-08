# Deployment Guide - Anna Corporation Landing Page

## Overview
This guide covers deployment options for the Anna Corporation landing page to free hosting platforms.

## Deployment Options

### Option 1: GitHub Pages (Recommended)

#### Prerequisites
- GitHub account
- Git installed locally

#### Steps

1. **Create GitHub Repository**
```bash
# Initialize git (if not already done)
git init

# Add all files
git add .

# Commit
git commit -m "Initial commit: Anna Corporation landing page"

# Create repository on GitHub
# Then add remote
git remote add origin https://github.com/YOUR_USERNAME/anna-corporation-site.git

# Push to GitHub
git push -u origin main
```

2. **Configure GitHub Pages**
- Go to repository Settings
- Navigate to Pages section
- Source: Deploy from a branch
- Branch: Select `main` and `/root` or `/docs`
- Click Save

3. **Build and Deploy**
```bash
# Build the project
pnpm run build

# The dist folder contains your production files
# You can use gh-pages package for automatic deployment
pnpm add -D gh-pages

# Add to package.json scripts:
# "deploy": "pnpm run build && gh-pages -d dist"

# Deploy
pnpm run deploy
```

4. **Custom Domain (Optional)**
- Add CNAME file to public folder with your domain
- Configure DNS settings:
  - Type: CNAME
  - Name: www
  - Value: YOUR_USERNAME.github.io
- Enable HTTPS in GitHub Pages settings

#### GitHub Pages URL
```
https://YOUR_USERNAME.github.io/anna-corporation-site
```

---

### Option 2: Vercel (Easiest)

#### Prerequisites
- Vercel account (free)
- GitHub repository

#### Steps

1. **Connect Repository**
- Go to https://vercel.com
- Click "New Project"
- Import your GitHub repository
- Vercel auto-detects Vite configuration

2. **Configure Build Settings**
- Framework Preset: Vite
- Build Command: `pnpm run build`
- Output Directory: `dist`
- Install Command: `pnpm install`

3. **Deploy**
- Click "Deploy"
- Vercel builds and deploys automatically
- Get your live URL: `https://your-project.vercel.app`

4. **Custom Domain**
- Go to Project Settings → Domains
- Add your custom domain
- Configure DNS as instructed
- SSL certificate auto-generated

#### Automatic Deployments
- Every push to main branch auto-deploys
- Preview deployments for pull requests
- Rollback to previous versions anytime

---

### Option 3: Netlify

#### Prerequisites
- Netlify account (free)
- GitHub repository

#### Steps

1. **Connect Repository**
- Go to https://netlify.com
- Click "Add new site" → "Import an existing project"
- Connect to GitHub
- Select your repository

2. **Configure Build Settings**
- Build command: `pnpm run build`
- Publish directory: `dist`
- Node version: 18 or higher

3. **Deploy**
- Click "Deploy site"
- Netlify builds and deploys
- Get your URL: `https://random-name.netlify.app`

4. **Custom Domain**
- Go to Site settings → Domain management
- Add custom domain
- Configure DNS
- SSL auto-enabled

#### Features
- Form handling (useful for contact forms)
- Serverless functions
- Split testing
- Analytics

---

### Option 4: Cloudflare Pages

#### Prerequisites
- Cloudflare account (free)
- GitHub repository

#### Steps

1. **Create Pages Project**
- Go to Cloudflare Dashboard
- Navigate to Pages
- Click "Create a project"
- Connect to GitHub

2. **Configure Build**
- Framework preset: Vite
- Build command: `pnpm run build`
- Build output directory: `dist`

3. **Deploy**
- Click "Save and Deploy"
- Get URL: `https://your-project.pages.dev`

4. **Custom Domain**
- Add custom domain in Pages settings
- Configure DNS (automatic if using Cloudflare DNS)
- SSL auto-enabled

---

## Pre-Deployment Checklist

### ✅ Content Review
- [ ] All text is correct and professional
- [ ] Contact information is accurate
- [ ] Links work correctly
- [ ] Images load properly
- [ ] No placeholder text remains

### ✅ Functionality
- [ ] All buttons work
- [ ] Forms are connected (or ready for integration)
- [ ] Navigation works smoothly
- [ ] Responsive on mobile and desktop
- [ ] Animations work properly

### ✅ SEO & Performance
- [ ] Meta tags are set
- [ ] Page title is correct
- [ ] Images are optimized
- [ ] No console errors
- [ ] Fast loading time

### ✅ Integrations
- [ ] Cal.com link is updated
- [ ] n8n webhooks are ready
- [ ] Analytics tracking is set up
- [ ] Email service is configured

---

## Post-Deployment Steps

### 1. Test Live Site
- Visit your live URL
- Test on different devices
- Check all links and buttons
- Verify forms work
- Test demo booking

### 2. Set Up Analytics
```html
<!-- Add to index.html before </head> -->
<!-- Google Analytics -->
<script async src="https://www.googletagmanager.com/gtag/js?id=GA_MEASUREMENT_ID"></script>
<script>
  window.dataLayer = window.dataLayer || [];
  function gtag(){dataLayer.push(arguments);}
  gtag('js', new Date());
  gtag('config', 'GA_MEASUREMENT_ID');
</script>
```

### 3. Configure DNS (Custom Domain)
```
Type: A
Name: @
Value: [Your hosting provider's IP]

Type: CNAME
Name: www
Value: [Your hosting provider's domain]
```

### 4. Enable SSL/HTTPS
- Most platforms auto-enable SSL
- Verify HTTPS works
- Redirect HTTP to HTTPS

### 5. Set Up Monitoring
- Use UptimeRobot (free) for uptime monitoring
- Set up alerts for downtime
- Monitor performance with PageSpeed Insights

---

## Environment Variables

If you need environment variables (for API keys, etc.):

### Vercel
```bash
# In Vercel Dashboard → Settings → Environment Variables
VITE_API_KEY=your_api_key
VITE_N8N_WEBHOOK=your_webhook_url
```

### Netlify
```bash
# In Netlify Dashboard → Site settings → Environment variables
VITE_API_KEY=your_api_key
VITE_N8N_WEBHOOK=your_webhook_url
```

### GitHub Pages
- Create `.env.production` file
- Add to `.gitignore`
- Use build-time variables only

---

## Continuous Deployment

### Automatic Deployments
All platforms support automatic deployment:
1. Push to GitHub
2. Platform detects changes
3. Builds automatically
4. Deploys to production

### Branch Deployments
- `main` branch → Production
- `develop` branch → Staging
- Pull requests → Preview deployments

---

## Rollback Procedure

### Vercel
1. Go to Deployments
2. Find previous working deployment
3. Click "..." → "Promote to Production"

### Netlify
1. Go to Deploys
2. Find previous deployment
3. Click "Publish deploy"

### GitHub Pages
1. Revert commit in Git
2. Push to main branch
3. Redeploy

---

## Performance Optimization

### Before Deployment
```bash
# Optimize images
# Use WebP format
# Compress assets

# Analyze bundle size
pnpm run build
# Check dist folder size
```

### After Deployment
- Use Cloudflare CDN (free)
- Enable caching
- Compress assets (Gzip/Brotli)
- Lazy load images

---

## Troubleshooting

### Build Fails
- Check Node version (18+)
- Verify all dependencies installed
- Review build logs
- Test build locally first

### Site Not Loading
- Check DNS settings
- Verify deployment succeeded
- Clear browser cache
- Check hosting status

### Images Not Showing
- Verify image URLs are absolute
- Check CORS settings
- Ensure images are in public folder
- Test image URLs directly

### Forms Not Working
- Verify webhook URLs
- Check CORS settings
- Test with browser console
- Review network requests

---

## Security Best Practices

1. **HTTPS Only**
   - Force HTTPS redirect
   - Use HSTS headers

2. **Content Security Policy**
```html
<meta http-equiv="Content-Security-Policy" 
      content="default-src 'self'; script-src 'self' 'unsafe-inline';">
```

3. **Hide Sensitive Data**
   - Never commit API keys
   - Use environment variables
   - Add `.env` to `.gitignore`

4. **Regular Updates**
   - Update dependencies monthly
   - Monitor security advisories
   - Test after updates

---

## Monitoring & Maintenance

### Weekly Tasks
- [ ] Check uptime status
- [ ] Review analytics
- [ ] Test critical features
- [ ] Check for broken links

### Monthly Tasks
- [ ] Update dependencies
- [ ] Review performance metrics
- [ ] Backup data
- [ ] Test disaster recovery

### Quarterly Tasks
- [ ] Security audit
- [ ] Performance optimization
- [ ] Content refresh
- [ ] SEO review

---

## Support Resources

### Hosting Platforms
- GitHub Pages: https://pages.github.com
- Vercel: https://vercel.com/docs
- Netlify: https://docs.netlify.com
- Cloudflare Pages: https://developers.cloudflare.com/pages

### Tools
- PageSpeed Insights: https://pagespeed.web.dev
- UptimeRobot: https://uptimerobot.com
- Google Analytics: https://analytics.google.com

---

## Cost Breakdown (Free Tier Limits)

### GitHub Pages
- **Cost**: Free
- **Bandwidth**: 100GB/month
- **Build time**: Unlimited
- **Custom domain**: Yes
- **SSL**: Free

### Vercel
- **Cost**: Free
- **Bandwidth**: 100GB/month
- **Builds**: 6000 minutes/month
- **Custom domain**: Yes
- **SSL**: Free

### Netlify
- **Cost**: Free
- **Bandwidth**: 100GB/month
- **Build minutes**: 300/month
- **Custom domain**: Yes
- **SSL**: Free

---

## Recommended Setup

For Anna Corporation, we recommend:

1. **Primary**: Vercel (easiest, best DX)
2. **Backup**: GitHub Pages (always available)
3. **CDN**: Cloudflare (free, fast)
4. **Monitoring**: UptimeRobot (free alerts)
5. **Analytics**: Google Analytics (free, comprehensive)

---

© 2025 Anna Corporation
