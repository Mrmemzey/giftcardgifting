# Keycard

Send a Steam key to a friend as a sealed pack they swipe to rip open. Inside are your note and the key on a card with the game's art. It's a static site for GitHub Pages, plus one small free Cloudflare Worker for game search and art.

- **Create:** fill in the names, start typing a game and pick it from the list (this adds its art), paste the key, write a message, then copy the link.
- **Receive:** your friend opens the link and swipes across the top of the pack to rip it open, with a mouse or a finger. On a keyboard they can press Enter, and there's an "Open without swiping" button. Tapping the card copies the key. **Redeem on Steam** opens `store.steampowered.com/account/registerkey` with the key filled in.

The gift is packed into the link's `#` part, which browsers never send to any server. Anyone who has the link can read the key, so only send it to the person it's for.

## Files

| File | What it is |
|---|---|
| `index.html` | The whole site |
| `config.js` | Where you paste your worker's URL |
| `worker/` | The Cloudflare Worker for game search and art |

## 1. Deploy the worker (game search + art)

Steam and SteamGridDB don't let a web page call them directly, and a SteamGridDB API key put in a public page would be visible to anyone. The worker sits in between. Cloudflare's free plan covers it.

1. Get a SteamGridDB API key: sign in at steamgriddb.com, then go to **Preferences → API**. This step is optional. Without a key, the worker uses Steam's own store art.
2. Deploy it, from the `worker` folder:

   ```bash
   npx wrangler login
   ```

   ```bash
   npx wrangler deploy
   ```

   ```bash
   npx wrangler secret put SGDB_KEY
   ```

   (Paste the key when asked.) Wrangler prints the worker URL, for example `https://keycard-api.yourname.workers.dev`.
3. In `worker/wrangler.toml`, set `ALLOWED_ORIGIN` to your Pages origin, such as `https://yourname.github.io`, so other sites can't use your worker. Then run `npx wrangler deploy` again.
4. Paste the worker URL into `config.js`.

If `config.js` is left empty the site still works. The Game field becomes plain text and cards have no art.

## 2. Deploy the site on GitHub Pages

1. Push `index.html`, `config.js` and this README to a repository's `main` branch. The `worker` folder can go in the repository too; Pages ignores it.
2. Go to **Settings → Pages**, set **Source** to *Deploy from a branch*, pick `main` / `(root)`, and save.
3. After a minute the site is at `https://<your-username>.github.io/<repo>/`.
