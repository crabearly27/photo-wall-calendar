# Project brief: Photo Wall Calendar (working name)

Read this whole brief carefully. Do not create files, scaffold the project or write any code yet. When you have read it, reply with: (1) your understanding of the project in a few lines, (2) any questions or gaps you see, (3) a proposed phased build plan and tech stack, with anything you would change from my suggestions below and why. Then wait for my approval before doing anything.

## Who I am and why this exists

I'm a solo builder based in London (timezone Europe/London). This is a personal project first: I'm building it to solve my own problem, then I may release it publicly. It is not a commercial product right now, so there is no need for payments, pricing or growth features. Keep things simple, cheap to run (free tiers where possible) and easy for me to maintain.

This is a separate project from my other calendar idea (custom calendar systems). Do not merge them, though they may share a similar stack.

## The idea

A calendar view for my existing calendars (Google Calendar and Outlook) that looks and feels like a printed wall calendar: the festive kind with a large image at the top of each month and a grid of days below. The unique feature is that each day square can hold an image, so the calendar becomes a visual memory album as much as a schedule.

It should work as a good everyday calendar, but its main purpose is display and memories.

## What I want to put on days (my real use cases)

* Video games I completed, shown with the game's cover art.
* Films I watched at the cinema, shown with the poster.
* Memorable days: meeting interesting people, time with family and friends, shown with my own photos.

## Must have features (personal version)

1. **Wall calendar month view.** Large hero image at the top of each month (chosen by me, or defaulting to a highlight from that month's memories). Below it, a month grid where each day square shows its image filling the square, with the date number and a small label overlaid legibly.
2. **Memories as their own entries.** A memory has a date, a title, an optional note, one or more images and a type (game, film, people, family, other; types should be editable). A memory is stored in this app, not written into Google Calendar. Optionally a memory can be linked to an existing calendar event.
3. **Multiple memories on one day.** Decide how the square handles this (cover image chosen by me, small count badge, tap to see all) and propose options.
4. **Day detail view.** Tap a square to see the day's memories, images at full size, notes and that day's calendar events.
5. **Adding images, three ways:**
   * Upload from my device (phone camera roll or desktop).
   * Pick from Google Photos.
   * Automatic artwork lookup: type a film or game name, pick the right match, and the poster or cover is attached.
6. **Calendar events.** Read my Google Calendar events (and later Outlook) and show them in the views in a lighter style, so the app still works as a normal calendar. Read only to begin with.
7. **Other views.** A normal month and week view, plus a year overview that works like a mosaic of the year's memories.
8. **Works well on my phone and on a large screen**, including a "display mode" that cycles through months full screen, suitable for a tablet or spare monitor on a wall.

## Technical facts to account for (please verify current details)

* **Google Calendar:** reading events needs Google sign in and the read only calendar scope. For personal use the Google Cloud project can stay in testing mode with me as a test user. Opening it to the public later requires Google's app verification for sensitive scopes, so keep scopes minimal from day one.
* **Outlook:** reading events uses Microsoft Graph with a read calendar permission and a Microsoft sign in. This can come after Google.
* **Google Photos:** since 2025 the Photos Library API no longer lets apps browse a user's whole library. The supported route is the **Google Photos Picker API**, where I choose photos in Google's own picker. The media URLs it returns are temporary, so the app must download the chosen images straight away and keep its own copy in storage. Design the storage model around owning copies of every image.
* **Film posters:** TMDB API (free for non commercial use, requires attribution in the app).
* **Game covers:** IGDB API (accessed with Twitch developer credentials).
* API keys and OAuth secrets must stay on the server, never in client code.
* Images should be resized and served in sensible sizes (thumbnail for squares, larger for hero and detail views) so the grid loads quickly on mobile.

## Later (not for the first version, but design so they fit)

* Outlook support if not in the first version.
* Export a month or year as a printable wall calendar PDF (this could become a lovely physical keepsake).
* Sharing a month or year publicly via a link, or with family.
* Optional writing back to Google Calendar (for example a separate "Memories" calendar), only if it proves useful.
* Multiple users with accounts, and a public release.
* Other artwork sources (books, TV series, concerts) using the same lookup pattern.

## Technical preferences (suggestions, push back if you have better ideas)

* Web app first, installable on my phone as a PWA. No app store builds yet.
* Next.js with TypeScript, hosted on Vercel; Supabase for database, auth and image storage.
* Keep the integrations (Google Calendar, Microsoft Graph, Google Photos Picker, TMDB, IGDB) behind small, separate server modules so each can be added, swapped or removed independently.
* Keep dependencies few and explain each one you add. I'm comfortable with Claude Code but I want to understand the architecture.
* Write tests for the date logic (month grids, weeks starting Monday, timezones, all day events not shifting a day because of UTC conversion).

## Design direction

* The look should feel like a beautiful printed calendar: generous imagery, elegant typography, warm and personal rather than a corporate dashboard.
* Day squares are photo first; text must stay readable over any image (consider gradients or scrims).
* Weeks start on Monday. UK date formats.

## Copy and style rules

* British English spelling.
* No hyphens anywhere in user facing copy (UI text, labels, buttons, empty states). Rephrase instead.

## Reminder

Do not start building. Read, ask questions, propose the plan and wait for my go ahead.
