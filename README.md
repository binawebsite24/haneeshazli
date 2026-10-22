# haneeshazli

Personal digital business card — a single self-contained `index.html`.

Save-contact (vCard), share sheet, on-page QR, and quick links to WhatsApp,
Instagram and email. All assets are inlined, so there is nothing to build:
the file is the site.

## Deploy

Pushing to `main` deploys to Cloudflare Pages automatically —
<https://haneeshazli.pages.dev>. No build command; the repo root is served
as-is.

## Editing

`index.html` is a self-extracting bundle: the real page lives as JSON in a
`<script type="__bundler/template">` tag, and on load the unpacker calls
`document.documentElement.replaceWith(...)`, swapping out the whole
document — head included.

That matters for the link preview. Chat crawlers never run JavaScript, so
the Open Graph tags have to sit in the outer shell for WhatsApp to see
them; they are mirrored inside the template too, or the unpacker would
drop them the moment the page loads. **Re-exporting the card from the
editor overwrites both copies**, so the tags have to be re-applied each
time.

`og.jpg` (1200×630) is the preview image. WhatsApp caches previews per URL
for about a week — if you replace it, give it a new filename and update
`og:image`, or the old one keeps showing.
