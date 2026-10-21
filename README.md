# Imager

Minimal, API-first image hosting on Cloudflare Workers + R2 for agents and scripts.

## Setup

1. Create R2 bucket `personal-images`.
2. Connect this repo in Cloudflare Workers > Create > Import a repository, selecting main. Build command: `npm install`; deploy command: `npx wrangler deploy`.
3. In Worker settings add secret `ADMIN_TOKEN`, a long random value. Store it in Claude's environment as `IMAGE_API_KEY`.
4. Use your deployed Worker URL or attach a custom domain.

### Upload

```bash
curl --fail-with-body -sS -X POST https://YOUR_DOMAIN/api/v1/images \
  -H "Authorization: Bearer $IMAGE_API_KEY" \
  -H "Content-Type: image/png" --data-binary @image.png
```

Returns JSON with absolute `url`, `markdown`, `id` and file metadata.

### Other routes

- `GET /i/{id}` — public image delivery
- `GET /api/v1/images` — authorized list (supports `cursor`)
- `DELETE /api/v1/images/{id}` — authorized delete

Original images are public to anyone with the URL. Upload/list/delete require the bearer token. The R2 bucket itself stays private. No MCP needed.
