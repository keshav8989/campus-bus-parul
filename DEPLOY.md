# Deploy free on Vercel (no timeouts)

1. Push this folder to GitHub, then vercel.com → Add New → Project → import it (Vite is auto-detected).
2. **Shared live data (needed so the driver's phone and students' phones see the same bus):**
   Project → Storage → Marketplace → **Upstash Redis** (free plan) → connect. Vercel adds the env vars automatically. Redeploy.
3. **Google Maps (optional, free tier):** Google Cloud → enable *Maps JavaScript API* → create a key, restrict it to your Vercel domain →
   Vercel → Settings → Environment Variables → `VITE_GOOGLE_MAPS_API_KEY`. Redeploy.
   Without a key the app uses the keyless Google embed map, which still works.
4. Driver GPS only works over HTTPS (Vercel provides it) and after the driver taps “Share my live location”.

Why it won't time out: the API is one short function (<1s), polling replaces long connections, and GET /api/state is CDN-cached for 3s to stay inside free Redis limits.

Local: `npm install && npm run dev` (Python backend auto-starts).
