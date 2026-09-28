# Write the Docs India

Source for [writethedocs-india.github.io](https://writethedocs-india.github.io), the site for the India chapter of [Write the Docs](https://www.writethedocs.org/). It's a Jekyll site that GitHub Pages builds on every push to `main`.

## Add an event

Add an entry to [`_data/events.yml`](_data/events.yml). The comment at the top of that file lists the fields. Events dated today or later show under "Upcoming"; older ones move to "Past events" on the next build.

## Write a debrief

Add a Markdown file to `_posts/` named `YYYY-MM-DD-short-name.md`:

```markdown
---
layout: post
title: "Meetup name: what it was about"
description: One line for the debriefs list.
---

Who spoke, what they covered, links to slides and recordings.
```

It publishes at `/debriefs/YYYY/short-name/`. Link it from the event with `debrief:` in `events.yml`. Put photos in `assets/img/debriefs/<event>/`.

## Other settings

`_config.yml` holds the community links (WhatsApp, LinkedIn, Meetup, Slack, Code of Conduct) and `cadence`, the regular meetup slot. The homepage hides the cadence line while it's empty.

Organisers are listed in [`_data/organisers.yml`](_data/organisers.yml).

## Preview locally

With Ruby 3.x:

```sh
bundle install
bundle exec jekyll serve
```

Or with Docker, without installing Ruby:

```sh
docker run --rm -it -p 4000:4000 -v "$PWD":/srv -w /srv ruby:3.3 \
  sh -c "bundle install && bundle exec jekyll serve --host 0.0.0.0"
```

Then open <http://localhost:4000>.

## Planning notes

These come from the Write the Docs [sustainable meetups guide](https://www.writethedocs.org/organizer-guide/meetups/sustainable-meetups/):

- Run at most ten meetups a year, in the same slot each month. The guide suggests skipping August and December. In India, also check the dates for Diwali and other regional festivals before you book.
- Keep at least two organisers on every event.
- If no speaker is available, screen a talk from the [Write the Docs YouTube channel](https://www.youtube.com/c/WritetheDocs) and invite the speaker to join for Q&A.

## Design

The page borrows from how documents look: a running head, section numbers in the left margin, ruled sections, a contents list, change bars next to new items, and dates in the margin for past events. If you add something, try to keep it in that vocabulary.

Colors come from the logo: navy `#07038D`, saffron `#FF671F`, green `#046A38`. Saffron fails contrast for text on white, so only use it for rules and marks. Headings use [Martel](https://fonts.google.com/specimen/Martel) and body text uses [Martel Sans](https://fonts.google.com/specimen/Martel+Sans), both designed alongside Devanagari, so Hindi or Marathi content would sit comfortably next to English. Dates and section numbers use IBM Plex Mono. The two handwritten margin notes use [Kalam](https://fonts.google.com/specimen/Kalam) from the Indian Type Foundry; keep them rare or they stop reading as notes. All styles are in `assets/css/site.css` under the `wtdi-` prefix.
