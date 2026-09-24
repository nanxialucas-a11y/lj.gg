# lj.gg

a small personal corner of the internet, some games, tools, and a few experiments i built. previously called "the hub". the name rebrand is pretty self-explanatory.

**lj.gg live at:** [lucas.nanpro.com.au](https://lucas.nanpro.com.au)

---

## what's here

| section | path | what it is |
|---|---|---|
| **unblocked games** | `/games/` | a growing library of ad-free browser games. see below for how i add one using HTML arrays. |
| **ljproxy v2** | hosted separately at `ljproxy.lucas.nanpro.com.au` | a lightweight browsing proxy built from scratch on cloudflare workers. handles most sites but heavy js sites (TikTok, YouTube) still break. |
| **ljVM** | `/ljvm.html` | a real browser running in the cloud (via Hyperbeam), embedded straight into the page. |
| **apps & websites** | `/apps-websites/` | a library card catalog styled bookmarks page for and apps and websites i actually use, split into an apps/websites switcher with category filters. |
| **anime** | `/anime/` | was going to be a free tv section, but due to implementation complications it's stopped for now. |

## tech stack

- **static HTML/CSS/JS** — no framework, no build step. every page is a single self-contained file.
- **simple hosting and deployment methods** all website files are edited locally and then pushed to github using terminal. cloudflare then automatically detects this updated brand and rebuilds and redeploys the new version, which then syncs to a custom domain.
- **fonts** [Lora](https://fonts.google.com/specimen/Lora) (serif, headings) + [Inter](https://fonts.google.com/specimen/Inter) (sans, body).
- **design system** warm cream/olive palette (`#f2ecd6` background, `#47542f` accent).

## Project structure

```
lj.gg/
├── index.html             entrance page (bloom animation → home.html)
├── home.html              main page / index of everything
├── ljvm.html              embeds Hyperbeam VM session
├── music-player.css       site-wide stylesheet (name's a leftover from an earlier version and i cant be pissed to update everything)
├── favicon.ico            site favicon
├── games/
│   ├── index.html         games list (data-driven, see below)
│   └── <game-name>/       one folder per game, each self-contained
├── apps-websites/
│   └── index.html         the "catalog" page
├── anime/                 empty for now
└── images/
    └── games/             one thumbnail per game
```

## adding a new game

open `games/index.html`, find the `const games = [ ... ]` array near the top of the `<script>` block. copy an existing entry, paste it anywhere in the array, and fill in the fields:

```js
{
    img: "/images/games/yourgame.png",
    alt: "your game",
    title: "your game",
    desc: "a short description",
    link: "/games/yourgame/"
    // add status: "down" if it's currently broken — shows a red badge instead
},
```

order in the array = order on the page. no other files need to change.

## adding a new catalog entry (apps & websites)

same pattern as above, in `apps-websites/index.html`'s `const entries = [ ... ]` array:

```js
{
    title: "name",
    url: "https://example.com",
    desc: "a line or two about whatever it does",
    category: "whatever",   // any word. new filter chips generate themselves automatically
    type: "website"         // or "app". this controls which switcher tab it shows under
},
```

favicons are pulled automatically from each entry's own domain, no icon work is needed.

## License

© 2026 Lucas Jiang. Contact: nanxia.lucas@gmail.com. All rights reserved. No part of this site or its content may be reproduced, copied, modified, or adapted without prior written consent.
