# Move Shop.Warsha to another domain or subdomain

The domain lives in ONE place in the code: the env var `NEXT_PUBLIC_APP_URL`.
Hosting: Cloudflare Workers (project name `shop-warsha`). DNS: Hostinger (warsha.org).

## Steps (about 10 minutes)

1. **Cloudflare** > Workers & Pages > `shop-warsha` > Settings > Domains & Routes
   - Add the new domain (example: `store.warsha.org`).
   - If the domain's DNS is NOT on Cloudflare, Cloudflare shows a CNAME target. Copy it.
2. **Hostinger** > Domains > warsha.org > DNS / Nameservers
   - Delete any old A record with the new name.
   - Add `CNAME` : name = `store` , target = the value from step 1.
3. **Cloudflare** > `shop-warsha` > Settings > Variables and Secrets
   - Change `NEXT_PUBLIC_APP_URL` to `https://store.warsha.org`.
   - Redeploy (Deployments > Retry / or push any commit).
4. **Supabase** > Authentication > URL Configuration
   - Site URL = new domain. Add new domain to Redirect URLs (keep old one until switch is done).
5. Test: home, product, cart, checkout (COD), login, /dashboard.
6. Remove the old domain from Cloudflare + its CNAME in Hostinger.

## Moving to a totally different host
Code is standard Next.js. `npm run build` works on any Node 20+ host (Vercel, Hostinger Business/Cloud, VPS).
Copy the same 4 env vars. Database stays on Supabase, nothing to migrate.

## Env vars
NEXT_PUBLIC_SUPABASE_URL, NEXT_PUBLIC_SUPABASE_ANON_KEY, SUPABASE_SERVICE_ROLE_KEY (secret), NEXT_PUBLIC_APP_URL
