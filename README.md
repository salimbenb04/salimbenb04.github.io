# Booma links (free, about 10 minutes)

YouTube and YouTube Music links always open in the official apps: Android only lets the owner of
youtube.com (Google) open those links automatically. So Booma shares links on an address of your own,
which Android lets Booma open automatically:

    https://YOUR-NAME.github.io/booma/?v=VIDEO_ID

- Friends with Booma: the link opens straight in Booma (song plays, playlist opens).
- Friends without Booma: the page sends them to the song in YouTube Music.

It's free (GitHub Pages). You do it once; afterwards every Booma you install handles these links.

## 1. Put this folder on GitHub Pages

1. On github.com, create a **public** repository named exactly **`YOUR-NAME.github.io`**
   (your GitHub user name, e.g. `khalil-dev.github.io`). It must be this name: Android checks a file at the
   root of the address.
2. Upload everything in this `share-page` folder, keeping the folders:
   `booma/index.html`, `.well-known/assetlinks.json` and `.nojekyll`.
   (On the website: Add file > Upload files, drag the folders in. If `.well-known` is hidden on your PC,
   show hidden files, or create the file on GitHub with Add file > Create new file and type the name
   `.well-known/assetlinks.json`.)
3. Settings > Pages > Deploy from a branch > `main` / `(root)` > Save. After a minute,
   `https://YOUR-NAME.github.io/booma/?v=dQw4w9WgXcQ` shows the Booma page.

## 2. Tell Android this address belongs to Booma

1. In the Booma project folder run:

       gradlew.bat signingReport

   Under `Variant: release` (or `debug`, they're the same key), copy the **SHA-256** line,
   e.g. `AB:CD:12:…` (32 pairs).
2. In the repository, edit `.well-known/assetlinks.json` and replace `PASTE:YOUR:SHA-256:FINGERPRINT:HERE`
   with it (keep the quotes). Commit.
3. Check it: `https://YOUR-NAME.github.io/.well-known/assetlinks.json` shows the file.

## 3. Build Booma with your address

1. In `gradle.properties` (Booma project folder), set:

       boomaShareHost=YOUR-NAME.github.io

2. Build (`gradlew.bat assembleRelease`) and install `installer/Booma.apk`.

Share buttons now send `https://YOUR-NAME.github.io/booma/…` links, and tapping one opens Booma.
Android checks the address when Booma is installed, so install after steps 1 and 2.
If a link still opens the browser: App info > Booma > Open by default > the address should show as verified;
reinstalling Booma makes Android check again.

Friends need a Booma built by you (the same signing key), which is the one you send them.
