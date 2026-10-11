# jidict-frequency-yomitan

Yomitan frequency dictionary for JLPT (N1–N5) from JIDict.

## Install

1. Go to [Releases](../../releases/latest) and download `jidict-frequency-yomitan.zip`
2. Open Yomitan Settings → Dictionaries → Import → select the `.zip` (do not unzip)
3. Enable the dictionary and set it as frequency source if needed

## Update (auto)

This dictionary supports Yomitan's **Check for Updates**:

1. Yomitan Settings → Dictionaries → **Check for Updates**
2. If a new revision is available, click `!` → **Update**

This works via `isUpdatable`, `indexUrl`, and `downloadUrl` in `src/index.json`:

- `indexUrl`: `https://github.com/philiaspaceai/jidict-frequency-yomitan/releases/latest/download/index.json`
- `downloadUrl`: `https://github.com/philiaspaceai/jidict-frequency-yomitan/releases/latest/download/jidict-frequency-yomitan.zip`

Yomitan compares local `revision` with the remote `index.json` revision. If different, it downloads the new zip.

## For maintainers: how to release a new version

1. Edit files under `src/` (`term_meta_bank_*.json`, `index.json` description, etc.)
2. Commit to `main`
3. Create and push a new date-based tag matching the new revision, e.g.:
   ```bash
   # edit src/index.json revision first, e.g. 2026.10.18, commit it
   git tag 2026.10.18
   git push origin main --tags
   ```
4. GitHub Action [`.github/workflows/release.yml`](.github/workflows/release.yml) will:
   - sync `revision` in `index.json` to the tag name,
   - zip `src/*` into `jidict-frequency-yomitan.zip` (files at zip root, not nested),
   - create a GitHub Release for that tag with assets:
     - `jidict-frequency-yomitan.zip`
     - `index.json`
5. Users get the update via Yomitan Check for Updates (stable `latest/download` URLs).

Revision format: calendar versioning `YYYY.MM.DD` (e.g. `2026.10.11`).
