# aionbuilt.com

The Aion Innovations LLC site — a single static page at `index.html` with no
build step and no dependencies. Open it in a browser to preview; there is
nothing to install.

## Editing

Everything is in `index.html`, marked with `TODO` comments in the order worth
filling in:

1. **Hero** — your name and one sentence on what you build. Specific beats broad.
2. **Selected work** — three sharp projects, each linked to a repo or live demo.
   Duplicate an `<article class="project">` block to add another.
3. **Contact** — LinkedIn URL.

Styling is a set of CSS custom properties at the top of the `<style>` block.
Change `--accent` to re-skin the page; light and dark both derive from those
tokens, so they stay in sync.

## Deploying

`.github/workflows/deploy-pages.yml` publishes the repo root on every push to
`main`. To turn it on:

1. **Settings → Pages → Source: GitHub Actions**
2. **Settings → Pages → Custom domain:** `aionbuilt.com` (the `CNAME` file
   already sets this; the field should populate itself)
3. Add these records in the Cloudflare dashboard, both set to **DNS only** —
   the grey cloud, not the orange one:

   | Type  | Name             | Target                |
   |-------|------------------|-----------------------|
   | CNAME | `aionbuilt.com`  | `mmorrisj.github.io`  |
   | CNAME | `www`            | `mmorrisj.github.io`  |

4. Wait for the certificate, then tick **Enforce HTTPS**.

GitHub provisions HTTPS through Let's Encrypt, which requires seeing the request
reach its own servers. With Cloudflare's proxy enabled the challenge fails
silently and "Enforce HTTPS" stays greyed out. Leave the records on DNS only.

This repo must stay **public** for Pages to serve it on a free account.

## Email

Pages serves static files only — it cannot receive or send mail, so
`hello@aionbuilt.com` needs to come from somewhere else.

Use **Cloudflare Email Routing** (free): in the Cloudflare dashboard, pick the
domain, open **Email → Email Routing**, and add a rule forwarding
`hello@aionbuilt.com` to your personal inbox. It writes the required MX records
itself. Verify the destination address when the confirmation mail arrives, or
the route stays inactive.

That covers receiving. To *send* from the address, add it to Gmail as a send-as
account — which needs an SMTP relay, either Google Workspace (~$7/user/mo) or
the existing Bluehost account, whose cPanel provides SMTP credentials.

Forwarding alone is fine to start; replies just come from your personal address.
