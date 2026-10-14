# Gumroad Assets

Public hosting for cover art / thumbnails consumed by the Gumroad API
(`POST /v2/products/:id/covers` needs a server-fetchable image URL).

| File | Used by |
|---|---|
| `cover_1280x840.png` | product cover (The Gumroad Playbook 2026) |
| `thumb_square.png`   | product thumbnail (must be square) |

## Wiring (verified 2026-10-14)

```
https://raw.githubusercontent.com/yuhanbae/gumroad-assets/main/cover_1280x840.png
  -> POST /v2/products/<id>/covers   {url: ...}   OK
  -> POST /v2/products/<id>/thumbnail {url: thumb_square.png}   OK
```

Note: the pre-signed S3 attachment URL returned by `/v2/files/presign` is **not**
server-fetchable by Gumroad (403), so covers cannot come from the attachment
bucket directly — host images here (or any public CDN) instead.
