# Deploying

The site is public, published from this repository by GitHub Pages at
**<https://has-reasoning.github.io/reasoning-workshop-2027/>**.

There is no build server and no Actions workflow. GitHub serves the `.html`
files in the repository root exactly as they are, so:

```sh
python3 tools/build.py     # only if you edited tools/build.py
git add -A
git commit -m "Update the program"
git push
```

The live site updates within a minute or two. `.nojekyll` is present, which
stops GitHub trying to run Jekyll over the files.

## Checking a change before you push

```sh
python3 -m http.server 8000
```

Then open <http://localhost:8000>. This serves the same files GitHub does, so
what you see is what will ship.

## Pages settings

Already configured, but for reference: **Settings → Pages → Source: Deploy from
a branch → `main` / `(root)`**.

## Custom domain

If the department gets a domain or an `arizona.edu` subdomain from UITS:

1. Add a file named `CNAME` in the repository root containing only the
   hostname, e.g. `b2workshop.arizona.edu`.
2. Point DNS at GitHub — a `CNAME` record to `has-reasoning.github.io` for a
   subdomain, or GitHub's four `A` records for an apex domain.
3. **Settings → Pages → Custom domain**, enter it, and tick **Enforce HTTPS**
   once the certificate is issued.

Doing this would provide a shorter public address if the department wants one.

## Repository ownership and the original URL

The site is owned by the `has-reasoning` GitHub organization. The canonical
repository is <https://github.com/has-reasoning/reasoning-workshop-2027>.

The official flyer was created while the site still used Nabin's personal
GitHub Pages address, so its QR code points to:

<https://nkalauni.github.io/reasoning-workshop-2027/>

That address is intentionally kept alive by a separate, minimal redirect
repository under `nkalauni`. Do not delete or repurpose it while printed flyers
or other old links may still be in circulation. It forwards every path to the
canonical organization-hosted site.

If a custom domain is added later, update both the canonical site and this
redirect.

## Taking the site private again

If you ever need to pull it back to a reviewers-only draft, set
`PRIVATE_DRAFT = True` in `tools/build.py` and rebuild. That restores the draft
banner and the `noindex` tag on every page. Note that this does *not* hide the
site: **a private repository still publishes a public website.** Access-
controlled Pages requires GitHub Enterprise Cloud. For a genuinely gated
preview you would need to host it elsewhere — Cloudflare Pages plus Cloudflare
Access does it on the free tier, with email one-time PINs.

## Still to do before this is print-ready

- [ ] Confirm `has-reasoning@arizona.edu` is live and being read — it is the
      contact address on every page
- [ ] Registration page still says "date to be announced"
- [ ] Abstract submission system not chosen, so nothing is linked
