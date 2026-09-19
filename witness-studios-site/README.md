# Witness Studios — website

A 5-section marketing site (Home, Projects, Services, Rentals, Contact) built as a
single self-contained static page. No build step, no framework, no separate CSS/JS
files — `index.html` carries its own `<style>` and `<script>`. Open it in a server
and it runs.

Navigation between sections is client-side (no page reloads), backed by the URL
hash (`#projects`, `#services`, …), so links are shareable and back/forward work.

## Structure

```
index.html         Everything — markup, styles, and behavior in one file
assets/             Logo (white/ink), favicon set — the only other files the page needs
chats/, project/    The original Claude Design handoff bundle — kept for history,
                     not used by the live site
```

## Run it locally

Any static file server works, e.g.:

```
python3 -m http.server 8000
```

then open `http://localhost:8000`.

## Things that still need your input before this is fully live

**1. Contact form isn't sending anywhere yet.**
The page posts to [web3forms.com](https://web3forms.com) (a free, keyless-backend
form relay — no server needed). Right now the hidden `#formAccessKey` input holds a
placeholder, so submitting shows "Form isn't wired up yet" instead of silently
failing. To activate: create a free account at web3forms.com, copy your Access
Key, and paste it into:

```html
<input type="hidden" name="access_key" id="formAccessKey" value="YOUR_WEB3FORMS_ACCESS_KEY">
```

**2. Hero video is a placeholder.** The original design had an AI-generated demo
clip here; we agreed that didn't belong on a page representing your real work.
The hero currently shows a "Showreel — footage to supply" marker in the top
corner. To add real footage, replace the `.hero-video-slot` block with:

```html
<video autoplay muted loop playsinline preload="metadata"
       poster="assets/hero-poster.jpg" src="assets/witness-reel.mp4"></video>
```

placed as the first child of `.hero` (before the grain overlay), then remove the
`.hero-video-slot` block.

**3. Rentals equipment photo is a placeholder** for the same reason (the supplied
image also looked AI-generated rather than a photo of your actual gear). Replace
the `.placeholder-block` inside `.rentals-feature-media` with a real `<img>` once
you have one.

**4. Selected-work / Projects thumbnails and Services process stills** are
intentionally brand-tinted placeholder blocks, not stock photos — per your
instruction not to represent real client work with imagery that isn't actually
from that project. Swap in real stills/video frames as they become available.

## Deploying

It's static — Netlify, Vercel, GitHub Pages, or any S3-style bucket all work with
zero configuration. Just make sure `index.html` and `assets/` ship together
relative to the same root.
