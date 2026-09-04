# Go-To_Gifting

Shopify theme for **go-togifting.com** (`bro-basket.myshopify.com`) — Horizon-based,
Go-To Gifting / BroBasket branding, plus the co-brand product and collection templates
used by the Bev Connect brand portals.

## Branches

| Branch | Role |
|---|---|
| `shopify-live` | **Deploy branch.** Connected to the published Shopify theme. A merge here is a production deploy. |
| `main` | Integration branch. Feature work lands here first via PR. |
| `<feature>-YYYY-MM-DD` | Dated feature branches. One change set each. |

Flow: `feature-YYYY-MM-DD` → PR → `main` → fast-forward `main` into `shopify-live` to release.

Never commit directly to `shopify-live`.

## Shopify GitHub sync

The Shopify GitHub App must be installed on the **The-Bev-Connect-Portals** org
(installations are per-account and do NOT follow a transferred repo).

Sync is two-way. Shopify pushes `Update from Shopify for theme ...` commits whenever
the theme or code editor is used, so **always `git pull --rebase` before pushing.**

### Verify after every merge — do not trust the green check

Inbound GitHub-to-Shopify ingest has failed silently on this repo before
(`templates/collection.cobrand-rincon.json` sat in the repo unsynced from Jul 22 to
Sep 3, 2026). After a release, confirm the change actually landed:

- Open the file in Shopify's code editor, or
- `curl -s https://go-togifting.com/ | grep <marker>` for a rendered marker

## Tracking

`snippets/gtm-head.liquid` / `snippets/gtm-body.liquid` load GTM container
`GTM-M6FQ7NLK`, rendered from `layout/theme.liquid`.

GTM does **not** run inside Shopify checkout — checkout is a sandboxed frame.
Purchase and conversion tracking is handled by a Shopify Custom Pixel
(Settings > Customer events), not by this container.

Google Ads `AW-18374903893` and Merchant Center `MC-SHJZGF9JH8` already fire via the
Google & YouTube channel's web pixel. Do not add a GA4 or Google Ads tag to
GTM-M6FQ7NLK or events will be double-counted.
