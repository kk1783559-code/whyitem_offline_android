# Google Play release checklist

- [ ] Decide final app name, package ID, icon, screenshots, and store listing text.
- [ ] Build and test a signed Android App Bundle (`.aab`) in Android Studio.
- [ ] Set version code/name and confirm the target SDK requirement in Play Console at release time.
- [ ] Test on a real Android phone with airplane mode enabled.
- [ ] Verify world creation, switching, saves after force-close/restart, image upload, backup export/import, and language switching.
- [ ] Review the merged Android manifest and remove any permission that is not needed.
- [ ] Confirm there are no network requests, analytics SDKs, remote fonts, or remote assets if the product promise is fully offline.
- [ ] Complete Play Console Data safety, privacy policy/contact, content rating, target audience, and app access sections truthfully.
- [ ] Keep a secure copy of the signing key and exportable world-backup instructions.
- [ ] Set the intended one-time price (e.g. KRW 1,000) in Play Console; pricing is not hard-coded in this project.
- [ ] Follow any current closed-testing / developer-account requirements shown by Play Console.
