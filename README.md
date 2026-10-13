# Shopnix — Cloudflare Pages/Workers + D1

A responsive storefront starter with customer registration/login, cart, checkout/order creation, admin dashboard, product CRUD, order status management, and editable WhatsApp/Telegram contact details.

## Before deployment
1. Create a Cloudflare D1 database named `shopnix-db` and paste its database ID into `wrangler.toml`.
2. Set Worker secret `SESSION_SECRET` to a long random value (32+ characters) in Cloudflare Dashboard → Workers & Pages → shopnix-api → Settings → Variables and Secrets.
3. Apply the SQL migration: `npx wrangler d1 migrations apply shopnix-db --remote`.
4. Deploy from the project root with Wrangler or connect this repository to Cloudflare Workers Builds.
5. **Create the admin account:** register through the storefront first. Then in D1 Console run: `UPDATE users SET role='admin' WHERE email='your-email@example.com';` Replace with your registered email. Sign in again to access Admin.
6. In Admin → Settings enter your WhatsApp number (country code, digits) and Telegram username. No contact number is hard-coded.

## Local preview
`npx wrangler dev`

## Important
- Password storage uses SHA-256 as a lightweight starter; for a public production shop, upgrade to a dedicated password KDF (Argon2id/scrypt/PBKDF2 with appropriate parameters), add rate limits, CSRF protections where applicable, audit logs, email verification, and backups before accepting real customer data.
- UPI is shown as an order preference only; this starter does not process payments. Do not claim an order is paid until you verify payment.
- Product images can be upgraded to uploaded image URLs; current demo products use emoji artwork.
