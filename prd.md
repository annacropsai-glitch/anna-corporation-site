# Anna Corporation Cinematic 3D Landing Page Requirements Document

## 1. Project Overview

### 1.1 Project Name
Anna Corporation — Cinematic 3D-style Landing Page with Sender AI Integration\n
### 1.2 Project Description
Build a production-ready, free-hosted landing page with full cinematic immersion experience, including demo flow, analytics, Sender AI lead generation, and n8n integration for Anna Corporation (Anna Corps).

### 1.3 Brand Guidelines
- **Brand Name**: Anna Corporation (Anna Corps)
- **Tagline**: 'Halal. Ethical. Automated. Limitless.'
- **Color Palette**: Sapphire blue (#06204a), Gold (#d4af37), Pure white (#ffffff), Emerald green (#046a38)
- **Typography**: Inter or Poppins, headings 700weight, body regular
- **Tone**: Trustworthy, calm, futuristic, faith-respecting with modest visuals

## 2. Technical Requirements

### 2.1 Platform & Hosting
- **Primary Platform**: GitHub Pages (preferred) or Vercel free plan
- **Repository**: github.com/<username>/anna-corporation-site
- **Technology Stack**: Static HTML/CSS/JS with minimal dependencies
- **Responsive Design**: Desktop (1440px) and Mobile (375px) frames

### 2.2 Free Tools Integration
- Figma Free for design\n- Canva Free for assets
- Google Sheets for data management
- n8n Free Open Source for workflow automation\n- Sender AI for lead generation and email marketing
- Notion for admin dashboard
- Cal.com for demo booking
- Google Looker Studio for analytics

## 3. Design Specifications
\n### 3.1 Hero Section
- Full-screen hero with deep sapphire gradient background
- Central luminous crystalline digital globe (translucent glass with subtle glow)
- Golden Islamic geometric arabesque pattern overlay
- 4translucent light beams connecting to crescent-moon nodes: Finance, Donation, Complaint, Marketing
- Dual CTAs: 'Book AI Demo (Cal.com)' and 'See Live Demo'\n- Trust line: '100% Halal. No riba. No human contact required.'

### 3.2 Features Section
- 3D isometric cards grid (3 per row)
- Card types: AI Receptionist, Auto Booking, Complaint Agent, Social Manager, Halal Finance, Donation Agent
- Each card includes3D-style icon, title, benefit line, and 'See example' CTA
\n### 3.3 Demo Video Block
- Inline video placeholder with play button overlay
- Auto-play muted on click with full-screen modal option
- Caption: 'AI Demo runs live — book a demo to see your agent in action.'
\n### 3.4 Testimonials Section
- Carousel format with 3-5 testimonials
- Placeholder names with modest profile icons
- Halal-focused testimonial content
\n### 3.5 Pricing Section
- Three-column layout: One-time / Monthly / Yearly\n- Each column: price, feature bullets, 'Start7-day free trial' CTA
- Payment note: 'No credit card required; Wise / Bank Transfer options available'

### 3.6 Footer
- Navigation links: About, Services, Pricing, Contact, Privacy Policy
- Admin login link for CEO access
\n## 4. Interactive Elements

### 4.1 Motion & Micro-interactions
- Parallax scroll effects for hero elements
- Hover animations on 3D cards (scale + shadow)
- Subtle pulsating glow on geometric patterns
- IntersectionObserver for scroll-triggered animations

### 4.2 Accessibility Features
- High contrast text compliance
- Alt labels for all images
- Keyboard navigation support
- Screen reader compatibility
\n## 5. Integration Systems

### 5.1 Contact & Demo Booking
- Google Form or Netlify forms for contact submission
- Cal.com embed for demo scheduling
- Form data POST to n8n webhook: /webhook/anna/lead\n- Required fields: name, email, phone (optional), region, business type, message

### 5.2Sender AI Lead Generation Integration
- **Email Campaign Setup**: Automated email sequences for lead nurturing\n- **Lead Scoring**: Integration with Sender AI's lead scoring system
- **Segmentation**: Automatic lead categorization based on business type and region
- **Email Templates**: Halal-compliant email templates for different customer segments
- **A/B Testing**: Email subject line and content optimization
- **Unsubscribe Management**: Automated handling of opt-outs and preferences

### 5.3 N8N Free Open Source Workflow Automation
\n**Workflow1: Lead Intake + Sender AI Integration**
- Webhook trigger for form submissions
- Lead validation and deduplication
- Google Sheets data append\n- Sender AI contact creation via API
- Lead segmentation and tagging in Sender AI
- Auto-response email via Sender AI
- Admin notification (Telegram/Email)
\n**Workflow 2: Demo Booking → Trial Activation**
- Cal.com webhook integration
- Trial period setup (7 days)
- User creation in CRM
- Demo agent trigger
- Sender AI trial sequence activation
\n**Workflow 3: Trial Management + Email Automation**
- Daily scheduler for trial monitoring
- Sender AI automated email sequences for trial users
- Payment reminder emails via Sender AI
- Status updates based on payment\n- Trial completion follow-up campaigns

**Workflow 4: Lead Nurturing Campaigns**
- Sender AI campaign triggers based on user behavior
- Automated email sequences for different lead stages
- Re-engagement campaigns for inactive leads
- Conversion tracking and analytics sync
\n**Workflow 5: System Monitoring**
- Error logging and health checks
- Alert notifications for failures
- Sender AI delivery status monitoring
\n### 5.4 Data Management\n\n**Google Sheets'Dashboard Brain' Structure:**
- Tabs: Leads, Clients, Trials, Payments, Donations, AgentLogs, Errors, Metrics, SenderAI_Campaigns
- Lead columns: LeadID, CreatedAt, Name, Email, Phone, Source, Niche, Status, TrialStart, TrialEnd, LastContacted, Notes, SenderAI_ContactID, EmailStatus, CampaignTags
- Conditional formatting for trial status tracking
- Sender AI campaign performance tracking

## 6. Admin & Analytics
\n### 6.1 Notion Admin Hub
- 'Anna Corporation HQ' main page
- Subpages: Overview, Agents List, Supervision Checklist, Billing, Support, Email Campaigns
- Embedded Google Sheets and Looker Studio dashboard
- Sender AI campaign management interface

### 6.2 Analytics Dashboard
- Google Looker Studio integration
- Key metrics: Daily Leads, Trial Activations, Conversion Rate, MRR, Active Trials, Weekly Errors, Email Open Rates, Click-through Rates
- Sender AI campaign performance metrics
- View-only access for stakeholders

## 7. Content & Media Assets
\n### 7.1 Required Exports from Figma\n- hero_globe_layer.png (2x resolution)
- beams_overlay.png (transparent)\n- node_icons.svg (4 icons pack)
- feature_card_svgs.svg\n- CSS animation snippets
\n### 7.2 Demo Video\n- 10-20 second silent demo clip
- Created using Canva/CapCut free elements
- Hosted in GitHub repo or Google Drive
- Shows AI agent flow: globe → node → demo\n
### 7.3 Email Templates
- Welcome email template for new leads
- Trial activation email sequence
- Payment reminder templates
- Re-engagement campaign templates
- All templates following halal compliance guidelines

## 8. Compliance & Legal

### 8.1 Halal Compliance
- No riba-based financial products
- No non-mahram interaction imagery
- Modest visual representation
- Clear halal certification statement
\n### 8.2 Privacy & Legal
- Auto-generated Privacy Policy and Terms\n- Explicit consent checkboxes on all forms
- Data handling transparency statement
- GDPR-compliant data collection\n- Email marketing consent and unsubscribe options

## 9. SEO & Performance
\n### 9.1 SEO Optimization
- Meta title and description tags
- Open Graph image integration
- Structured data markup
- Semantic HTML structure\n\n### 9.2 Performance Requirements\n- WebP image format optimization
- Minimal JavaScript dependencies
- Lightweight CSS framework
- Fast loading on mobile networks
\n## 10. Quality Assurance

### 10.1 Testing Requirements
- Cross-browser compatibility testing
- Mobile responsiveness verification
- Form submission functionality\n- n8n workflow validation
- Google Sheets data flow confirmation
- Sender AI integration testing
- Email delivery and tracking verification

### 10.2 Documentation
- Repository README with adjustment instructions\n- CEO Quickstart guide in Notion
- 10-minute daily management checklist
- Troubleshooting guide for common issues
- Sender AI setup and configuration guide
\n## 11. Deliverables\n
1. Figma file with view/edit access
2. GitHub repository URL with deployed site
3. n8n workflow JSON export with webhook endpoints
4. Google Sheets Dashboard Brain template
5. Notion admin page with owner invitation
6. Looker Studio dashboard link
7. Demo video file URL
8. Sender AI account setup and configuration
9. Email template library for Sender AI
10. Complete documentation package (README + CEO Quickstart + Sender AI Guide)

## 12. Design Style

- **Visual Theme**: Cinematic 3D with Islamic geometric influences
- **Color Harmony**: Deep sapphire backgrounds with gold accents and emerald highlights
- **Typography Scale**: Clean hierarchy with 700-weight headings and regular body text
- **3D Elements**: Isometric cards with subtle drop shadows and soft reflections
- **Animation Style**: Smooth parallax scrolling with gentle hover transitions
- **Layout Approach**: Grid-based with generous white space and clear visual separation
- **Interactive Feedback**: Subtle scale transforms and glow effects on user interaction