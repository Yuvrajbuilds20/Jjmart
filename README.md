# 🛒 JJ Mart — Groceries & Daily Essentials, Delivered

A polished, single-page grocery delivery storefront built entirely in vanilla
JavaScript with a [Supabase](https://supabase.com) backend. Designed as a
realistic demo of a neighborhood superstore going online — fast, colorful,
and fully functional, with no framework and no build step.

## Features

- 🏬 **Storefront** — home page, category browsing, product search, and
  product detail pages with variants and stock status
- 🛒 **Cart** — supports both guest carts (persisted in `localStorage`) and
  logged-in carts, with automatic merge on login
- 💳 **Checkout** — Cash on Delivery and online payment flows, with pincode-
  based delivery area restrictions
- 📦 **Orders** — order history and status tracking per user
- 👤 **Accounts** — Supabase Auth-based login/signup and profile management
- 🛠️ **Admin dashboard** — manage products, categories, and orders (access
  gated by Supabase Row Level Security, not just client-side checks)
- 📱 **Responsive UI** — mobile tab bar, floating cart, and adaptive layouts
  for small screens
- 🎨 **Custom design system** — Nunito / Plus Jakarta Sans / JetBrains Mono
  typography, an animated marquee banner, and a fresh green/teal grocery
  color palette

## Tech Stack

- **Vanilla JavaScript** — custom client-side router and DOM renderer, no
  framework
- **[Supabase](https://supabase.com)** — Postgres database, Auth, and Row
  Level Security for access control
- **Plain CSS** — CSS custom properties for theming, no preprocessor or
  build step
- **Cloudinary** — direct unsigned image uploads (admin product images)

## Getting Started

This is a static, single-HTML-file app — no build tooling required.

1. Clone the repo
2. Open `jjmart-5-3.html` directly in a browser, or serve it with any static
   file server
3. Connect it to your own Supabase project by updating `SUPABASE_URL` and
   `SUPABASE_ANON_KEY` near the top of the `<script>` block

### 🔒 Security notes

The file has a live Supabase project URL and anon key hardcoded in it.
This is safe to expose because Row Level Security (RLS) is enabled and
reviewed on every table (`products`, `categories`, `orders`, `order_items`,
`profiles`, `cart_items`, `addresses`, `reviews`, `site_settings`) — the
anon key alone cannot bypass these policies.

As part of that review, a privilege-escalation gap in the `profiles` update
policy was found and fixed: the original policy only checked *who* could
update a row, not *what* they could change, which meant any logged-in user
could set `is_admin = true` on their own profile. The policy now includes a
`WITH CHECK` clause that locks the `is_admin` column to its existing value
unless the caller is already an admin.

If you fork this project or reuse it with your own Supabase backend:

- Re-run the same review — don't assume policies carry over safely
- Never commit a `service_role` key — only the `anon` key belongs in
  client-side code
- Consider swapping in a fresh demo/sandbox Supabase project if this key
  is tied to real data

## Project Structure

This project is currently a single self-contained HTML file
(`jjmart-5-3.html`) containing all markup, styles, and application logic.

## Status

This is a demo/portfolio project and is not a real, operating store.

## License

Add a license of your choice (e.g. MIT) if you intend for others to reuse
this code.
