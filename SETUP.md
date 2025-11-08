# Anna Corporation Landing Page - Setup Guide

## Overview
This is a production-ready, cinematic 3D landing page for Anna Corporation, featuring halal-compliant AI business automation services.

## Features
- ✨ Cinematic 3D design with Islamic geometric influences
- 🎨 Brand colors: Sapphire Blue, Gold, Emerald Green
- 📱 Fully responsive (desktop and mobile)
- ⚡ Smooth animations and parallax effects
- 🎯 6 AI service features with 3D cards
- 💰 Pricing section with 3 plans
- 💬 Testimonials carousel
- 🎥 Demo video section
- 📧 Contact forms ready for integration

## Technology Stack
- React 18 with TypeScript
- Tailwind CSS for styling
- shadcn/ui components
- Lucide React icons
- Vite for build tooling

## Quick Start

### Installation
```bash
pnpm install
```

### Development
```bash
pnpm run dev
```

### Build
```bash
pnpm run build
```

### Lint
```bash
pnpm run lint
```

## Integration Points

### 1. Cal.com Demo Booking
Update the Cal.com link in `src/components/landing/Hero.tsx`:
```typescript
onClick={() => window.open('YOUR_CAL_COM_LINK', '_blank')}
```

### 2. Contact Forms
The footer includes a newsletter subscription form. To integrate:
1. Add form submission handler
2. Connect to your email service (e.g., Mailchimp, SendGrid)
3. Or POST to n8n webhook

### 3. N8N Webhook Integration
Example webhook integration for lead capture:
```typescript
const handleSubmit = async (data) => {
  await fetch('YOUR_N8N_WEBHOOK_URL', {
    method: 'POST',
    headers: { 'Content-Type': 'application/json' },
    body: JSON.stringify(data)
  });
};
```

### 4. Demo Video
Replace the video placeholder in `src/components/landing/DemoVideo.tsx`:
- Add YouTube/Vimeo embed
- Or use self-hosted video with HTML5 video player

## Customization

### Brand Colors
Edit `src/index.css` to change brand colors:
```css
--sapphire: 215 88% 16%;
--gold: 45 69% 53%;
--emerald: 152 94% 21%;
```

### Content Updates
- **Hero**: `src/components/landing/Hero.tsx`
- **Features**: `src/components/landing/Features.tsx`
- **Testimonials**: `src/components/landing/Testimonials.tsx`
- **Pricing**: `src/components/landing/Pricing.tsx`
- **Footer**: `src/components/landing/Footer.tsx`

### Images
Replace images by updating URLs in components:
- Hero background: Line 21 in `Hero.tsx`

## Deployment

### GitHub Pages
1. Build the project: `pnpm run build`
2. Deploy the `dist` folder to GitHub Pages
3. Configure custom domain if needed

### Vercel
1. Connect your GitHub repository
2. Vercel will auto-detect Vite configuration
3. Deploy with one click

### Netlify
1. Connect your GitHub repository
2. Build command: `pnpm run build`
3. Publish directory: `dist`

## SEO Optimization
The landing page includes:
- Meta tags in `index.html`
- Semantic HTML structure
- Proper heading hierarchy
- Alt text for images (add as needed)

## Performance
- Optimized images (use WebP format)
- Lazy loading for images
- Minimal JavaScript bundle
- CSS animations using GPU acceleration

## Halal Compliance
The design follows halal business principles:
- ✓ No riba-based financial products
- ✓ Modest visual representation
- ✓ No inappropriate imagery
- ✓ Clear halal certification statements

## Support
For questions or issues, contact the development team or refer to the main README.md file.

## License
© 2025 Anna Corporation
