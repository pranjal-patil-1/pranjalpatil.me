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

### Custom domain

The site is served at [pranjalpatil.me](https://pranjalpatil.me) via Cloudflare DNS with a Worker route.

## License

Content and code in this repository are MIT licensed.
