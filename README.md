# pranjalpatil.me

Professional personal website for Pranjal Patil, built with Astro and ready for Cloudflare Pages.

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

## Deploy to Cloudflare Pages

Use one of the following methods:

### 1) Cloudflare Dashboard

1. Create a new Pages project and connect this GitHub repository.
2. Use these build settings:
   - Framework preset: `Astro`
   - Build command: `npm run build`
   - Build output directory: `dist`
   - Node.js version: `20` (or newer supported by Astro)
3. Deploy.

### 2) Wrangler CLI

```bash
npm run build
npx wrangler pages deploy dist --project-name pranjalpatil-me
```

`wrangler.toml` is already configured with `pages_build_output_dir = "dist"`.
