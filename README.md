# Fantasy Timeline

A single-file D&D campaign timeline, hosted for free on GitHub Pages.

## How it works

- **Everything runs in the browser.** There's no server or database — `index.html` is the whole app.
- **`data.json`** in this repo is the shared campaign data (events, tags, players, DM password hash). It's what everyone sees when they first open the site.
- **DM Mode** (the 🔒 button) unlocks editing and reveals events marked "DM Only". Set a DM password the first time you click it.
- **Players** are just names the DM adds in Settings — there's no password for players, it's a simple "Playing as…" dropdown in the header so each person's browser remembers who they are.
- **Per-event visibility**: when adding/editing an event, "Visible To" can be set to Everyone or specific players. Anyone not on the list won't see that event at all (separate from the "DM Only" secret toggle, which hides it from all players).

## Publishing changes (DM workflow)

Since GitHub Pages can't run a server, "saving" for everyone means committing an updated `data.json`:

1. As the DM, make your edits (add events, add players, set visibility) — these save to your own browser as you go.
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

- There are no real player accounts — anyone can type any player name into the dropdown. This is meant for a trusted group (your table), not public access control.
- The DM password is hashed (SHA-256) before being stored, but that hash ends up in the public `data.json` once published. Don't reuse a password you use elsewhere.
- If you want true per-player logins with server-side enforcement, that requires a real backend (e.g. Firebase/Supabase) — this setup intentionally trades that off for "just works on GitHub Pages, no accounts to manage."
