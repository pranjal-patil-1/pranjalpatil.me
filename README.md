# pranjalpatil.me

Professional personal website for Pranjal Patil, built with Astro and ready for Cloudflare Workers deployment.

## Local development

```bash
npm install
npm run dev
```

## Production build

```bash
npm run build
npm run preview
```

## Deploy to Cloudflare Workers

### Wrangler CLI

```bash
npm run deploy:worker
```

`wrangler.toml` is configured to deploy the static Astro build from `dist`:

```toml
[assets]
directory = "./dist"
```

### Cloudflare console build settings

If you deploy from Cloudflare console using build + deploy commands:

- Build command: `npm run build`
- Deploy command: `npx wrangler deploy`
- Non-production branch deploy command: `npx wrangler versions upload`
- Path: `/`
