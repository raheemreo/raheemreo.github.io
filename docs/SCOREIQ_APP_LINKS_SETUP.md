# ScoreIQ verified Android App Links — deployment checklist

Production website: https://raheemreo.github.io/score_iq_web/
Verified app-link host: raheemreo.github.io
Required file: https://raheemreo.github.io/.well-known/assetlinks.json
Android package: com.reotech.scoreiq

## Why a root repository?
GitHub Pages project sites live under /score_iq_web/, but Android Digital Asset Links checks /.well-known/assetlinks.json **at the domain root**. Therefore the assetlinks file must be deployed through this root Pages repository or another host-root mechanism.

## App Signing certificate supplied (format validated)
Play Console App signing key (In use) SHA-256 supplied by the app owner:

`E9:DD:9F:2D:20:83:33:2F:C7:B3:A9:07:91:75:12:E8:DB:63:80:B2:06:73:09:08:B3:94:4F:70:77:0A:96:2A`

The actual `.well-known/assetlinks.json` and `.nojekyll` are included on this feature branch. The fingerprint format was validated as 32 colon-delimited hexadecimal bytes. Its Play Console provenance is owner-provided; live hosting and device verification have **not** yet been performed.

## Publish procedure (requires explicit permission)
1. Confirm this repository is the production GitHub Pages root for raheemreo.github.io.
2. Review the already staged `.well-known/assetlinks.json` against the current **In use** Play App Signing SHA-256 fingerprint.
3. Confirm `.nojekyll` is included in the actual Pages publishing source so `.well-known` is served.
4. Preserve existing ads.txt and app-ads.txt (do not edit them).
5. Deploy/merge only after explicit GitHub Pages production approval.
6. Confirm direct, unredirected HTTPS 200 for https://raheemreo.github.io/.well-known/assetlinks.json and valid JSON.
7. Check Android: adb shell pm verify-app-links --re-verify com.reotech.scoreiq; adb shell pm get-app-links com.reotech.scoreiq.
8. Verify the application is signed with the Play signing key; debug-key app installs may not match the JSON.
9. Check Play Console Deep links after the Play-signed updated release rolls out.

Note: Only five app-link website paths under /score_iq_web/open/ are registered in the Android app. Existing privacy, terms, data deletion, and support links should continue opening in the browser.
