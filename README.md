# OrangeCore Group — Website

Astro static site for orangecoregroup.com.
Built with Astro + Vercel + GoDaddy DNS.

## Stack

- Framework: Astro (static output)
- Hosting: Vercel
- Domain: GoDaddy (DNS only — points to Vercel)
- Version Control: GitHub

## Local Development

  npm install        # Install dependencies
  npm run dev        # Start dev server → http://localhost:4321
  npm run build      # Build for production
  npm run preview    # Preview production build locally

## Deploy to Vercel

### First deploy (one-time)

1. Push this repo to GitHub
2. Go to vercel.com and sign in
3. Click Add New → Project
4. Import the GitHub repo
5. Vercel auto-detects Astro. No framework settings needed.
6. Click Deploy

Vercel gives you a .vercel.app URL on first deploy. Test it before pointing DNS.

Every push to main triggers an automatic redeploy.

## Point GoDaddy DNS to Vercel

Do this AFTER the first successful Vercel deploy.

Step 1 — Add your custom domain in Vercel
- Vercel dashboard → your project → Settings → Domains
- Add orangecoregroup.com and www.orangecoregroup.com
- Vercel shows you the DNS records you need

Step 2 — Update GoDaddy DNS records
- Log into GoDaddy → My Products → DNS → orangecoregroup.com

  Type    Name   Value                    TTL
  A       @      76.76.21.21              600
  CNAME   www    cname.vercel-dns.com.    600

- Delete any existing A records pointing to the old WordPress host.
- Note: Verify Vercel's A record IP in your Vercel domain settings — they occasionally update it.
- DNS propagation: 15 min to a few hours. Check at dnschecker.org.

Step 3 — Verify in Vercel
Once DNS propagates, Vercel auto-provisions SSL. Site goes live at https://orangecoregroup.com.

## Sitemap

@astrojs/sitemap generates /sitemap-index.xml automatically on build.

After the site is live:
1. Go to search.google.com/search-console
2. Add and verify orangecoregroup.com
3. Submit: https://orangecoregroup.com/sitemap-index.xml

## Calendly Integration (Contact Page)

The contact page has a placeholder for Calendly.
To add it:
1. Get your Calendly embed code from calendly.com → Sharing → Embed
2. Open src/pages/contact/index.astro
3. Replace the .calendly-mock div with the Calendly inline embed script

## Folder Structure

  orangecore/
  ├── public/
  │   ├── favicon.svg
  │   └── robots.txt
  ├── src/
  │   ├── components/
  │   │   ├── Nav.astro
  │   │   └── Footer.astro
  │   ├── layouts/
  │   │   └── Base.astro
  │   ├── pages/
  │   │   ├── index.astro                          -> /
  │   │   ├── 404.astro
  │   │   ├── services/index.astro                 -> /services/
  │   │   ├── hubspot-revops-consultant/index.astro -> /hubspot-revops-consultant/
  │   │   ├── fractional-cro/index.astro           -> /fractional-cro/
  │   │   ├── about/index.astro                    -> /about/
  │   │   └── contact/index.astro                  -> /contact/
  │   └── styles/
  │       └── global.css
  ├── astro.config.mjs
  ├── package.json
  └── README.md

## Content Updates

All page content lives in src/pages/. Each .astro file is a page.
Nav and footer are in src/components/ — update once, reflects everywhere.

When you add a blog (/blog/) later: create src/pages/blog/ and Astro routes it automatically.
Run npm run build to verify the sitemap updates.
