# AGENTS.md

## Scope
This file applies to the entire repository.

## Project identity
- This repo is a Jekyll site based on al-folio.
- `_projects/` is currently used to render people/member cards through `site.projects`.
- Content is mainly data-driven from:
  - `_projects/` for people/member cards
  - `_news/` for news posts
  - `_bibliography/papers.bib` for publications

## General safety rules
- Keep edits minimal and scoped to the request.
- Do not rewrite or reformat large files unless the task explicitly requires it.
- Do not modify unrelated files.
- Do not invent, infer, or complete missing personal, publication, project, award, or funding information.
- Only use information explicitly provided in the task or already present in the repository.
- Do not search external sources unless explicitly requested.
- Do not update dependencies unless explicitly requested.
- Do not change site-wide layout, navigation, theme, CSS, or deployment settings unless explicitly requested.

## Git workflow
- Do not commit directly to `main` or `master`.
- Create a dedicated branch for each task.
- Submit changes via a Pull Request.
- In the PR description, list:
  - files changed
  - content added or updated
  - validation command run
  - whether the build passed
- If the build was not run, explain why.

## Protected files
Do not modify the following unless explicitly requested:
- `.github/workflows/*`
- `bin/deploy`
- `_config.yml`
- `Gemfile`
- `Gemfile.lock`
- `docker-compose.yml`
- `docker-local.yml`
- global layout files under `_layouts/`
- global includes under `_includes/`
- package manager lock files

## Content update conventions

### Add a member
1. Create one Markdown file in `_projects/`.
2. Use existing member Markdown files as templates.
3. Required front matter:
   - `layout: page`
   - `title`
   - `description1`
   - `description2`
   - `description3`
   - `img`
   - `importance`
   - `category`
4. `category` must be one of:
   - Assistant Professor
   - Postdoc
   - PhD Students
   - Master Students
5. Preserve the exact spelling of names, titles, email addresses, research interests, and homepage links provided by the user.
6. Do not modify existing member files unless explicitly requested.
7. Preserve the existing ordering logic within each category.
8. Use `importance` consistently with nearby members in the same category.
9. When unsure about `importance`, choose a value that places the new member after existing members in the same category.
10. If a field is missing, follow the existing placeholder convention rather than inventing content.

### Member images
1. If adding an image, place it under the existing people/member image directory if one exists; otherwise use `assets/img/`.
2. Follow existing image naming conventions.
3. Prefer lowercase filenames with hyphens or underscores, e.g., `san-zhang.jpg`.
4. Do not rename, move, or delete existing images unless explicitly requested.
5. Reference images using the same path style as existing member files.
6. If no image is provided, use the existing default placeholder image if available.

### Add a publication
1. Add one BibTeX entry in `_bibliography/papers.bib` following the existing ordering convention.
2. Required fields:
   - key
   - title
   - author
   - year
   - venue field: `booktitle` or `journal`
   - `abbr`
   - `bibtex_show={true}`
3. Optional fields:
   - `pdf`
   - `code`
   - `website`
   - `arxiv`
   - `doi`
4. Preserve the exact paper title, author order, venue name, and year provided by the user.
5. Do not normalize, abbreviate, or rewrite paper titles unless explicitly requested.
6. Use a unique BibTeX key consistent with existing entries.
7. Do not change existing BibTeX entries unless explicitly requested.
8. Do not add links by guessing or searching externally unless explicitly requested.
9. Ensure the publication year exists in `_pages/publications.md` `years` list if the site requires it.
10. Do not reformat the entire BibTeX file for a small publication update.

### Add a news item
1. Add one file in `_news/` named `announcement_YYYYMMDD.md`.
2. Front matter:
   - `layout: post`
   - `date` with timezone
   - `inline: true` unless a detail page is needed
3. Keep one concise, factual news sentence in the body.
4. Use the same language and tone style as existing news items.
5. Do not exaggerate achievements.
6. Do not modify existing news files unless explicitly requested.
7. Use the timezone format already used in existing `_news/` files.

## Local dev commands
- `bundle install`
- `bundle exec jekyll serve`
- `bundle exec jekyll build`
- Docker preview:
  - `docker-compose up`
  - or `docker-compose -f docker-local.yml build && docker-compose -f docker-local.yml up`

## Validation checklist before commit
- Run: `bundle exec jekyll build`
- Confirm no Liquid errors and no broken front matter.
- For content updates, verify:
  - member card appears in `/people/`
  - publication appears in `/publications/` under the correct year
  - news appears in the homepage news list
- Include the build result in the PR description.
- If validation fails, fix only errors caused by the current task.

## If validation fails
- Do not ignore build errors.
- First check whether the error is caused by the current task.
- Fix only task-related errors.
- If the build fails due to pre-existing unrelated issues, report them clearly in the PR description and do not make broad unrelated fixes.

## Deployment notes
- Production deploy is via GitHub Actions workflow `.github/workflows/deploy.yml`.
- Deployment branch is `gh-pages` through `bin/deploy`.
- Do not change the GitHub Pages source branch or deployment branch unless explicitly requested.
- Do not add Vercel or Netlify configs unless explicitly requested.
