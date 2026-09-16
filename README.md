# Innovien Games Draft Room — Vercel Deploy

Self-contained static HTML draft board, deployed to Vercel via GitHub. Same pattern as
the executive dashboard deploy, one folder, three files, no build step.

Why this exists: the claude.ai version of the board needs every screen to be signed in
to an Innovien account. This version needs nothing. It opens on any browser, on any
machine, with no login. That matters on a conference room PC.

## READ THIS BEFORE YOU SHARE THE URL

**Every card and every name is in the page source.** Anyone with the link can press
Ctrl+U and read the whole key before the draft starts. Vercel URLs are not secret,
they are just unlisted.

For draft night that is fine if you treat the URL as yours: put it on the room PC,
do not post it in Teams, do not email it round. The names come out that evening anyway.

If the URL does need to go wider, turn on Vercel's Deployment Protection first
(Project → Settings → Deployment Protection). It is a paid feature on Vercel's
current plans, so check what your account has before relying on it.

## One-time setup (first deploy)

### Step 1 — Create a private GitHub repo

1. Go to [github.com](https://github.com)
2. Click "+" top right → "New repository"
3. Name it `innovien-games-draft`
4. Set visibility to **Private**
5. Skip the README/license/.gitignore options
6. Click "Create repository"

### Step 2 — Upload the files

On the new repo's empty page, click "uploading an existing file" and drag in all three
files from this folder:

- `index.html`
- `vercel.json`
- `README.md`

Click "Commit changes" at the bottom.

### Step 3 — Connect Vercel

1. Go to [vercel.com](https://vercel.com), sign in with GitHub
2. "Add New..." → "Project"
3. Click "Import" next to `innovien-games-draft`
4. Vercel auto-detects a static site. **Change nothing.** Click "Deploy"
5. About 30 seconds later you get a URL like `innovien-games-draft.vercel.app`

## The broadcast open

`intro.html` deploys alongside the board and lives at `<your-url>/intro`. It is a
full-screen open of about **1 minute 45**: conference reveal, the five schools in team colours, the format, a countdown, then it holds on a title card so you can talk
over it while people settle.

It has **no audio**. Start a track before you hit play.

No captain names appear anywhere in it, you announce those as the board opens.
Every content slide from the conference reveal onward holds for **10 seconds**, with a thin progress
line along the bottom. You are not stuck with that pace: **Space** or **right arrow**
moves on early, **left arrow** goes back.

Keys: **F** full screen, **R** replay, **S** skip to the end card, **Esc** to leave
full screen. Open `/intro` in one tab and the board in another, run the open, then
switch tabs.

## Running the draft on it

1. Open the URL on the conference room PC, full screen (F11)
2. Turn on **Commissioner** (top right) so you get the controls
3. Turn on **Presenting** so the Roster and Cards tabs stop showing names
4. Click **TV** in the board bar to size the tiles for the room
5. **Setup → Reset draft** as the last thing before the room fills
6. Share the browser window over Teams, not the whole desktop

**If a captain is missing**, hit **Random pick** in the top strip when their team is on the
clock. It draws a random available card, opens it the same way, and badges the card and the
reveal as Random so the room can see nobody chose it. Nothing is automatic, it only fires
when you press it.

A captain calls a number, you click that tile, the full card opens, you read it out,
**Reveal the pick** drops the name in the team colour, **Next pick** returns to the wall.

## What is different from the claude.ai version

- **No login.** Anyone with the link opens it.
- **No live sync.** The draft state lives in that one browser, in local storage. Every
  screen that opens the URL runs its own independent board. This is the right trade for
  one operator screen sharing, and the wrong one if you ever want a second live screen.
- **Picks survive a refresh or a crash** on the same browser, same machine. They do not
  travel to another device.
- **Download CSV** falls back to copying the CSV to the clipboard.

## Updating the roster

When responses change and Claude rebuilds the board:

1. The new `index.html` lands in this folder
2. On GitHub, open the `innovien-games-draft` repo
3. Drag the new `index.html` onto the page, commit the change
4. Vercel redeploys within about 60 seconds, same URL

The cache header is set to revalidate on every load, so a plain refresh picks up the
new version. No hard refresh needed.

## Notes

- **Fonts** load from Google Fonts. If Innovien's network blocks that, the board still
  works, it just falls back to a system font. Nothing breaks.
- **Incognito.** If you run it in a private window, closing the window wipes the saved
  picks. Fine before the draft, not fine mid-draft. Use a normal window on the night,
  or finish in one sitting.
- **Paper backup.** The Cards tab with Commissioner on prints every card with the name
  at the bottom. Print it before the day.
