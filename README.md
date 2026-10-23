# MovieAPI Railway Relay

This is the MovieAPI-owned authenticated MovieBox relay. It contains no API-key database, quota data, admin UI, or secret values. Cloudflare remains responsible for the public API and key limits.

## Deploy

Railway's dashboard deploys from a connected GitHub repository; it does not directly deploy a ZIP file. Extract this ZIP and place its contents at the root of a GitHub repository, then in Railway choose **New Project → Deploy from GitHub Repo** and select that repository. Set the service root directory to `/` if Railway asks.

The included `railway.toml` sets the start command (`node relay-server.js`) and health check (`/health`). The Node runtime must be 24 or newer.

## Required Railway variable

Set `RELAY_SECRET` in the Railway service's Variables panel to the same secret already configured on the Cloudflare Worker. Do not put it in this repository, ZIP, or source file. Railway supplies `PORT` automatically.

Optional: set `MOVIEBOX_PROXY_URL` only if you have a valid, stable HTTP(S) CONNECT proxy URL. Without it, the relay uses Railway's network egress.

## After deployment

1. Open `https://<your-railway-domain>/health`; expect JSON with `service: "movieapi-origin"`.
2. Send me the service's HTTPS domain. I can then configure `ENGINE_RELAY_URL`, verify the authenticated relay routes, and deploy the Cloudflare Worker.
3. Do not share the `RELAY_SECRET` in chat.
