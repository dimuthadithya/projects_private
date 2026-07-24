# projects_private

A public repository used to manually list **private or client projects** that can't be open-sourced, so they still appear on [dimuthadithya.site](https://dimuthadithya.site).

The portfolio site's GitHub Actions workflow fetches `projects.json` from this repo daily and merges the entries with public GitHub repositories automatically.

---

## How to add a project

Open `projects.json` and add a new object to the array. Only these fields are required:

| Field | Type | Description |
|---|---|---|
| `id` | number | A unique ID — use `9001`, `9002`, `9003`… (increment each time) |
| `name` | string | A URL-safe slug, e.g. `"my-project-name"` |
| `description` | string | One-line description shown on the project card |
| `homepage` | string | Live demo URL (shown as the primary link) |
| `html_url` | string | GitHub repo URL — use `""` if the repo is private |
| `topics` | array | Must include `"project"` for it to appear on the portfolio. Add other tags freely |
| `languages` | object | `{ "Language": bytesCount }` — used for the language bar |
| `card_image` | string | URL to a preview image (hosted anywhere publicly accessible) |
| `updated_at` | string | ISO 8601 date — used for sorting, e.g. `"2026-07-24T00:00:00Z"` |
| `private` | boolean | Set to `true` to show a **Private** badge on the card |

---

## Example entry

```json
{
  "id": 9001,
  "name": "client-dashboard",
  "description": "Internal analytics dashboard built for a logistics client.",
  "homepage": "https://client-dashboard.vercel.app",
  "html_url": "",
  "topics": ["project", "react", "dashboard"],
  "languages": {
    "TypeScript": 92000,
    "CSS": 4100
  },
  "card_image": "https://raw.githubusercontent.com/dimuthadithya/projects_private/main/images/client-dashboard.png",
  "updated_at": "2026-07-24T00:00:00Z",
  "private": true
}
```

---

## Adding a card image

1. Add your screenshot to the `images/` folder in this repo
2. Use this URL pattern as the `card_image` value:

```
https://raw.githubusercontent.com/dimuthadithya/projects_private/main/images/YOUR-IMAGE.png
```

---

## How the sync works

```
projects.json (this repo)
        ↓  fetched daily by GitHub Actions
dimuthadithya.site → data/github-data.json → portfolio cards
```

The fetch script merges these manual entries with your public GitHub repos, deduplicating by `name`. Changes here reflect on the portfolio within 24 hours, or immediately after a manual workflow trigger.
