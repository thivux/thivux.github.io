# Personal Website Content Update Implementation Plan

> **For agentic workers:** REQUIRED SUB-SKILL: Use superpowers:subagent-driven-development (recommended) or superpowers:executing-plans to implement this plan task-by-task. Steps use checkbox (`- [ ]`) syntax for tracking.

**Goal:** Refresh the public homepage, news, selected publications, and portrait to reflect Thi Vu's incoming University of Washington Ph.D. position and 2026 achievements.

**Architecture:** Keep the existing al-folio/Jekyll structure and update only its current content sources: `_pages/about.md` for biography and profile configuration, `_news` for dated announcements, `_bibliography/papers.bib` for publications, and `assets/img` for the portrait. Verify source-level content first, then build the static site and inspect generated output.

**Tech Stack:** Jekyll, Liquid, Markdown with YAML front matter, BibTeX, Bundler, ImageMagick-responsive image plugin

## Global Constraints

- Preserve the existing visual design and rectangular rounded portrait presentation.
- Do not modify the downloadable CV PDF, sample structured CV data, navigation, research-interest subtitle, or overall styling.
- Do not add components, plugins, packages, or other dependencies.
- Use January 3, 2026 for the EACL acceptance notification and July 29, 2026 for the Applied Engineering award.
- Link Shyam Gollakota, Steven Seitz, Dat Quoc Nguyen, and Quan Pham to the URLs recorded in the approved design.

---

### Task 1: Homepage biography and portrait

**Files:**
- Modify: `_pages/about.md:6-45`
- Create: `assets/img/portrait_curly_hair.png`
- Source asset: `/home/thivux/itsyoubro/face/portrait_curly_hair.png`

**Interfaces:**
- Consumes: the existing `profile.image` front-matter field and about-page Markdown rendered by `_layouts/about.liquid`
- Produces: a homepage biography with four advisor links and a profile image resolved as `assets/img/portrait_curly_hair.png`

- [ ] **Step 1: Record the failing source-content assertions**

Run:

```bash
test ! -e assets/img/portrait_curly_hair.png
test "$(rg -c 'actively seeking' _pages/about.md)" -eq 1
test "$(rg -c 'homes.cs.washington.edu/~gshyam|smseitz.com|AzzJssIAAAAJ' _pages/about.md)" -eq 0
```

Expected: all three commands pass, proving that the new portrait and advisor copy are absent while the obsolete alert remains.

- [ ] **Step 2: Install the portrait asset without transforming it**

Run:

```bash
cp /home/thivux/itsyoubro/face/portrait_curly_hair.png assets/img/portrait_curly_hair.png
cmp /home/thivux/itsyoubro/face/portrait_curly_hair.png assets/img/portrait_curly_hair.png
```

Expected: `cmp` exits 0, confirming the site asset is byte-for-byte identical to the supplied portrait.

- [ ] **Step 3: Update homepage front matter and biography**

Change `profile.image` to:

```yaml
  image: portrait_curly_hair.png
```

Replace the existing Qualcomm opening and Ph.D.-seeking alert with:

```markdown
I am an incoming **Ph.D. student in Computer Science & Engineering** at the **Paul G. Allen School of Computer Science & Engineering, University of Washington**, where I will be advised by [Shyam Gollakota](https://homes.cs.washington.edu/~gshyam/) and [Steven Seitz](https://www.smseitz.com/).

Before that, I was a **Research Resident** at **[Qualcomm AI Research](https://www.qualcomm.com/research/artificial-intelligence)**, where I was advised by [Dr. Dat Quoc Nguyen](https://datquocnguyen.github.io/) and [Dr. Quan Pham](https://scholar.google.com/citations?user=AzzJssIAAAAJ&hl=en).
```

Replace the outdated closing sentence with:

```markdown
As I begin my Ph.D. at the University of Washington, I am excited to deepen my theoretical understanding and contribute to the future of multimodal and human-centered AI.
```

- [ ] **Step 4: Verify the homepage source contract**

Run:

```bash
test "$(rg -c 'actively seeking' _pages/about.md || true)" -eq 0
test "$(rg -c 'incoming \*\*Ph\.D\. student in Computer Science & Engineering\*\*' _pages/about.md)" -eq 1
test "$(rg -o 'https://homes.cs.washington.edu/~gshyam/|https://www.smseitz.com/|https://datquocnguyen.github.io/|https://scholar.google.com/citations\?user=AzzJssIAAAAJ&hl=en' _pages/about.md | wc -l)" -eq 4
test "$(rg -c 'image: portrait_curly_hair.png' _pages/about.md)" -eq 1
cmp /home/thivux/itsyoubro/face/portrait_curly_hair.png assets/img/portrait_curly_hair.png
```

Expected: every command exits 0.

- [ ] **Step 5: Commit the homepage update**

```bash
git add _pages/about.md assets/img/portrait_curly_hair.png
git commit -m "feat: update academic status and portrait"
```

### Task 2: EACL publication and 2026 news

**Files:**
- Modify: `_bibliography/papers.bib:1-12`
- Create: `_news/announcement_3.md`
- Create: `_news/announcement_4.md`

**Interfaces:**
- Consumes: Jekyll's `news` collection and jekyll-scholar's `selected=true` query
- Produces: two dated inline news records and one selected EACL 2026 BibTeX record

- [ ] **Step 1: Run the failing achievement assertions**

Run:

```bash
test "$(rg -l 'Vietnamese Automatic Speech Recognition: A Revisit' _news _bibliography | wc -l)" -eq 0
test "$(rg -l 'Outstanding Resident Award in Applied Engineering 2026' _news | wc -l)" -eq 0
```

Expected: both commands exit 0, showing the new achievement content is absent before implementation.

- [ ] **Step 2: Add the EACL acceptance news**

Create `_news/announcement_3.md` with:

```markdown
---
layout: post
date: 2026-01-03
inline: true
related_posts: false
---

🎉 My first-author paper, [**Vietnamese Automatic Speech Recognition: A Revisit**](https://arxiv.org/abs/2603.14779), is accepted to **Findings of EACL 2026**!
```

- [ ] **Step 3: Add the Applied Engineering award news**

Create `_news/announcement_4.md` with:

```markdown
---
layout: post
date: 2026-07-29
inline: true
related_posts: false
---

🏆 I am honored to receive the **Outstanding Resident Award in Applied Engineering 2026** from the Qualcomm AI Residency Program.
```

- [ ] **Step 4: Add the selected EACL publication**

Prepend this record to `_bibliography/papers.bib`:

```bibtex
@inproceedings{vietasr,
  title     = {Vietnamese Automatic Speech Recognition: A Revisit},
  author    = {{Thi Vu} and Linh The Nguyen and Dat Quoc Nguyen},
  year      = {2026},
  url       = {https://arxiv.org/abs/2603.14779},
  booktitle = {Findings of the Association for Computational Linguistics: EACL 2026},
  selected  = {true}
}
```

- [ ] **Step 5: Verify source metadata and retained content**

Run:

```bash
test "$(rg -l 'Vietnamese Automatic Speech Recognition: A Revisit' _news _bibliography | wc -l)" -eq 2
test "$(rg -c 'date: 2026-01-03' _news/announcement_3.md)" -eq 1
test "$(rg -c 'date: 2026-07-29' _news/announcement_4.md)" -eq 1
test "$(rg -c 'Outstanding Resident Award in Applied Engineering 2026' _news/announcement_4.md)" -eq 1
test "$(rg -c 'Zero-Shot Text-to-Speech for Vietnamese' _bibliography/papers.bib)" -eq 1
test "$(rg -c 'Outstanding Resident Award in Research 2025' _news/announcement_2.md)" -eq 1
```

Expected: every command exits 0.

- [ ] **Step 6: Commit the achievements update**

```bash
git add _bibliography/papers.bib _news/announcement_3.md _news/announcement_4.md
git commit -m "feat: add EACL paper and 2026 award"
```

### Task 3: Static-site integration verification

**Files:**
- Verify: `_site/index.html`
- Verify: `_site/assets/img/portrait_curly_hair.png`

**Interfaces:**
- Consumes: all content and asset changes from Tasks 1 and 2
- Produces: a successful Jekyll build whose generated homepage contains the complete updated public content

- [ ] **Step 1: Build the site**

Run:

```bash
bundle exec jekyll build
```

Expected: Jekyll exits 0 and reports that generation completed successfully.

- [ ] **Step 2: Verify generated homepage text, links, and retained content**

Run:

```bash
test "$(rg -c 'incoming <strong>Ph.D. student in Computer Science &amp; Engineering</strong>' _site/index.html)" -eq 1
test "$(rg -o 'https://homes.cs.washington.edu/~gshyam/|https://www.smseitz.com/|https://datquocnguyen.github.io/|https://scholar.google.com/citations\?user=AzzJssIAAAAJ&amp;hl=en' _site/index.html | wc -l)" -eq 4
test "$(rg -c 'actively seeking' _site/index.html || true)" -eq 0
test "$(rg -c 'Vietnamese Automatic Speech Recognition: A Revisit' _site/index.html)" -ge 2
test "$(rg -c 'Outstanding Resident Award in Applied Engineering 2026' _site/index.html)" -eq 1
test "$(rg -c 'Zero-Shot Text-to-Speech for Vietnamese' _site/index.html)" -ge 1
test "$(rg -c 'Outstanding Resident Award in Research 2025' _site/index.html)" -eq 1
```

Expected: every command exits 0.

- [ ] **Step 3: Verify generated portrait assets**

Run:

```bash
test -f _site/assets/img/portrait_curly_hair.png
test "$(rg -c 'portrait_curly_hair' _site/index.html)" -ge 1
```

Expected: both commands exit 0. Responsive derivatives may also be generated by the configured ImageMagick plugin.

- [ ] **Step 4: Run final repository checks**

Run:

```bash
git diff --check
git status --short
```

Expected: `git diff --check` emits no output. `git status --short` contains no uncommitted source changes; ignored/generated `_site` output is acceptable.

