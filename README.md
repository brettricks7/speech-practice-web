# Speech Practice (public web snapshot)

Live demo: **https://brettricks7.github.io/speech-practice-web/**

Public GitHub Pages snapshot of the Speech Practice Flutter web build (**mock scoring**).  
**Source stays private** in [`brettricks7/carl`](https://github.com/brettricks7/carl) at `products/speech-practice/`.

Built **without** Azure `--dart-define` keys → mock scoring banner for UI review only. No secrets in this repo.

## Redeploy

Needs: Flutter stable on PATH, `gh` auth as `brettricks7`, `rsync`.

```bash
# 1) Fetch source (tarball; no full clone required)
gh api repos/brettricks7/carl/tarball/main > /tmp/carl.tar.gz
PREFIX=$(tar -tzf /tmp/carl.tar.gz | head -1 | cut -d/ -f1)
rm -rf /tmp/sp-src && mkdir -p /tmp/sp-src
tar -xzf /tmp/carl.tar.gz -C /tmp/sp-src --strip-components=2 \
  "${PREFIX}/products/speech-practice"

# 2) Build mock web for project Pages
cd /tmp/sp-src
flutter pub get
flutter build web --release --base-href=/speech-practice-web/

# 3) Publish ONLY build/web to gh-pages (include .nojekyll)
rm -rf /tmp/sp-pages && mkdir /tmp/sp-pages
rsync -a --delete --exclude='.last_build_id' build/web/ /tmp/sp-pages/
touch /tmp/sp-pages/.nojekyll
# optional: copy this README into /tmp/sp-pages/

cd /tmp/sp-pages
git init
git checkout -b gh-pages
git add -A
git -c user.name='brettricks7' -c user.email='brettricks7@users.noreply.github.com' \
  commit -m "Redeploy Speech Practice web (mock scoring)"
git remote add origin https://github.com/brettricks7/speech-practice-web.git
git push -f origin gh-pages
```

Pages: branch `gh-pages`, folder `/` → https://brettricks7.github.io/speech-practice-web/
