# For Meitcy

A small pixel-art confession game for Meitcy. It is intentionally a story-first experience, not a template landing page.

## Install

From the project folder:

```bash
npm install
npm run dev
```

Then open `http://localhost:3000`.

## Where the story lives

Edit `src/data/story.ts`. The opening, chapter dialogue, timeline, final letter, response text, button labels, nicknames, and Easter eggs are all kept there so the personal writing is easy to update from a phone.

## Where the pixel art lives

The core pixel art is built locally in `src/components/PixelArt.tsx` and `src/app/globals.css`. This keeps sprites lightweight, crisp, and consistent without external image URLs.

## Editing the story

Change only `src/data/story.ts` for most text edits. The scene flow is defined in `src/data/story.ts` as `sceneOrder`.

## Response tracking

The browser sends `POST /api/response` with either `yes` or `no`. The server stores only the response and an ISO timestamp. A simple `POST /api/visit` counter records page loads so the private admin screen can show total visits. No location, contacts, camera, microphone, photos, passwords, or device fingerprinting are collected.

For persistence on Vercel, configure Upstash Redis environment variables:

- `KV_REST_API_URL`
- `KV_REST_API_TOKEN`

Without them, the story still works, but response tracking returns a storage-not-configured state.

## Admin page

Open `/admin` in a browser. It is protected by HTTP Basic Authentication in `middleware.ts`.

Configure:

- `ADMIN_USER` optional, defaults to `admin`
- `ADMIN_PASSWORD` required

The admin page shows the latest response, response timestamp, total visits, YES count, and NO count. It is not included in the public navigation and is protected server-side.

## Vercel deployment

1. Import this folder as a Next.js project in Vercel.
2. Add the environment variables above in the Production environment.
3. Deploy.
4. Set the same `ADMIN_USER` and `ADMIN_PASSWORD` in Vercel.
5. Confirm `/admin` prompts for credentials and `/api/response` accepts test responses before sharing the public URL.

## Phone-first editing

For simple changes, open `src/data/story.ts` in a mobile code editor and edit the strings there. The components are reusable, so visual changes can stay in `src/app/globals.css` and `src/components/PixelArt.tsx`.

## Notes

The site intentionally avoids external asset URLs, generic icon libraries, emoji artwork, gradient text, glassmorphism, excessive motion, and hover-only interactions. The NO choice remains possible and respectful.
