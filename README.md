# Microbiology Seminar Series — 2026–2027

A living schedule for the Department of Microbiology seminar series.
Wednesdays, 12:30pm, ACLS West 4th Floor Conference Room unless otherwise indicated.

**Live at:** https://ben-tenoever.github.io/seminars

---

## How to change the schedule

Everything lives in **one block in `index.html`**. Open the file, find the block
marked `THE SCHEDULE LIVES HERE`, and edit the line you care about. There is no
build step, no data file to keep in sync, and nothing else to touch.

One line per session:

```json
{"date":"2027-02-10","speaker":"Leigh Miller, PhD","host":"Kamal Khanna","location":"","kind":"seminar"}
```

| Field | What it does |
|---|---|
| `date` | `YYYY-MM-DD`. Drives sorting, the "Next" badge, and greying out past dates. |
| `speaker` | The name, or `TBD`, or what the session is (`Departmental Retreat`). |
| `host` | Lab or PI. Leave `""` for a slot nobody has claimed. |
| `location` | Leave `""` for the default room. Anything here shows under the speaker. |
| `kind` | See below. |

### `kind` values

| Value | Shows as | Use it for |
|---|---|---|
| `seminar` | plain row | A confirmed, named speaker |
| `tbd` | amber **Needs speaker** | Date is spoken for, speaker not yet named (host optional) |
| `open` | green **Open** | No host at all — free for the taking |
| `defense` | red **Defense** | Public portion of a thesis defense |
| `special` | plain row | State of the Department, Postdocs/Students, Retreat |
| `none` | greyed row | No seminar that week |

### Common edits

**Someone takes over a slot** — change `host`, and `speaker` if known:

```json
{"date":"2027-04-14","speaker":"TBD","host":"Kamal Khanna","location":"","kind":"tbd"}
```

**A defense gets booked into a TBD slot** — change `kind` to `defense`, put the
student's name in `speaker`, and add the room and time if it is not the usual one:

```json
{"date":"2027-03-10","speaker":"Jane Doe — Thesis Defense","host":"Bo Shopsin","location":"SB 103, 2:00pm","kind":"defense"}
```

**A speaker gets confirmed** — change `kind` from `tbd` to `seminar` and replace
`TBD` with the name.

**An extra session on a non-Wednesday** — just add a line with that date. The page
sorts by whatever order the lines are in, so keep them chronological.

---

## What the page works out for itself

Nothing here needs maintaining. It recalculates every time someone loads it:

- which session is **next**, and badges it
- past dates greyed out
- how many slots still need a speaker
- how many are completely open
- the counts on every filter chip

So the page stays honest between edits — the week after a seminar happens, it
moves itself along.

---

## Publishing

Standard GitHub Pages, served from `main` at the repository root:

```
Settings → Pages → Source: Deploy from a branch → main / (root)
```

Pages takes about five minutes to rebuild after a push. If the live page looks
stale, that is the cache, not your edit — wait and reload.

## Optional

Drop a `assets/nyulh-logo.png` into the repo and it appears in the header. If the
file is absent the header silently drops it, so this is safe to skip.
