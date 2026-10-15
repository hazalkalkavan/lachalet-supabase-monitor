# La Chalet d'Hazal — Supabase health monitor

This GitHub Actions workflow checks a configured HTTPS endpoint daily at 08:17 UTC, and can be run manually.

## Required configuration
In this repository go to **Settings → Secrets and variables → Actions → New repository secret** and create `SUPABASE_HEALTH_URL`.

Its value must be an HTTPS URL for a **read-only endpoint that actually checks the Supabase database** and responds with HTTP 2xx when healthy, non-2xx when unavailable. Do not use the public homepage alone: it may return 200 even when Supabase is paused.

Do not put service-role keys, database passwords, or access tokens into URLs. The endpoint should be safe for automated requests, with appropriate rate limits.

Then open **Actions → Supabase daily health check → Run workflow** to verify. GitHub Actions may need to be enabled.

**Important:** Periodic requests do not guarantee that Supabase Free projects avoid inactivity pausing. This workflow provides a daily check, not guaranteed keep-alive or proactive alerts. For guaranteed no inactivity pause, use an eligible paid Supabase plan.
