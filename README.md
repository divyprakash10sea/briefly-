# Briefly

An Android news reader that aggregates public RSS feeds, identifies the original publisher,
stores only headline, publisher and article URL, shows a short independently written summary,
and sends readers to the original article.

## Get the APK (no local setup)
1. Create a GitHub repository and push this folder to it (branch `main`).
2. Open the **Actions** tab, then **Build APK**. It runs automatically on push.
3. When it finishes, download `briefly-apk` from the run's **Artifacts**, unzip, and install the APK
   (allow "Install unknown apps" on your phone).

Tag a commit `v1.0.0` to publish the APK as a GitHub Release.

## Proper signing (for Play Store or updates)
Without secrets, the APK is signed with a debug key (installable, not for the Play Store).
Add these repository secrets to sign with your own key:
`KEYSTORE_BASE64` (`base64 -w0 release.jks`), `KEYSTORE_PASSWORD`, `KEY_ALIAS`, `KEY_PASSWORD`.

## Local build
Open in Android Studio (Koala or newer) and run, or `gradle assembleRelease` with Gradle 8.9 and JDK 17.

## Notes
- Publisher identification: Google News feeds tag each item with its original publisher; direct feeds
  (BBC, NPR, Guardian, Al Jazeera) use the feed's own name.
- Summaries: add an Anthropic API key in Settings. The model gets the headline and short feed blurb
  and writes an original 1-2 sentence summary. Without a key, cards show headline, publisher and link only.
- Google News links redirect to the original article when opened.
- Feed list lives in `data/Feeds.kt`. Respect each publisher's feed terms.
