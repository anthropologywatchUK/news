# Anthropology in the news — how the feed is updated

The page (`news.html`) is a fixed template. Everything it shows comes from `news.json`, so keeping the page current means adding items to that one file. Both files sit side by side wherever the site is hosted.

## The data file

Each story is one object in `items`:

| Field | Meaning |
|---|---|
| `id` | Unique, readable key: `YYYY-MM-DD-short-slug` |
| `date` | Date of the coverage or event, `YYYY-MM-DD` |
| `date_precision` | `day`, `month` or `year` (use `year` with `YYYY-01-01` when only the year is known) |
| `stream` | `public` (Anthropology in public) or `profession` (From the profession) |
| `title` | Headline in our own words, under 90 characters |
| `summary` | 30–60 words in our own words, saying who and why it matters for anthropology |
| `outlet` | Where it appeared (BBC, The Guardian, RAI, a department) |
| `url` | Link to the original source; prefer the article itself over a department round-up |
| `status` | `pending` (drafted, not shown) or `published` (live) |
| `added` | Date the item was added to the file |
| `note` | Optional, internal only; not shown on the page |

Update the top-level `updated` date whenever the file changes.

## Approving items

New items arrive as `pending` and stay off the page. To approve one, change its `status` to `published`. To reject one, delete it. Nothing goes live without that edit.

## The weekly run

Default cadence: every Friday morning, UK time. Each run follows the instructions below and only adds `pending` items.

> **Weekly update: Anthropology in the news**
>
> 1. Read the current `news.json`. Note every `url` and `id` already present.
> 2. Search the web for coverage from the last 7 days in two streams:
>    - **Anthropology in public:** UK-based anthropologists quoted, interviewed or writing in mainstream media (BBC, Guardian, Times, Telegraph, Independent, FT, The Conversation UK, New Scientist, national and regional press, radio and podcasts), and anthropological research that made the news.
>    - **From the profession:** prizes and medals (RAI, ASA, British Academy), named lectures, fellowships, major book launches, new podcasts, manifestos and public events from UK anthropology departments, the ASA, the RAI and Discover Anthropology.
> 3. Leave out stories about cuts, closures and redundancies; those belong in the Programme Tracker.
> 4. Skip anything whose URL is already in the file, anything not traceable to a public source, and anything outside the last 7 days.
> 5. For each new story, add an item with `status: "pending"` and today's date in `added`. Write the title and summary in our own words; never copy sentences from the source, and use at most one short quotation of under 15 words. Link to the original article, not an aggregator.
> 6. Update `updated`, keep the file valid JSON, and report a short list of the items added (title, outlet, link) so they can be reviewed.

## Hosting (still to decide)

Any of these work without changing the page:

- **Alongside the tracker on GitHub Pages:** add `news.html` and `news.json` to the tracker repository and link the "In the News" tab. A scheduled run can then commit new pending items directly.
- **A shared spreadsheet or Claude-hosted page:** keep the same fields as columns; the page would need a small change to read from that source instead of `news.json`.

Opening `news.html` straight from a computer will not load the feed, because browsers block reading `news.json` from local files. Serve the folder over the web, or run `python3 -m http.server` in the folder and visit `http://localhost:8000/news.html`.
