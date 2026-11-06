# GlowNest Skincare

A responsive Next.js App Router storefront concept for a modern, understated skincare brand. Built to demonstrate a polished frontend and a server-side lead handoff to n8n.

## Run locally

```bash
npm install
cp .env.example .env.local
npm run dev
```

Open http://localhost:3000.

## Enquiry delivery

The browser posts to `POST /api/leads`. The route validates and normalizes the submission, adds an ISO timestamp and source path, then forwards the payload to the server-only `N8N_WEBHOOK_URL`.

Set `N8N_WEBHOOK_URL` in your local `.env.local` and in the hosting provider's server environment variables. Do not prefix it with `NEXT_PUBLIC_`, commit it, or expose it to the browser.

Expected webhook JSON:

- `name`, `email`, `phone`
- `product`, `message`, `budget`, `timeline`
- `marketingConsent` (boolean)
- `enquiryType` (`general` or `product`)
- `source` (page path)
- `submittedAt` (ISO 8601 timestamp)

The API returns a clear configuration error when the webhook is missing, and an upstream error when n8n cannot accept the request. It never reports a false success.

## Pages

- `/` — editorial homepage, collection, story and routine sections
- `/shop` — product listing
- `/products/[slug]` — product detail and product-specific enquiry
- `/contact` — general enquiry form
- `/api/leads` — validated server-side webhook proxy

## Product and asset structure

Product content is centralized in `lib/products.ts`. Uploaded images are preserved at the repository root and copied into `public/` with their exact original filenames for Next.js static serving. Update product imagery by replacing the matching files in `public/`.

## Important

This is a demonstration storefront, not a live commerce checkout. Product descriptions and prices are illustrative. No payment or medical claims are implemented.
