# ITR Computation Sheet — Android App Package

This folder is a complete **Progressive Web App (PWA)**. On Android it installs
like a real app — its own icon, its own window (no browser address bar), and it
keeps working offline once loaded — with no Play Store submission needed.

## Folder contents
```
index.html          the app itself
manifest.json        app name, icons, colors (what makes it "installable")
service-worker.js     caches the app so it works offline
icons/                app icon in the sizes Android expects
```

## Option A — Install it on your phone in 2 minutes (no build tools)
PWAs need to be served over `http(s)://`, not opened directly as a `file://`,
for the install prompt and offline caching to work. Easiest free ways to host it:

1. **GitHub Pages** — create a new public repo, upload these files, turn on
   Pages in repo settings. You'll get a URL like
   `https://yourname.github.io/itr-app/`.
2. **Netlify Drop** — go to app.netlify.com/drop and drag this folder in.
   Gives you a live URL immediately, no account required for a quick test.

Then, on your Android phone:
1. Open that URL in **Chrome**.
2. Tap the **⋮** menu → **"Install app"** (or **"Add to Home screen"**).
3. It installs with the stamp icon and opens full-screen like any other app.

## Option B — Get an actual installable `.apk` / Play Store `.aab`
If you specifically want a file ending in `.apk`, use **PWABuilder** (free,
made by Microsoft, no coding required):

1. Host the folder using Option A first, so you have a live URL.
2. Go to **https://www.pwabuilder.com**, paste your URL, click **Start**.
3. Click **Android** in the package options → **Generate Package**.
4. Download the `.apk` (for direct installation) or `.aab` (for Play Store
   submission).

PWABuilder wraps the site in a Trusted Web Activity — a thin native Android
shell — so the generated app is a real installable package, not just a
shortcut.

## Option C — Wrap it natively yourself (Capacitor)
If you want to keep customizing it in Android Studio with native plugins
(camera, biometrics, etc.), Capacitor can wrap these same files:
```
npm install -g @capacitor/cli @capacitor/core @capacitor/android
npx cap init "ITR Computation Sheet" "com.yourname.itrsheet"
npx cap add android
# copy index.html, manifest.json, service-worker.js, icons/ into ./www
npx cap open android   # opens the project in Android Studio to build/run
```

## Notes
- All calculations run entirely on the device — nothing is sent to a server.
- Excel/JSON exports use the device's normal file-save/share flow once wrapped
  as a native app (via PWABuilder or Capacitor); inside plain Chrome they
  download to the Downloads folder as usual.
- This remains a simplified planning tool, not an official filing utility —
  see the in-app disclaimer.
