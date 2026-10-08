# devvy-m.github.io

The Pizza Cutter launch site. One small static site, no build step, no scripts, no external
requests. It exists to serve three things the App Store and AdMob require:

| File | Required by | App Store Connect field |
|---|---|---|
| `pizza-cutter/privacy.html` | Apple, for every app | Privacy Policy URL |
| `pizza-cutter/support.html` | Apple | Support URL |
| `pizza-cutter/index.html` | AdMob, as the developer website | Marketing URL |
| `app-ads.txt` | AdMob and LevelPlay | — (must stay at the domain root) |

The root `index.html` is a small landing page listing the games; it is **not** one of Pizza
Cutter's registered URLs, so it can change freely. Each game owns a folder, and that folder's
page is what AdMob shows as "Developer Website" at the bottom of the app's page.

```
/                            landing page, lists games (free to change)
/app-ads.txt                 shared by ALL apps on this domain; must stay here
/style.css
/pizza-cutter/               <- Marketing URL
/pizza-cutter/privacy.html   <- Privacy Policy URL
/pizza-cutter/support.html   <- Support URL
```

Published at **https://devvy-m.github.io/** — a repository named exactly `<user>.github.io`
publishes at the domain root, which is what puts `app-ads.txt` at `/app-ads.txt`.

The decision record and the reasoning behind all of this live in the game repository:
`docs/design/launch-setup-checklist.md`, section 5 ("Privacy and legal" and "Website").

## Still to do

1. **Re-check `app-ads.txt` periodically.** It is complete as of 8 October 2026: the AdMob
   DIRECT line, the ironSource DIRECT line (publisher id 689029), the IAB `ownerdomain` field,
   and ironSource's 125 authorised-reseller lines. **Unity updates that reseller list from time
   to time** — re-copy it from
   <https://docs.unity.com/en-us/grow/programmatic/ironsource-exchange/app-ads-txt> now and then,
   and whenever an ad network is added or removed in LevelPlay.
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

## Adding a second game later

The site is structured for this from the start (Devon, 8 October 2026): each game owns a folder,
so a second one is a new folder and nothing moves.

- **`app-ads.txt` stays at the root, and is shared by every app.** AdMob reads only the *domain*
  from an app's Marketing URL and looks for `/app-ads.txt` there, so one file serves all your
  apps — Google's page notes that a crawl "updates the status for all apps that share the same
  app-ads.txt file". The AdMob and ironSource publisher lines are account-level, so they are
  already correct for a future game. A new game only adds lines if it uses a new ad network.
- **Give each new game its own folder**: `/next-game/privacy.html`, `/next-game/support.html`,
  and `/next-game/` as that app's Marketing URL. Paths are ignored by AdMob's crawler, so a
  subfolder Marketing URL still resolves `app-ads.txt` at the root.
- **Never move a game's pages once its version is live.** Those URLs are printed into App Store
  Connect, and at minimum the Marketing URL cannot be changed without submitting a new app
  version. This layout exists so that never becomes necessary.
- Turning `/` into a studio landing page that lists games is free at any time — it is not one of
  the three registered URLs for Pizza Cutter, only the Marketing URL's domain matters.

## Editing

Plain HTML and one stylesheet. `style.css` carries the game's palette from the design system
(`docs/design/design-system.md`) and has a dark-mode block. There are deliberately no web fonts:
ThaleahFat is licensed for use inside the game, not for redistribution, so it must not be served
from this site.
