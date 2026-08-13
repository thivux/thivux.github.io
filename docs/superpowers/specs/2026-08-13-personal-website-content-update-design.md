# Personal Website Content Update

## Goal

Update the public-facing website to reflect Thi Vu's incoming Ph.D. position, recent EACL 2026 Findings paper, 2026 Qualcomm award, and new portrait. Keep the existing visual design and avoid expanding the work into a complete résumé or CV-page rewrite.

## Homepage biography

Make the incoming Ph.D. position the primary introduction: “I am an incoming Ph.D. student in Computer Science & Engineering at the Paul G. Allen School of Computer Science & Engineering, University of Washington, where I will be advised by Shyam Gollakota and Steven Seitz.” Link [Shyam Gollakota](https://homes.cs.washington.edu/~gshyam/) and [Steven Seitz](https://www.smseitz.com/) to their corresponding faculty websites.

The next sentence will present Qualcomm AI Research as the preceding role: “Before that, I was a Research Resident at Qualcomm AI Research, where I was advised by Dr. Dat Quoc Nguyen and Dr. Quan Pham.” Link [Dr. Dat Quoc Nguyen](https://datquocnguyen.github.io/) and [Dr. Quan Pham](https://scholar.google.com/citations?user=AzzJssIAAAAJ&hl=en) to the supplied pages, and retain the existing Qualcomm AI Research link.

Remove the blue alert that says Thi is seeking a Fall 2026 Ph.D. position. Revise the final biography sentence so it no longer describes entering a Ph.D. program as a future aspiration. Preserve the existing research-interest and research-vision content otherwise.

## News

Add two inline news entries, following the existing `_news` format:

- January 3, 2026: the first-author paper “Vietnamese Automatic Speech Recognition: A Revisit” was accepted to Findings of EACL 2026. Link the paper title to <https://arxiv.org/abs/2603.14779>. This date is the official EACL 2026 acceptance-notification date; main-track and Findings decisions were released simultaneously.
- July 29, 2026: Thi received the Outstanding Resident Award in Applied Engineering 2026 from the Qualcomm AI Residency Program.

The existing ACL 2025 paper and Outstanding Resident Award in Research 2025 news entries remain unchanged.

## Publications

Add “Vietnamese Automatic Speech Recognition: A Revisit” to `_bibliography/papers.bib` as a selected first-author publication in Findings of EACL 2026. Use the author list from the résumé—Thi Vu, Linh The Nguyen, and Dat Quoc Nguyen—and link to <https://arxiv.org/abs/2603.14779>. Retain the existing ACL 2025 publication.

## Portrait

Copy `/home/thivux/itsyoubro/face/portrait_curly_hair.png` into `assets/img/` with a clear, stable filename and update the homepage profile configuration to reference it. Preserve the existing rectangular, rounded presentation (`image_circular: false`); do not crop or otherwise alter the source portrait.

## Scope boundaries

Do not modify the downloadable CV PDF, the sample structured CV data, page navigation, research-interest subtitle, or overall site styling. No new components or dependencies are required.

## Verification

- Build the Jekyll site using the repository's supported build command.
- Confirm the build completes without errors.
- Check the generated homepage for the UW introduction, all four advisor links, removal of the Ph.D.-seeking alert, both new news items, the selected EACL publication, and the new portrait path.
- Confirm the portrait asset exists in the built site and the prior ACL 2025 publication/news remain present.
