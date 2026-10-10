# WHYITEM — Parallel Worlds (Offline MVP)

A bilingual (Korean/English), text-first, offline RPG prototype. Every world is generated and saved locally on the device. No game server, account, remote database, or AI API is used by the core game.

## Included in this first playable build

- Mobile-first, portrait-oriented UI designed for ordinary smartphone screens.
- Korean / English toggle.
- Multiple independent parallel worlds with randomized rules and world seeds.
- Procedurally generated item names, rarity, stats, and effect combinations.
- Explore, local world events, chronicle/history, and simulated battles against a world echo.
- Items with no image display `?` and prompt the player to add their own image.
- Player-selected images are resized locally and stored in IndexedDB on the device.
- Export one world or all worlds to JSON; import backups.
- No network requests are made by the game code.

## Important limitations of this MVP

- This is a playable prototype/source project, not a signed Android APK/AAB. Google Play submission requires building and signing an Android App Bundle in Android Studio and completing Play Console setup.
- This MVP uses a rules engine that simulates an AI-like world; it does not call a generative AI model.
- Core gameplay is offline single-player. Online rankings, multiplayer, cloud sync, and cross-device save transfer are intentionally not included.
- App data can be lost if the user clears storage or uninstalls the app. Encourage users to export backups.
- The app is not yet fully QA-tested across all Android devices. Test the generated Android build on real phones before release.

## Run as a local web app

Because the game is static, you can open `www/index.html` in a modern browser for a quick test. Some browsers restrict IndexedDB/file-origin behavior when opened directly; for reliable testing, use a local static server such as `npx serve www` (the server is only for local development; the game itself makes no network calls). For actual offline play, use the Android app build below.

## Build an Android project with Capacitor

Requirements: Node.js LTS, Android Studio, a compatible Android SDK, and Java version required by your installed Android Gradle Plugin.

1. Unzip this project on a computer.
2. In the project folder, run:

   ```bash
   npm install
   npx cap add android
   npx cap sync android
   npx cap open android
   ```

3. In Android Studio, run the app on a real Android phone and test offline mode, world saves, image picker, export/import, and Korean/English text.
4. For Google Play, configure the application ID, app icon, version code/name, privacy/data-safety disclosures, and signing key. Then use **Build > Generate Signed Bundle / APK > Android App Bundle** and upload the signed `.aab` to Play Console.

If `npx cap add android` reports that an Android platform already exists, skip that command and run `npx cap sync android`.

## Offline / privacy notes

- Game state and uploaded item images are stored in local IndexedDB inside the app WebView.
- The app does not need an account or backend.
- Image files are processed locally in the browser/WebView and reduced to a maximum 512px longest edge before saving.
- Do not add analytics, ad SDKs, remote fonts, remote image URLs, or other network dependencies if strict offline operation is a product requirement.
- Capacitor/Android build tooling may include default permissions; review the final merged Android manifest and remove unnecessary permissions before release. Verify network behavior using airplane mode and a traffic inspection test.

## Project structure

- `www/index.html` — app shell and navigation
- `www/styles.css` — mobile-first readable UI
- `www/app.js` — world generation, local save, items, image upload, combat, backup/import
- `www/manifest.webmanifest` — PWA metadata
- `capacitor.config.ts` — Android wrapper configuration

## Pricing note

The planned KRW 1,000 price is configured in Google Play Console, not in the source code. Availability and pricing depend on Play Console account setup, country/region settings, taxes, and current Play policies.
