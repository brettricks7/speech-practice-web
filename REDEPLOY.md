See README.md for full redeploy steps.

Quick path once source is local at `$SP_SRC`:

```bash
cd "$SP_SRC"
flutter build web --release --base-href=/speech-practice-web/
rsync -a --delete --exclude='.last_build_id' build/web/ /path/to/speech-practice-web-checkout/
# commit + force-push gh-pages (or main if that is your Pages branch)
```
