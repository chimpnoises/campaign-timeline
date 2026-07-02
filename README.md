# Fantasy Timeline

A single-file D&D campaign timeline, hosted for free on GitHub Pages.

## How it works

- **Everything runs in the browser.** There's no server or database — `index.html` is the whole app.
- **`data.json`** in this repo is the shared campaign data (events, tags, players, DM password hash). It's what everyone sees when they first open the site.
- **The header** is icon-only: a tag icon toggles the tag filter row, a quill icon opens Add Event, and the dragon icon opens the menu (search, "Playing as…", and DM Mode).
- **DM Mode** (in the dragon menu) unlocks editing and reveals events marked "DM Only". Set a DM password the first time you click it. Settings and all data export/publish controls only appear once DM Mode is unlocked.
- **Players** are added by the DM in Settings (only reachable in DM Mode). When you add a player you're immediately prompted to set their password — since you set it yourself (rather than the player signing up), do this together in person or share the password with them directly. Click the 🔑 icon on a player's chip later to change it.
- **Logging in as a player**: pick a name from the "Playing as…" dropdown in the dragon menu, enter that player's password, and the timeline filters to what they can see.
- **Logins persist on that browser** — once you or a player successfully logs in (DM or player), the site remembers it on reload, so nobody has to re-enter a password every visit. Lock DM Mode (or pick the blank "Playing as…" option) to log out.
- **"View as Player"** (in the dragon menu, once DM Mode is unlocked) lets the DM instantly preview the timeline as any player — or as an anonymous visitor — without needing that player's password. While previewing, Settings is hidden too, so it's a true preview of what they'd see. Toggle it off to return to full DM view.
- **Per-event visibility**: when adding/editing an event, "Visible To" can be set to Everyone or specific players. Anyone not authenticated as one of the listed players won't see that event at all (separate from the "DM Only" secret toggle, which hides it from all players including unauthenticated visitors).

## Publishing changes (DM workflow)

Since GitHub Pages can't run a server, "saving" for everyone means committing an updated `data.json`:

1. As the DM, make your edits (add events, add players and set their passwords, set visibility) — these save to your own browser as you go.
2. Open **Settings → ⬇ Download data.json**.
3. Replace `data.json` in this repo with the downloaded file.
4. Commit and push. GitHub Pages will redeploy automatically (usually within a minute).
5. Players click **Settings → ↻ Reload Published Data** to pick up the update (this discards any of their own unpublished local state, but players never write data, so that's safe).

## Hosting it on GitHub Pages

1. Push this folder's contents (`index.html`, `data.json`) to a GitHub repo.
2. In the repo, go to **Settings → Pages**.
3. Under "Build and deployment", set Source to **Deploy from a branch**, branch `main`, folder `/ (root)`.
4. Save. Your site will be live at `https://<username>.github.io/<repo-name>/` within a minute or two.

## Security notes

- Player and DM passwords are hashed (SHA-256) before being stored, but those hashes end up in the public `data.json` once published — anyone can download the repo and attempt to crack a weak password offline. Don't reuse passwords used elsewhere, and pick something a stranger couldn't guess.
- This is client-side gating, not server-enforced access control: the filtering happens in each visitor's browser. It stops casual snooping by someone without a password, but a technically determined person could inspect the page's JavaScript/data to find restricted content. Fine for a trusted home group; not a substitute for a real backend if you ever need actual security guarantees (that would mean Firebase/Supabase or similar).
- Logins persist on the browser they were entered on (no expiry). Anyone with physical/unlocked access to that browser has whatever access was last logged into it — lock DM Mode or switch back to "— Playing as… —" when stepping away from a shared device.
- Anyone (not just the DM) can still click the quill icon to add an event — those edits just never leave their own browser since only the DM can push to the GitHub repo.
