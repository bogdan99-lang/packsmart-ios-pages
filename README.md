# packsmart-ios-pages

Public website for the PackSmart apps (iPhone/iPad on iOS 17+ and Android 7.0+),
in English and Romanian, served with GitHub Pages at
`https://bogdan99-lang.github.io/packsmart-ios-pages/`. The repository name is
kept so that all published URLs stay the same.

| Page | URL | Used in |
|---|---|---|
| Home | `/` | App Store Connect → Marketing URL; Google Play listing → website; Google OAuth consent screen → home page. Links to both stores. |
| Support | `/support.html` | App Store Connect → Support URL; Google Play listing → contact/support. FAQs cover both apps (Android steps are marked "Android:"). |
| Privacy Policy (iOS) | `/privacy.html` | App Store Connect → Privacy Policy URL; AdMob consent (UMP) message on iOS; Google OAuth consent screen; Firebase sign-in providers |
| Privacy Policy (Android) | `/privacy-android.html` | Google Play listing → Privacy policy URL (the Firebase Hosting `/privacy` page redirects here) |
| Terms of Use | `/terms.html` | End of the App Store description ("Terms of Use: …"); the in-app paywall on both platforms. Covers iPhone, iPad and Android. |

Privacy section numbers are kept identical in the English and Romanian text and
are referenced from inside the pages (for example "sections 10 and 11"); if you
add or remove a section, update those references.

## Publishing

Repository → Settings → Pages → Source: *Deploy from a branch* → `main` / `/ (root)`.

## Keep in sync with the app

- **Gemini plan.** The Privacy Policy (section 5) assumes the Firebase
  project is on the paid Blaze plan, so Google doesn't use prompts to
  improve its products. If that changes, update section 5.
- **Premium.** If the plans, trial length or Premium features change,
  update Terms section 3 (English and Romanian) and the Premium FAQs in
  `support.html`. The pages deliberately show no prices.
- **Data flows.** Before adding analytics, crash reporting, cloud sync, cloud
  storage of photos or the App Tracking Transparency prompt, update both
  Privacy Policies, the App Store privacy answers and the Google Play Data
  safety form.
- **Effective dates.** Bump the "Effective" date on the privacy pages and the
  terms (English and Romanian) when their content changes.

## Release checklist (manual items)

1. **Deploy order.** Deploy the Firebase backend first (Cloud Functions,
   including the list-share changes for luggage, and Firestore rules/Hosting
   from the Android repository `packsmart-v2`), then release the iOS and Android
   apps, then publish these pages once the new app versions are available in
   the stores. These pages describe features (luggage, item photos, destination
   suggestions, weekly Premium, full-screen ads) that are only true once the
   new app versions are live.
2. **Store setup the pages assume.** The weekly Premium subscription must exist
   in App Store Connect (same subscription group as the yearly one) and in
   Google Play Console, and the AdMob full-screen (interstitial) ad units must
   be live. The product id used in code is a proposal until the owner
   approves it. Update the store privacy answers / Data safety form (camera
   and photos stay on the device) and the "contains ads" declarations.
   The apps also include Google Analytics for Firebase (collection starts only
   after ad consent, never for Premium) and the iOS app can show Apple's App
   Tracking Transparency prompt. The App Store "App Privacy" answers (tracking,
   Device ID, Advertising Data, Product Interaction) and the Play Console
   Advertising ID declaration / Data safety form must match sections 13 and 16
   of both privacy policies.
3. **`app-ads.txt` does not live in this repository's served site.** AdMob only
   reads `app-ads.txt` at the root of a domain, so the live copy is in the
   `bogdan99-lang.github.io` repository (served at
   `https://bogdan99-lang.github.io/app-ads.txt`). The copy in this repository
   is a reference only (this project site is served under
   `/packsmart-ios-pages/`). Keep the developer/marketing website URL in the
   store listings on host `bogdan99-lang.github.io`. Do not edit the file here
   without updating the other repository.
4. **`assetlinks.json` and `apple-app-site-association` are not in this
   repository on purpose.** They must be served from `/.well-known/` at the
   root of the domain used by the app links. The app links use
   `https://packsmart-a6d26.web.app` (Firebase Hosting), and a GitHub Pages
   project site cannot serve `/.well-known/` at a domain root (it is served
   under `/packsmart-ios-pages/`, which iOS and Android never read). Both files
   live in the Firebase Hosting folder of the Android repository
   (`packsmart-v2`, `public/.well-known/`) and are deployed with
   `firebase deploy --only hosting`.
5. **Play App Signing SHA-256 (owner input needed).** For verified Android App
   Links, `assetlinks.json` must contain the SHA-256 fingerprint of the
   **App signing key certificate** from Google Play Console → Setup → App
   integrity (not only the upload key). The fingerprint currently committed
   in the Android repository could not be verified; the owner must supply or
   confirm the Play App Signing SHA-256, add any other fingerprint to test
   with, redeploy Hosting, and check it on a device with
   `adb shell pm get-app-links com.packsmart.app`. For iOS, confirm that the
   Associated Domains capability is enabled for the app identifier in the Apple
   Developer portal.
