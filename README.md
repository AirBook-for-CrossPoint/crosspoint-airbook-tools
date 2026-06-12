# CrossPoint AirBook Tools

Web-based firmware flasher and build system for the [CrossPoint Reader + AirBook](https://github.com/Yoddikko/crosspoint-reader) fork. Serves firmware that includes the AirBook iOS companion app BLE integration.

Adapted from [crosspoint-reader/crosspoint-tools](https://github.com/crosspoint-reader/crosspoint-tools).

## Differences from upstream tools

- **Firmware source** — All firmware served is built from the [`Yoddikko/crosspoint-reader`](https://github.com/Yoddikko/crosspoint-reader) fork (CrossPoint + AirBook), not the main `crosspoint-reader/crosspoint-reader` repo
- **Upstream sync tracking** — The landing page shows how many commits behind (or ahead) of upstream CrossPoint Reader this fork is, via the `/api/upstream-status` endpoint
- **AirBook mention** — Landing page and meta tags reference the AirBook iOS companion app

## Architecture

Same as upstream: Cloudflare Worker (`src/index.ts`), R2 bucket for firmware binaries, KV for metadata, GitHub Actions for CI builds.

## Setup

```bash
npm install
npx wrangler r2 bucket create crosspoint-firmware
npx wrangler kv namespace create BUILD_META
npx wrangler secret put GITHUB_WEBHOOK_SECRET
npx wrangler secret put GITHUB_TOKEN
npm run deploy
```

The worker builds firmware from `Yoddikko/crosspoint-reader` by default. Override with env vars:
- `GITHUB_ACTIONS_REPO` — defaults to `Yoddikko/crosspoint-reader`

## License

MIT — same as upstream.
