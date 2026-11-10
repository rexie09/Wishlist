# Our Wishlists — GitHub Pages + Firebase setup

About 15 minutes, all free. You need a Google account and a GitHub account.

## 1. Create the Firebase project
1. Go to https://console.firebase.google.com → **Create a project** (name it e.g. `our-wishlists`). Google Analytics can be off.
2. **Build → Authentication → Get started → Sign-in method → Google → Enable** → Save.
3. **Build → Firestore Database → Create database** → pick a location near you (e.g. `us-west`) → start in **production mode**.
4. **Project settings (gear) → Your apps → Web (`</>`)** → register an app (no hosting). Copy the `firebaseConfig` values it shows.

## 2. Lock it down
1. Open `firestore.rules`, replace `you@gmail.com` and `her@gmail.com` with your two real Google emails (lowercase).
2. Firebase console → **Firestore → Rules** → paste the whole file → **Publish**.

## 3. Fill in the page
Open `index.html`, find the `EDIT THESE` block near the bottom:
- paste your `apiKey`, `authDomain`, `projectId`, `appId`
- set `OWNER_EMAIL` (you) and `PARTNER_EMAIL` (her) — same emails as the rules

The Firebase config is *meant* to be public; the rules are what keep strangers out.

## 4. Put it on GitHub Pages
1. GitHub → **New repository** (e.g. `wishlist`). Public is fine — there's no private data in the code.
2. Upload `index.html` (and the other files if you like).
3. Repo **Settings → Pages → Source: Deploy from a branch → `main` / root → Save.**
4. After a minute your site is at `https://YOUR-USERNAME.github.io/wishlist/`.

## 5. Allow your domain to sign in
Firebase console → **Authentication → Settings → Authorized domains → Add domain** → `YOUR-USERNAME.github.io`

## 6. Upload the app files too
Besides `index.html`, upload `manifest.json`, `apple-touch-icon.png`, `icon-192.png`, `icon-512.png` and `icon-maskable-512.png` to the same repo folder.

**Install on iPhone:** open the link in Safari → Share → **Add to Home Screen**. It opens full-screen with the gift icon.
**Android:** Chrome menu → **Add to Home screen** / **Install app**.
Note: the home-screen app keeps its own login separate from Safari, so sign in once more inside the app.

## Done
Send her the link. She taps **Sign in with Google**, and lands on her own list. Anyone else who signs in gets told they're not on the guest list, and the database refuses them anyway.

### Troubleshooting
- **Sign-in won't open from the home-screen app** → sign in once in Safari to check it works, then try the app again; if it still won't, tell Claude the error shown under the button.
- **Sign-in popup closes with `auth/unauthorized-domain`** → step 5.
- **"Couldn't load the list (permission-denied)"** → the email in `firestore.rules` doesn't match the account (check lowercase, check you published the rules).
- **Page stays blank** → open the browser console; if the Firebase script failed to load, change `13.2.0` in the three import lines to `12.15.0`.
