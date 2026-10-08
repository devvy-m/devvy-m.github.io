# devvy-m.github.io

The Pizza Cutter launch site. One small static site, no build step, no scripts, no external
requests. It exists to serve three things the App Store and AdMob require:

| File | Required by | App Store Connect field |
|---|---|---|
| `privacy.html` | Apple, for every app | Privacy Policy URL |
| `support.html` | Apple | Support URL |
| `app-ads.txt` | AdMob and LevelPlay | (the site root goes in **Marketing URL**) |

`index.html` is what AdMob shows as "Developer Website" at the bottom of the app's page, so it
is a real page rather than a redirect.

Published at **https://devvy-m.github.io/** — a repository named exactly `<user>.github.io`
publishes at the domain root, which is what puts `app-ads.txt` at `/app-ads.txt`.

The decision record and the reasoning behind all of this live in the game repository:
`docs/design/launch-setup-checklist.md`, section 5 ("Privacy and legal" and "Website").

## Still to do

1. **`app-ads.txt` is not here yet.** It needs the real AdMob publisher line, which AdMob gives
   under **Apps → View all apps → app-ads.txt**, plus LevelPlay's lines from its dashboard.
   `app-ads.txt.template` has the shape; fill it in and rename it to `app-ads.txt`. Do not
   publish a placeholder: a live `app-ads.txt` that lists no valid seller tells crawlers nobody
   is authorised to sell this app's inventory.
2. **Recheck the privacy policy against the shipped build.** It is written for the SDKs decided
   as of 8 October 2026: Unity LevelPlay, Google AdMob, Google UMP, Unity IAP and Apple's ATT
   prompt. Analytics, crash reporting and remote config were still *Suggested*, not decided, and
   are deliberately **not** described. If any of them ship, this page and the App Store privacy
   labels both need a new section before that version is submitted.
3. **Add the App Store link to `index.html`** once the app is live — there is a commented-out
   block ready for it.
4. **Custom domain, if one is bought later.** Add a `CNAME` file and the DNS records GitHub
   lists, then tick Enforce HTTPS. Note that the App Store **Marketing URL can only be edited
   when a new version is submitted**, so a move to a custom domain after launch needs an app
   update to go with it.

## Editing

Plain HTML and one stylesheet. `style.css` carries the game's palette from the design system
(`docs/design/design-system.md`) and has a dark-mode block. There are deliberately no web fonts:
ThaleahFat is licensed for use inside the game, not for redistribution, so it must not be served
from this site.
