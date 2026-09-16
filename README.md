# Tanishk Universe Portfolio

🌌 **Live Portfolio:** (https://tanishk-universe.netlify.app/)

An interactive 3D universe-themed portfolio showcasing my projects, skills, education, experience, and achievements.


# Tanishk Kekan — Personal Universe

An interactive 3D "personal universe" portfolio built with Three.js. The site
is a single self-contained HTML file — no build step, no dependencies to
install, no bundler. Open it in a browser and it runs.

**Live artifact:** https://claude.ai/artifact/2xA5AtzJdTBw5knyPT1wfA
(private until you publish/share it — see [Sharing the artifact](#sharing-the-claude-artifact) below)

---

## What's in it

A central star with ten destinations orbiting around it, each mapped to a
section of the portfolio:

| Body | Section |
|---|---|
| ☀ Central star | Home |
| 🪐 About planet | Bio, location, education summary |
| 🪐 Projects hub (+ 6 moons) | Six projects, one per moon |
| ✦ Skills constellation | Four skill clusters connected by glowing lines |
| 🪐 Education planet | Degree + school history, shown as a timeline |
| 🪐 Experience planet | AI/ML internship, milestones orbit as nodes |
| ☄ Asteroid belt | Four achievements as collectible rocks |
| 🌌 GitHub galaxy | Spiral galaxy linking to your GitHub profile |
| 🚀 Resume spaceship | Launches on click, opens resume panel |
| 📡 Contact satellite | Contact form + email/LinkedIn/GitHub links |

Everything — planet surfaces, rings, nebulae, the sun, the starfield — is
generated procedurally at load time from noise functions. There are no image
files to download, so nothing can go missing or fail to load.

**Also included:**
- A cinematic loading sequence, hero name animation, and camera fly-throughs
- A "Text view" toggle — a fully readable, non-3D version of every section,
  for accessibility and for anyone whose browser can't run WebGL
- `prefers-reduced-motion` support (shortens/removes animation automatically)
- A print-to-PDF resume generated from the same data (no separate file to keep in sync)
- Two easter eggs: a comet with developer quotes, and the Konami code

---

## Running it locally

No installation needed:

```bash
# just open it
open tanishk-kekan-universe.html          # macOS
start tanishk-kekan-universe.html         # Windows
xdg-open tanishk-kekan-universe.html      # Linux
```

Or serve it (recommended if you plan to edit and reload often):

```bash
python3 -m http.server 8000
# then visit http://localhost:8000/tanishk-kekan-universe.html
```

---

## Before you deploy: three placeholders to fill in

Open the file and find the `CONTACT` block near the top of the `<script>`:

```js
const CONTACT = {
  email:    "",   // e.g. "tanishk@example.com"
  linkedin: "",   // e.g. "https://linkedin.com/in/tanishkkekan"
  resumeURL:""    // e.g. "./Tanishk-Kekan-Resume.pdf"
};
```

Until these are filled in, the site is honest about it rather than showing
fake contact info: the Contact panel shows a labelled placeholder chip
instead of an email address, and the Resume panel offers "Print resume"
(a real PDF built from the on-page data) instead of a broken download link.

Each project in the `PROJECTS` array also has a `repo` field set to `null`:

```js
{ id:"chatgpt-clone", name:"ChatGPT Clone", ... repo:null, ... }
```

Set it to a real GitHub URL to make that project's "View code" button live.
Until then, the button opens your GitHub profile instead of a broken link.

---

## Editing content

All portfolio content lives in plain data objects near the top of the script
— nothing to hunt through the 3D/rendering code:

- `PROFILE` — name, role, location, intro paragraph
- `PROJECTS` — array of project objects (add one to add a new orbiting moon)
- `SKILLS` — grouped skill list with levels and descriptions
- `EDUCATION` — school history
- `EXPERIENCE` — internship/role history with milestone points
- `ACHIEVEMENTS` — asteroid-belt items
- `QUOTES` — comet easter-egg quotes
- `SECTIONS` — nav bar labels/order

Adding a seventh project, for example, just means adding one more object to
the `PROJECTS` array — a new moon appears in orbit automatically, with its
own panel, features list, and GitHub button.

---

## Deploying to a public URL

The file needs no build step, so any static host works.

**Netlify Drop (fastest, no account needed)**
1. Rename the file to `index.html`
2. Go to [app.netlify.com/drop](https://app.netlify.com/drop) and drag it in
3. You get a live URL immediately (e.g. `your-site.netlify.app`)

**Vercel**
1. Go to [vercel.com](https://vercel.com), sign in with GitHub
2. "Add New Project" → "Upload", drop in `index.html`

**GitHub Pages**
1. Create a repo on your GitHub account, upload `index.html`
2. Settings → Pages → set source to your main branch, folder `/root`
3. Live at `Tanishk-commit.github.io/<repo-name>` within a couple of minutes

Any of these also let you attach a custom domain later from their dashboard.

### Sharing the Claude artifact

The link above is private until you publish it from within Claude:
open the artifact → **⋯ menu → Share** (or **Publish**, depending on your
plan) → confirm. Public link-sharing is available on Free/Pro/Max plans;
Team/Enterprise accounts can only share within their organization, not to
the public web — for a public link on those plans, use one of the hosts
above instead.

---

## Accessibility

- Full keyboard navigation; all interactive elements are focusable
- Visible focus outlines
- `prefers-reduced-motion` significantly shortens or removes animation
- WebGL-unavailable fallback: the site automatically shows the full text
  view instead of a blank canvas
- The manual "Text view" toggle in the nav bar gives the same fallback
  on demand, for anyone who prefers reading over the 3D scene

---

## Tech notes

Built in vanilla JavaScript + Three.js (r128, loaded from cdnjs) rather than
React/R3F, because it needed to run as a single hostable HTML file. The data
layer (`PROFILE`, `PROJECTS`, `SKILLS`, etc.) is deliberately separated from
the scene-building and UI code, so porting this into a React + Vite + R3F
project later is mostly a matter of moving those objects into their own
`.ts` files and turning each `build...()` function into a component.
