# Aubrey's Safety & Recovery Plan

Single-page site, black & pink, no build step. `index.html` + `images/`.
Everything typed into the plan saves automatically. With Firebase configured, it syncs live between every open device.

## 1. Firebase (so you both can edit live) — about 5 minutes

1. Go to https://console.firebase.google.com → **Add project** (any name, e.g. `aubrey-plan`). Analytics off is fine.
2. Left menu → **Build → Realtime Database → Create database**. Pick a US location, start in **locked mode**.
3. **Rules** tab → replace with the rules below → **Publish**:
   ```json
   {
     "rules": {
       ".read": false,
       ".write": false,
       "aubrey-plan": { ".read": true, ".write": true }
     }
   }
   ```
4. Project settings (gear icon) → **Your apps → Web app (`</>`)** → register it (no hosting needed) → copy the `firebaseConfig` object.
5. Config is already pasted into `index.html` (project `aubrey-c4c9d`). If you created the database outside the US, copy the database URL shown at the top of the Realtime Database **Data** tab into `databaseURL`.
6. Optional: set `const PASSCODE = "1234";` to put a simple passcode screen in front of the page.
   (It's a speed bump, not real security — anyone with the link who knows the code gets in.)

## 2. GitHub Pages

1. New repo (e.g. `aubrey-plan`). Upload `index.html`, `README.md`, and the whole `images/` folder.
2. Repo **Settings → Pages → Source: Deploy from a branch → main / (root) → Save**.
3. Your site is live at `https://<username>.github.io/aubrey-plan/` within a minute or two.

Any later change to `index.html` (new photos, new text) is just a commit — the saved answers live in Firebase, not in the file, so editing the page never wipes them.

## Adding photos

Drop the file in `images/` and add its path to the `PHOTOS` array in `index.html`.
The photo rows at the top of **My Why** (Aubrey / Will / son) are set directly in the `.why-block` HTML in `index.html`; their captions are editable on the page and sync.

## Status dot (top right)

- **Green** — connected to Firebase, saved.
- **Yellow** — saving.
- **Red** — offline; Firebase queues the change and syncs when back.
- **Grey "Local only"** — no Firebase config yet; saves on this device only.
