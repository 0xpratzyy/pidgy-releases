# pidgy-releases

Public release artifacts + Sparkle appcast feed for the Pidgy macOS app.

Source lives in the private [`telegraham`](https://github.com/0xpratzyy/telegraham) repo. This repo only hosts:

- **`appcast.xml`** — the feed Sparkle polls every 6 hours. New `<item>` blocks added at the top.
- **GitHub Releases** — each `vX.Y.Z` tag has the corresponding `Pidgy-<sha>.dmg` attached.

## Installing Pidgy (testers)

Download the latest DMG from the [Releases page](https://github.com/0xpratzyy/pidgy-releases/releases/latest), mount it, drag Pidgy to Applications. No Gatekeeper warning — every release is notarized by Apple.

After install, Pidgy auto-checks for updates every 6 hours, plus you can trigger a check manually via **Pidgy → Check for Updates…** in the menu bar.

## Cutting a new release (devs)

In the `telegraham` repo:

```sh
# 1. Bump the version
$EDITOR project.yml                     # bump MARKETING_VERSION

# 2. Build, sign, notarize, and print the appcast snippet
scripts/make_dmg.sh --publish

# 3. Follow the printed instructions: upload the DMG + paste the
#    snippet into this repo's appcast.xml, commit + push.
```

Within ~5 minutes of pushing, every installed Pidgy will see the new version on its next scheduled check.
