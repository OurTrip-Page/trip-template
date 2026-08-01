# Your trips

This repository is yours. Every trip page you have on OurTrip is a file in here,
and every edit — by you, by your AI agent, by anyone you invite — is a git commit.
That means version history, undo, and an audit trail come for free, and it means
you can clone this repo and walk away with everything at any time.

```
trips/<slug>/index.html   the page itself — this IS what visitors see
sources/                  raw originals: emails, PDFs, screenshots. Never published.
profile.md                what we know about how you travel
```

## The page is the document

There is no template engine, no JSON file, no schema. `trips/welcome/index.html`
is a complete HTML page, and it is byte-for-byte what gets served behind your
login. Restyle it, restructure it, throw it away and write your own — nothing in
OurTrip will fight you.

When you push — or when your agent writes to it — the file is stored exactly as
you wrote it and served from there. Nothing is derived, rewritten or stripped.

## Privacy — one page, one allowlist

There is **one copy** of each trip page and it is never public. It reaches only
the email addresses on that trip's allowlist; everyone else gets a sign-in wall.

That means the page keeps everything: confirmation numbers, door codes,
addresses, prices. A trip page without the logistics is a worse page, not a safer
one — the reason to open it on the morning of a flight is that the reference
number is right there.

Access is not written into the page. It is a list of addresses kept outside the
document, so changing who can read a trip never means editing or re-committing
one. Nothing under `sources/` is ever served.

## Conventions

`trips/welcome/index.html` is a worked example of all of them — a real-looking
trip with cards, collapsible detail rows, map links, activity suggestions and a
day-by-day plan. Delete it and write your own, or keep it as a pattern to copy.

The one convention the page itself depends on:

- **`data-start` / `data-end` on every `.card`**, as `YYYY-MM-DD`. The script at
  the bottom of the page reads them to dim what is done, highlight where you are
  now, and offer the "hide past days" toggle. A card without them simply has no
  state — nothing breaks, you just lose the time-awareness for that card.

The same script also filters the page as you type in the "Find in this trip" box
— useful on a phone, where the browser's own find is buried in a share menu. It
matches on card text, so it costs you nothing to keep and nothing to delete. Like
the rest of the script it is *your* JavaScript, sitting in your file: OurTrip
serves the bytes you wrote and never injects anything into them.

Everything else is yours: JSON-LD if you want rich search results, any `data-*`
attribute of your own, or none of it. We will not touch what we do not read.

The full set of conventions an agent follows when editing these pages — document
anatomy, the class vocabulary, and the
planning workflow — lives in the authoring guide, which is published to your
agent with every prompt. You never have to read it; it is there so the agent
does not have to guess.

## Working with an agent

Connect OurTrip to Claude (or any MCP-capable agent) and it can read and write
these pages directly: `list_trips`, `create_trip`, `get_trip`, `put_trip`,
`store_source`. It reads your email with its own connector, files the originals
under `sources/`, and edits the page. OurTrip never sees your mailbox.
