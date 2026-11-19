# Secret Santa

One page. Everyone joins live, the host starts the draw, everyone picks a present and sees only their own match.

## Setup (~10 min, one time)

1. **Firebase**: go to https://console.firebase.google.com, then *Add project* (Analytics off is fine).
2. **Build → Realtime Database → Create database**. Start in **test mode**.
3. Open the **Rules** tab, paste this, and publish:
   ```json
   { "rules": { "rooms": { "$room": { ".read": true, ".write": true } } } }
   ```
4. **Project settings (gear) → Your apps → Web (`</>`)**: register an app and copy the `firebaseConfig` values into the top of `index.html`. Make sure `databaseURL` is filled in.
5. **GitHub**: create a new repo, upload `index.html`, then go to **Settings → Pages → Deploy from branch → main / root**. After a minute you get `https://<you>.github.io/<repo>/`.

## Using it

- Team link: `https://<you>.github.io/<repo>/?room=xmas2026`
- Your host link: the same URL plus `&host` → `...?room=xmas2026&host`
- Everyone joins with a name and a PIN. Once 3 or more people are in, the host clicks **Start**, and each person picks a present to see who they're buying for.
- If someone reloads or switches PC, they use the same name and PIN to get back in.

## How it stays secret

Each person's result is encrypted for their browser alone and unlocked with their PIN. Even the database owner can't read who has whom. Pairs form one shuffled circle, so nobody draws themselves.

Limits: anyone with the link can join or reset the room (the Firebase config is visible in the page, which is normal for Firebase). Fine for a team, but don't post the link publicly.
