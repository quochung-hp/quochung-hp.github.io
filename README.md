# Academic website — Nguyen Quoc Hung

A five-page static site. No build step, no dependencies, no software to install.
Open `index.html` in a browser to see it exactly as visitors will.

```
Website/
├── index.html              Home — bio, fields, current work, profile links
├── research.html           Working papers, articles, chapters, data & code
├── teaching.html           Courses, syllabi, seminar
├── cv.html                 Embedded CV preview + download, summary tables
├── contact.html            Address, office hours, admissions pointer
├── assets/
│   ├── style.css           All styling for every page
│   └── photo.jpg           ← add your portrait here (not yet present)
├── NguyenQH_CV_Web.pdf     PUBLIC CV — no phone, no email. Linked from the site.
└── NguyenQH_CV_092026.pdf  PRIVATE master (has phone + email). Never publish it.
```

> Move `NguyenQH_CV_092026.pdf` somewhere outside this folder when convenient —
> see the warning in §5. Everything else here is meant to be public.

---

## 1. What to fill in

Everything below is already written except the links. Search the HTML files for
`href="#"` — every one is a placeholder waiting for a URL.

| Where | What's needed |
|---|---|
| `index.html` | Google Scholar, RePEc/IDEAS, SSRN, ORCID URLs |
| `index.html`, `research.html` | Drive links for the three working papers |
| `research.html` | DOI / publisher links for the eight journal articles |
| `teaching.html` | Your real course names, codes, terms, and Drive links |
| `contact.html` | Office building and room, office hours |
| — | Your phone number and email are deliberately **not** on the site (see §6) |
| `assets/photo.jpg` | A portrait, roughly 600×740 px |

The photo is optional — if the file is missing, the site hides the image slot
cleanly rather than showing a broken icon.

---

## 2. Linking files from Google Drive

This is the part that makes the site maintainable: the PDFs live in Drive, and
the site only points at them. **Replace a syllabus in Drive and the site is
instantly current — you never re-upload the site.**

### Set up the folders once

In Google Drive, create `Academic Website Materials` containing:

- `Research Papers`
- `Teaching Materials`
- `CV`

Right-click each folder → **Share** → under *General access* choose
**Anyone with the link** → **Viewer**. Files added to a shared folder inherit
that permission, so you only do this once.

> Set it on the **folder**, not on each file. This is the single most common
> mistake — a visitor clicking a paper and hitting "You need access" is worse
> than no link at all.

### Turn a share link into a website link

Drive gives you a link like:

```
https://drive.google.com/file/d/1AbC2dEfGhIjK3LmN4oPqRsTuV5wXyZ/view?usp=sharing
                               └──────────── the FILE ID ────────────┘
```

Take the file ID and use whichever form you want:

| Purpose | URL to paste |
|---|---|
| Opens in Drive's viewer | `https://drive.google.com/file/d/FILE_ID/view` |
| Downloads immediately | `https://drive.google.com/uc?export=download&id=FILE_ID` |
| Embeds in the page | `https://drive.google.com/file/d/FILE_ID/preview` |

For the "Download PDF" buttons, the **download** form is the right one. Paste it
between the quotes:

```html
<a class="btn" href="https://drive.google.com/uc?export=download&id=1AbC2...">Download PDF</a>
```

### The two CV files

`NguyenQH_CV_Web.pdf` is the one the site links and embeds. It has no phone
number and no email address. `NguyenQH_CV_092026.pdf` is your original and is
linked from nowhere — keep it for job applications, grant forms and anything
else where the full contact block belongs.

If you regenerate the web CV later, keep the same filename and the site picks it
up with no edits. If you'd rather serve it from Drive so updates are automatic,
replace the `<object>` block in `cv.html` with:

```html
<iframe class="embed" src="https://drive.google.com/file/d/FILE_ID/preview"
        title="Curriculum vitae" allow="autoplay"></iframe>
```

---

## 3. Adding a new paper

Copy an existing block in `research.html` and edit the text. The structure:

```html
<li class="pub">
  <span class="pub__title">Title of the paper</span>
  <p class="pub__meta">Nguyen, Q.H. (2027). <em>Journal Name</em>, 12(3), 100&ndash;120.</p>
  <p class="pub__abstract">Optional two-sentence plain-language summary.</p>
  <div class="pub__links">
    <a class="btn" href="URL">Download PDF</a>
  </div>
</li>
```

Remember to also update the "Current work" list on `index.html` when a working
paper becomes published.

---

## 4. Viewing the site on your own computer

Before anything is online, you can see the finished site exactly as visitors
will:

**Double-click `index.html`.** It opens in your default browser. Click the
navigation — Home, Research, Teaching, CV, Contact — and everything works.

There is no server to start and nothing to install. These are ordinary files;
your browser reads them directly. The address bar will show something like
`file:///C:/Users/quoch/Documents/Website/index.html` instead of a web address,
which is normal and is the only visible difference.

Two small things behave differently offline than they will online:

- The CV preview on the CV page may not display inline in some browsers when
  opened as a local file. The Download button still works, and it displays
  correctly once published.
- Nothing else. Links, layout and dark mode all work locally.

Edit any `.html` file, save it, then press **F5** in the browser to see the
change. That is the whole editing loop.

---

## 5. Publishing on GitHub Pages

You have a GitHub account, so this is your route. It is free, permanent, and
supports a custom domain later. Two ways to do it: with `git` (§5b), or entirely in the browser with no command line at all (§5a).

**One idea to get straight first:** a GitHub *repository* ("repo") is just a
folder that lives on GitHub's servers. GitHub Pages is a switch that says "serve
this folder as a website." That is the entire concept.

### Step 1 — Make the repository

1. Sign in at **github.com**.
2. Top right, click **+** → **New repository**.
3. **Repository name:** type `yourusername.github.io`, replacing
   `yourusername` with your actual GitHub username, exactly as it is spelled,
   in lowercase. If your username is `qhnguyen`, the name is
   `qhnguyen.github.io`.
   *This exact name is what gives you the short address
   `https://qhnguyen.github.io`. Any other name works too, but then the site
   sits at `https://qhnguyen.github.io/reponame/`.*
4. Set it to **Public**. (Pages needs this on a free account. Only the website
   files are public — nothing else on your account is affected.)
5. Leave every checkbox unticked. Do **not** add a README — you already have one.
6. Click **Create repository**.

### Step 2 — Upload the files

> ### ⚠ Read this before you upload
>
> **Anything you put in the repo is downloadable by anyone**, whether or not a
> page links to it. A file is public the moment it is in a public repo.
>
> That means `NguyenQH_CV_092026.pdf` — your private master, which still
> contains your phone number and email — **must not be uploaded**. Nothing on
> the site links to it, but that is not protection: the URL
> `https://yourusername.github.io/NguyenQH_CV_092026.pdf` would work for anyone
> who guessed it, and search engines find unlinked PDFs routinely.
>
> The safest fix is to move that file out of the `Website` folder altogether —
> say to `C:\Users\quoch\Documents\CV\` — so it cannot be swept up by a
> Ctrl+A. Then you never have to remember this rule again. Do that now if you
> can.

1. On the new empty repo page, click the link **uploading an existing file**
   (in the line "…or upload an existing file"). If you don't see it, go to
   **Add file** → **Upload files**.
2. Open `C:\Users\quoch\Documents\Website` in File Explorer.
3. Select everything *inside* it **except `NguyenQH_CV_092026.pdf`**, and drag
   the selection onto the GitHub page. (Ctrl+A to select all, then Ctrl+click
   that one file to deselect it. If you already moved it out, plain Ctrl+A is
   fine.)

   > Drag the **contents**, not the `Website` folder itself. If you drag the
   > folder, your site ends up at `.../Website/index.html` and the front page
   > will be blank. `index.html` must sit at the top level of the repo.

   The `assets` folder comes along with its files inside it; that is correct and
   expected. `README.md` and `GOOGLE-SITES-GUIDE.md` are harmless to upload —
   they contain nothing private — but you can leave them out if you prefer.
4. Wait for every file to finish uploading. The CV PDF is the slow one.
5. Scroll down, click the green **Commit changes**.
6. **Check:** the repo file list should show `NguyenQH_CV_Web.pdf` and *not*
   `NguyenQH_CV_092026.pdf`. If the wrong one is there, click it → the **⋯**
   menu → **Delete file** → **Commit changes**, and see the note below.

> If a private file ever does get committed, deleting it removes it from the
> live site immediately, but it stays visible in the repo's history. For a CV
> with a phone number that is a minor exposure and deleting the file is enough.
> To erase it completely, delete the whole repository (Settings → bottom of the
> page → Delete this repository) and start again — which is cheap to do, since
> re-uploading takes two minutes.

"Commit" just means "save this to the repo." You will see your files listed on
the repo page afterwards.

### Step 3 — Turn on Pages

1. In the repo, click **Settings** (the tab along the top, with the gear icon —
   not your account settings).
2. In the left sidebar, click **Pages**.
3. Under **Build and deployment → Source**, choose **Deploy from a branch**.
4. Under **Branch**, choose **main**, leave the folder as **/ (root)**, and click
   **Save**.
5. Wait one to two minutes, then reload that page. A green banner appears:
   *"Your site is live at https://yourusername.github.io/"*.

Click it. That is your website, publicly reachable from anywhere.

> If you get a 404 page: wait another two minutes and reload — the first build
> genuinely takes a few minutes. If it persists, check that `index.html` is
> visible on the repo's front page. If it is inside a `Website` folder there,
> that is the drag mistake from Step 2; delete the folder and re-upload the
> contents.

### Step 4 — Updating it later

Any time you edit a file on your computer:

1. Go to your repo on github.com.
2. **Add file → Upload files**, drag in the changed file(s), **Commit changes**.
3. Uploading a file with the same name replaces the old one. The live site
   updates within a minute or two.

For a one-line text fix you can skip your computer entirely: click the file in
the repo, click the pencil icon, edit, **Commit changes**.

If you find yourself doing this often, install **GitHub Desktop**
(desktop.github.com) — a normal Windows app that syncs the folder to GitHub with
one button, no commands.

### A custom domain (optional, later)

A domain like `nguyenquochung.com` costs roughly ¥1,500–2,000 per year from
Cloudflare Registrar. Once you own one: **Settings → Pages → Custom domain**,
enter it, and follow GitHub's DNS instructions. GitHub then issues an HTTPS
certificate automatically.

Worth doing eventually. A personal domain survives any future change of
institution, which a university page does not — the URL you print on a working
paper in 2027 still works in 2040.

### If you would rather not use GitHub at all

**app.netlify.com/drop** — drag the `Website` folder onto the page and it is
live in about thirty seconds, no account needed to test. Good for checking how
the site looks online before committing to the GitHub route.

---

## 6. Privacy: phone number and email

**Phone.** Your number appears nowhere — not in any page, and not in
`NguyenQH_CV_Web.pdf`, the CV the site publishes. The original
`NguyenQH_CV_092026.pdf` still contains it, which is correct for a private
master copy; just make sure you never link that file from a page, and never
upload it to the public Drive folder.

**Email.** No email address appears on the site at all — not as a link, not as
text, not hidden in an attribute or a script. This is the strongest option
available and needs no maintenance. The Contact page says so explicitly and
points enrolled students at the course system and everyone else at the
university.

If you ever want to put an address back, the safe way is **not** to type it into
the HTML. Either:

- embed a Google Form (visitors write to you, the address stays private), or
- ask me to restore `assets/email.js`, which assembled the address in the
  visitor's browser from two halves so that harvesters reading the raw HTML
  found nothing.

Bear in mind that your address is already printed on every published paper and
in the university directory, so removing it here reduces new scraping but does
not undo what is already circulating. Gmail's filters are worth ten minutes
regardless.

---

## 7. Changing the look

Open `assets/style.css`. The first block, `:root`, holds every colour and font
as a named value:

```css
--accent: #1f3a5f;   /* deep navy — links, headings, accents */
```

Change that one line and every link, button and accent on all five pages
follows. The site already adapts to dark mode automatically.
