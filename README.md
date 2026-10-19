# Elyss School Open Day — Landing Page

Mashujaa Day campaign landing page (`index.html`) and post-registration page
(`thank-you.html`). Static HTML/CSS/JS, no build step; deploys to Netlify as-is.

```
index.html          landing page + Netlify form "elyss-open-day"
thank-you.html      shown after submitting (fires the Meta Pixel Lead event)
assets/landing.css  shared styles (palette tokens live in each page's <style> block)
assets/landing.js   validation, Netlify submission, WhatsApp hand-off, Pixel, UTM capture
images/             logo and Mashujaa artwork cropped from the school's poster
netlify.toml        publish settings
```

## Deploying on Netlify

1. Netlify → **Add new site → Import an existing project → GitHub** → pick this repo
   and the branch holding this code. Build command: *(empty)*. Publish directory: `.`
2. **Site configuration → Forms → Enable form detection**, then **Deploys → Trigger deploy**.
3. Check **Forms** lists `elyss-open-day`, and add an email notification for the admissions team.

## Settings (`window.LANDING`, top of both pages)

`phone`, `whatsapp` (international format, e.g. 2547XXXXXXXX), `waIntro`, `metaPixelId`,
`formEndpoint` (optional extra webhook), `campaign`. Elements marked `data-contact` are
filled from these and hidden while empty, so the page never shows a dead link.

## Confirm before publishing

Open Day dates (21–30 Oct, skipping Mashujaa Day on 20 Oct and Sunday 25 Oct) come from the planning sheet's recommended window, not a confirmed school date. Edit the `visit_date` options in `index.html` once confirmed. Times are offered as Morning/Afternoon only.

Local preview: `python3 -m http.server 8080` (form submissions only work on Netlify).
