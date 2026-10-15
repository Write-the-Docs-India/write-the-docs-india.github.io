# Write the Docs India

Source for [write-the-docs-india.github.io](https://write-the-docs-india.github.io), the site for the India chapter of [Write the Docs](https://www.writethedocs.org/). It's a Jekyll site that GitHub Pages builds on every push to `main`.

## Add an event

Add an entry to [`_data/events.yml`](_data/events.yml). The comment at the top of that file lists the fields. Events dated today or later show under "Upcoming"; older ones move to "Past events" on the next build.

## Write a blog post

Add a Markdown file to `_posts/` named `YYYY-MM-DD-short-name.md`:

```markdown
---
layout: post
title: "Meetup name: what it was about"
description: One line for the blog list.
authors:
  - Your Name
---

Who spoke, what they covered, links to slides and recordings.
```

Names under `authors` show as a byline under the title, linked to their page if they're in `organisers.yml`. It publishes at `/blog/YYYY/short-name/`. Link it from the event with `blog:` in `events.yml`. Put photos in `assets/img/blog/<event>/`.

## Other settings

`_config.yml` holds the community links (WhatsApp, LinkedIn, Meetup, Slack, Code of Conduct) and `cadence`, the regular meetup slot. The homepage hides the cadence line while it's empty.

Organisers are listed in [`_data/organisers.yml`](_data/organisers.yml).

## Deploy

GitHub Pages builds the site with the same `github-pages` gem pinned in the `Gemfile`, so there's no separate workflow to maintain. In the repo settings, Pages is set to deploy from the `main` branch, root folder. Each push to `main` triggers a `pages-build-deployment` run in the Actions tab, and the site updates a minute or two later.

Pull requests also get a preview build on Read the Docs, configured in [`.readthedocs.yaml`](.readthedocs.yaml). The Read the Docs bot comments on the PR with a link to the preview and the pages that changed. Direct pushes to `main` skip this, so open a PR when you want someone to look first.

## Preview locally

With Ruby 3.x (the Ruby that ships with macOS is 2.6, which is too old; `brew install ruby` gets a current one):

```sh
bundle install
bundle exec jekyll serve
```

Or with Docker, without installing Ruby:

```sh
docker run --rm -p 4000:4000 -v "$PWD":/srv -v wtdi-gems:/usr/local/bundle -w /srv ruby:3.3 \
  sh -c "bundle install && bundle exec jekyll serve --host 0.0.0.0 --force_polling"
```

Then open <http://localhost:4000>. Docker Desktop has to be running, and nothing else can be using port 4000. The `wtdi-gems` volume keeps the installed gems between runs, so only the first start is slow, and `--force_polling` makes Jekyll notice edits made on the Mac side. Restart it after changing `_config.yml`, since Jekyll only reads that file at startup.

## Planning notes

These come from the Write the Docs [sustainable meetups guide](https://www.writethedocs.org/organizer-guide/meetups/sustainable-meetups/):

- Run at most ten meetups a year, in the same slot each month. The guide suggests skipping August and December. In India, also check the dates for Diwali and other regional festivals before you book.
- Keep at least two organisers on every event.
- If no speaker is available, screen a talk from the [Write the Docs YouTube channel](https://www.youtube.com/c/WritetheDocs) and invite the speaker to join for Q&A.

## Design

The page borrows from how documents look: the logo as a drop cap, section numbers in the left margin, ruled sections, a contents sidebar, change bars next to new items, and dates in the margin for past events. If you add something, try to keep it in that vocabulary.

Colors come from the logo: navy `#07038D`, saffron `#FF671F`, green `#046A38`. Saffron fails contrast for text on white, so only use it for rules and marks. Headings use [Martel](https://fonts.google.com/specimen/Martel) and body text uses [Martel Sans](https://fonts.google.com/specimen/Martel+Sans), both designed alongside Devanagari, so Hindi or Marathi content would sit comfortably next to English. Dates and section numbers use IBM Plex Mono. The two handwritten margin notes use [Kalam](https://fonts.google.com/specimen/Kalam) from the Indian Type Foundry; keep them rare or they stop reading as notes. All styles are in `assets/css/site.css` under the `wtdi-` prefix.
