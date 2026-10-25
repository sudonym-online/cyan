# Cyan

A desktop-style web app with a game launcher, an AI chat, and a public chat room, each running in its own window. Built with Svelte and packaged as a single HTML file.

**Demo video:** [paste link]

[Screenshot or GIF: paste here]

This is version 3 of a personal project I've worked on since December 2025.

## What it does

- **Windows:** each app opens in a window that you can drag, minimize, and close. The interface has a dark, terminal-style look.
- **Cyanide (game launcher):** a launcher for browser games listed in `games.json`. You can search, mark favorites, switch between grid and list views, and play in fullscreen. Each game can show a status: working, bugged, or broken. The list starts empty; see [Add a game](#add-a-game).
- **Fluoride (AI chat):** chat with Google Gemini models through Firebase AI Logic. Replies stream in and render Markdown and math.
- **Sulfur (chat):** a public chat room that runs on Nostr relays, with no server of my own. You pick a username, the last 100 messages load when you open it, and new messages appear in real time.
- **Feedback:** a form in the sidebar that sends bug reports and feature requests as messages to public Nostr relays.

## Tech stack

- Svelte 5, Vite, JavaScript, and TypeScript
- `vite-plugin-singlefile` (builds the whole app into one HTML file)
- Firebase AI Logic (Gemini)
- `nostr-tools` (chat and feedback messages)
- `markdown-it` and KaTeX (chat formatting)

## Run it locally

You need Node.js 20.19 or later (Vite 7 requires it).

```sh
npm install
npm run dev
```

Open the address that Vite prints. To build the single-file version, run `npm run build`; the result is `dist/index.html`.

`src/firebase.ts` points to my Firebase project. To use your own, replace that config with your project's settings.

## Add a game

Add an entry to `games.json`:

```json
{
  "games": [
    {
      "title": "My Game",
      "imageSrc": "https://example.com/cover.png",
      "genre": "Puzzle",
      "type": "HTML",
      "link": "https://example.com/my-game/index.html",
      "description": "One line about the game.",
      "status": ["Working", "No known issues."]
    }
  ]
}
```

Only add games that you made or that allow sharing.

## What I learned

- **Building a window manager.** Opening, focusing, dragging, and minimizing several app windows meant keeping one shared list of open windows in a Svelte store.
- **Real-time chat without my own server.** Sulfur and the feedback form send signed messages to public Nostr relays and subscribe to new ones, so the app needs no backend.
- **Shipping as one file.** Bundling every script, style, and asset into a single HTML file makes the app easy to share and open anywhere.

## What I would improve next

- Move the Firebase settings out of the source code and into environment variables.
- Add a few of my own games to the launcher.
