# packsmart-ios-pages

Public website for the PackSmart iOS app, in English and Romanian, served
with GitHub Pages at `https://bogdan99-lang.github.io/packsmart-ios-pages/`.

| Page | URL | Used in |
|---|---|---|
| Home | `/` | App Store Connect → Marketing URL; Google OAuth consent screen → home page |
| Support | `/support.html` | App Store Connect → Support URL |
| Privacy Policy | `/privacy.html` | App Store Connect → Privacy Policy URL; AdMob consent (UMP) message; Google OAuth consent screen; Firebase sign-in providers |
| Terms of Use | `/terms.html` | End of the App Store description ("Terms of Use: …"); the in-app paywall |

## Publishing

Repository → Settings → Pages → Source: *Deploy from a branch* → `main` / `/ (root)`.

## Keep in sync with the app

- **App Store link.** When the App Store listing exists, replace the "Coming
  soon to the App Store" label in `index.html` with a link to
  `https://apps.apple.com/app/id…`.
- **app-ads.txt.** AdMob only reads `app-ads.txt` at the root of a domain,
  so it can't live in this project site (it is served under
  `/packsmart-ios-pages/`). Put it either in a repository named
  `bogdan99-lang.github.io` (served at `https://bogdan99-lang.github.io/app-ads.txt`),
  or in this repository once it has a custom domain. The file contains one
  line, with your AdMob publisher ID:
  `google.com, pub-XXXXXXXXXXXXXXXX, DIRECT, f08c47fec0942fa0`
- **Gemini plan.** The Privacy Policy (section 5) assumes the Firebase
  project is on the paid Blaze plan, so Google doesn't use prompts to
  improve its products. If that changes, update section 5.
- **Premium.** If the trial length, prices or Premium features change,
  update Terms section 3 (English and Romanian).
- **Data flows.** Before adding analytics, crash reporting, cloud sync or
  the App Tracking Transparency prompt, update the Privacy Policy and the
  App Store privacy answers.
