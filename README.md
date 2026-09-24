# Speech Practice (public web snapshot)

Live demo: **https://brettricks7.github.io/speech-practice-web/**

Public GitHub Pages snapshot of the Speech Practice Flutter web build (mock scoring).  
**Source stays private** in [`brettricks7/carl`](https://github.com/brettricks7/carl) at `products/speech-practice/`.

This site is built **without** Azure `--dart-define` keys, so it runs in **mock scoring** mode (UI review only).

## Redeploy

From a machine with Flutter stable + `gh` authenticated as `brettricks7`:

```bash
# 1) Get / update source (example: tarball extract)
gh api repos/brettricks7/carl/tarball/main > /tmp/carl.tar.gz
# extract products/speech-practice/ to SP_SRC

# 2) Build (mock mode = no Azure dart-defines)
cd "$SP_SRC"
flutter pub get
flutter build web --release --base-href=/speech-practice-web/

# 3) Publish build/web to this repo's gh-pages branch
rm -rf /tmp/sp-pages && mkdir /tmp/sp-pages
rsync -a --delete --exclude='.last_build_id' build/web/ /tmp/sp-pages/
cd /tmp/sp-pages
git init
git checkout -b gh-pages
git add -A
git -c user.name='brettricks7' -c user.email='brettricks7@users.noreply.github.com' \
  commit -m "Redeploy Speech Practice web (mock scoring)"
git remote add origin https://github.com/brettricks7/speech-practice-web.git
git push -f origin gh-pages
```

Pages source: branch `gh-pages`, folder `/`.
