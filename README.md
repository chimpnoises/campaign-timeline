# Fantasy Timeline

A single-file D&D campaign timeline, hosted for free on GitHub Pages.

## How it works

- **Everything runs in the browser.** There's no server or database — `index.html` is the whole app.
- **`data.json`** in this repo is the shared campaign data (events, tags, players, DM password hash). It's what everyone sees when they first open the site.
- **DM Mode** (the 🔒 button) unlocks editing and reveals events marked "DM Only". Set a DM password the first time you click it.
- **Players** are added by the DM in Settings. When you add a player you're immediately prompted to set their password — since you set it yourself (rather than the player signing up), do this together in person or share the password with them directly. Click the 🔑 icon on a player's chip later to change it.
- **Logging in as a player**: pick a name from the "Playing as…" dropdown in the header, enter that player's password, and the timeline filters to what they can see. This resets on every page reload — like DM Mode, there's no persistent "stay logged in."
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
- Anyone (not just the DM) can still click "+ Add Event" — those edits just never leave their own browser since only the DM can push to the GitHub repo.
