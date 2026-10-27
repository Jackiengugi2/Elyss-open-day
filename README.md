# Elyss School — Meta Ads Landing Page

Form-first landing page for Meta ads: logo header, a one-line headline, then the form.
`thank-you.html` is shown after submitting and fires the Meta Pixel `Lead` event.
Static HTML/CSS/JS, no build step.

```
index.html          landing page + Netlify form "elyss-open-day"
thank-you.html      post-submit page with WhatsApp hand-off
assets/landing.css  shared styles (school palette lives in each page's <style> block)
assets/landing.js   validation, Netlify submission, WhatsApp hand-off, Pixel, UTM capture
images/logo.png     school logo
netlify.toml        publish settings
```

## Settings (`window.LANDING`, top of both pages)

| Key | Value |
|---|---|
| `phone` / `whatsapp` | 0711 650 405 / 254711650405 |
| `campaign` | `ELYSS_LEAD_LP_OpenDay_PROS_OCT26` (playbook naming: CLIENT_OBJ_DEST_SEGMENT_LAYER_MMMYY) |
| GTM container | `GTM-M7XNWV3Q` (snippet in `<head>` and right after `<body>` on both pages) |
| `metaPixelId` | empty: add the Pixel ID on both pages | (or load the Pixel through GTM instead, not both) |
| `formEndpoint` | optional extra webhook (Privyr / Google Sheet) |

Ad links should carry `utm_source=meta&utm_campaign=<Ads Manager name>`; the form saves
every `utm_*` value and `fbclid` with the enquiry.

## GTM dataLayer events

| Event | When | Extra fields |
|---|---|---|
| `form_start` | first interaction with the form | `form_name`, `campaign`, `school` |
| `form_submit` | Netlify accepted the enquiry (form page) | `form_name`, `grade`, `campaign`, `school` |
| `generate_lead` | thank-you page, once per enquiry | `form_name`, `grade`, `campaign`, `school` |

Use `generate_lead` (or a Page View trigger on `/thank-you.html`) for the Meta Pixel `Lead`
and any conversion tag.

## Netlify

Publish directory `.`, no build command. Enable **Forms** and check `elyss-open-day` is listed;
add an email notification under **Forms → Form notifications**.

## Notes

Open Day is Saturday 14 November 2026 (hidden `visit_date` field). Campus is not shown on the page until the school confirms it.

Local preview: `python3 -m http.server 8080` (form submissions only work on Netlify).
