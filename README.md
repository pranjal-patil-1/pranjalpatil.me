# pranjalpatil.me

Personal website for [Pranjal Patil](https://pranjalpatil.me) — Head of Engineering (Principal IC) building reliable systems at internet scale.

## Tech Stack

- **Framework:** [Astro](https://astro.build)
- **Hosting:** [Cloudflare Workers](https://workers.cloudflare.com) (static assets)
- **Styling:** Vanilla CSS with custom properties (dark/light mode)
- **Fonts:** Space Grotesk, Source Serif 4

## Project Structure

```text
src/
├── layouts/
│   └── Layout.astro        # Base HTML layout with theme toggle
├── pages/
│   └── index.astro          # Home page
└── styles/
    └── global.css           # Global styles & dark mode variables
public/
├── pranjal.jpeg             # Profile photo
├── favicon.svg              # Favicon
└── og-card.svg              # Open Graph card
```

## Development

```bash
npm install          # Install dependencies
npm run dev          # Start dev server at localhost:4321
npm run build        # Production build to ./dist/
npm run preview      # Preview production build locally
```

## Deploy

```bash
npm run deploy:worker
```

This runs `astro build` and then `wrangler deploy` to push static assets to Cloudflare Workers.

### Cloudflare console build settings

If deploying from the Cloudflare dashboard (Workers & Pages → Build):

| Setting                | Value                |
| ---------------------- | -------------------- |
| Build command          | `npm run build`      |
| Deploy command         | `npx wrangler deploy`|
| Build output directory | `dist`               |

### Custom Domain Setup (Cloudflare Workers)

If you're hosting your site on Cloudflare Workers and want to use a custom domain (e.g. `pranjalpatil.me`), follow these steps:

#### 1. Set the apex domain as your Worker's custom domain

- Go to **Workers & Pages** → select your worker → **Settings** → **Domains & Routes**
- Click **Add** → **Custom Domain**
- Enter your apex domain (e.g. `pranjalpatil.me`, without `www`)
- Cloudflare will automatically create the required DNS records

> **Why apex over www?** Most modern sites (github.com, vercel.com, cloudflare.com) use the apex domain. It's shorter, cleaner, and easier to share.

#### 2. Redirect `www` to the apex domain

Since Cloudflare Workers only allows one custom domain, set up a redirect for `www`:

**a) Add a DNS record for `www`:**

| Type | Name  | Content     | Proxy status |
| ---- | ----- | ----------- | ------------ |
| A    | `www` | `192.0.2.1` | Proxied      |

> The IP `192.0.2.1` is a dummy address — traffic won't reach it because Cloudflare's proxy intercepts it first.

**b) Create a redirect rule:**

- Go to **Rules** → **Redirect Rules** → **Create Rule**
- **Rule name:** `www to apex`
- **When:** Hostname equals `www.yourdomain.com`
- **Then:** Dynamic redirect to `https://yourdomain.com${http.request.uri.path}`
- **Status code:** 301 (permanent redirect)

This ensures:

- `yourdomain.com` → served by your Cloudflare Worker
- `www.yourdomain.com` → 301 redirects to `yourdomain.com`

#### 3. Verify DNS setup

Your Cloudflare DNS should have:

| Type    | Name  | Content                           | Proxy status |
| ------- | ----- | --------------------------------- | ------------ |
| A/CNAME | `@`   | *(auto-created by custom domain)* | Proxied      |
| A       | `www` | `192.0.2.1`                       | Proxied      |

Make sure **DNS Setup** shows **Full** and both records have the orange proxy cloud enabled.

#### 4. Update `astro.config.mjs`

Set the `site` field to your apex domain:

```js
export default defineConfig({
  site: "https://yourdomain.com"
});
```

This ensures sitemaps, canonical URLs, and Open Graph tags all point to the correct domain.

## License

Content and code in this repository are MIT licensed.
