# Keycard

Send a Steam key to a friend as a card with a message. It's one static page with no backend, so it runs on GitHub Pages.

- **Create:** open the site, fill in the names, an optional game title, the key and a message, then copy the link.
- **Receive:** your friend opens the link, sees your message and the key on a card, taps the card to copy the key, or presses **Redeem on Steam**. That opens `store.steampowered.com/account/registerkey` with the key filled in.

The gift is packed into the link's `#` part, which browsers never send to any server. Anyone who has the link can read the key, so only send it to the person it's for.

## Deploy on GitHub Pages

1. Create a repository and push `index.html` (and this README) to the `main` branch.
2. Go to the repository's **Settings → Pages**, set **Source** to *Deploy from a branch*, pick `main` / `(root)`, and save.
3. After a minute the site is at `https://<your-username>.github.io/<repo>/`.
