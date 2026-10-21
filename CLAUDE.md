# Imager — image hosting API

For images Claude has permission to publish publicly, upload local image files to the Imager API:

```bash
curl --fail-with-body -sS -X POST "https://YOUR_WORKER_DOMAIN/api/v1/images" \
  -H "Authorization: Bearer $IMAGE_API_KEY" \
  -H "Content-Type: image/png" \
  --data-binary @image.png
```

The JSON response contains `url`, `markdown`, and `id`. Use the returned `url` as the public image link. Never print, commit, or expose the API key. Supported MIME types: PNG, JPEG, WEBP, GIF, AVIF. Upload limit: 15 MiB.
