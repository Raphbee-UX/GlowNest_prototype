# GlowNest Skincare

A responsive premium skincare storefront built with the Next.js App Router, TypeScript, Tailwind CSS and custom responsive styling.

## Pages
- / — editorial homepage, collection, brand story and routine storytelling
- /shop — three-product collection
- /products/[slug] — dynamic product detail pages
- /contact — general enquiry form
- POST /api/leads — validated server-side n8n webhook proxy

## Local development
```bash
npm install
cp .env.example .env.local
npm run dev
```
The storefront can be explored without n8n configured. Enquiry submissions deliberately return a configuration error until N8N_WEBHOOK_URL is set.

## Enquiry integration
Set N8N_WEBHOOK_URL in .env.local for local development and in Vercel Project Settings → Environment Variables for deployment. Keep it server-side; do not use a NEXT_PUBLIC_ prefix. The API validates required fields and explicit contact consent, then sends a JSON POST containing event, submittedAt, source, lead contact/product/message details, budget, timeline and consent flags. The browser never receives the webhook URL. A success response is returned only when n8n responds with a 2xx status. Missing configuration, invalid input, timeout and upstream failures return real errors.

## Deployment
Import the repository into Vercel, select the Next.js preset and root directory. Set NEXT_PUBLIC_SITE_URL to the canonical deployed site origin for metadata and sitemap URLs, and configure N8N_WEBHOOK_URL as a server-only environment variable for the desired environments. Deploy and test the live enquiry flow. No checkout or Shopify functionality is simulated. Product data is isolated in lib/products.ts for a future commerce integration.

See ASSET-MANIFEST.md for the organized asset paths and intended uses.