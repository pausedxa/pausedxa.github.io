# pause.dxa website: instructions for Claude

This is the website of **pause.dxa**, the Dhrupad and electronic soundscapes duo of Sahitya and Harsh, based in Auroville, India. It's live at **https://pausedxa.github.io**, served by GitHub Pages from the `main` branch of this repo. Anything pushed to `main` goes live in about a minute.

Sahitya and Harsh edit the site by chatting with Claude. They aren't web developers, so explain changes in plain language, show them what changed, and confirm before publishing anything big.

## How the site is built
- It's a single static page: `index.html`, with inline CSS and JS, and images, audio and fonts in `assets/`. There's no build step.
- **Editable text lives in `content/site.json`**, and the **performances list in `content/gigs.json`** (newest first). The page loads these files and fills in every element marked `data-c="section.key"` (plus `data-c-href` for links and `data-list` for the places and venues lists). The text written in `index.html` is only a fallback. **When changing text, edit the JSON files, not the HTML.** Formatting in the JSON: `*word*` = serif italic, `**word**` = bold.
- Sahitya and Harsh also edit these two files without Claude, through **Pages CMS** (https://app.pagescms.org, signed in with the pausedxa GitHub account). Its form layout is defined in `.pages.yml`. If you add a new editable piece of text, add a `data-c` attribute in `index.html`, the key in `content/site.json`, and a matching field in `.pages.yml`.
- The year filter buttons are generated from the years in `gigs.json`.
- Other lists are JS arrays near the bottom of `index.html`:
  - `TRACKS`: SoundCloud tracks.
  - `WALL`: the photos section. Entries are `[image name without .jpg, Instagram post code or null, caption]`.
  - `FILM`: the scrolling photo strip.
  - `STAGES`: the sleep-cycle text in the Bedtime Sonic Fables section.
- **Colours** are set in the `:root` tokens at the top of the CSS. **Layout and pace** are in the `CALM LAYER` block, and **fonts** in the `TYPE` block, both near the end of `<style>`.
- **Section order:** hero → about → dhrupad → upcoming-show band → photo strip → projects → Bedtime Sonic Fables → performances (photo, journey map, places, venues, list) → listen → photos → work with us → contact.
- To preview, run `python3 -m http.server 8765` in this folder and open http://127.0.0.1:8765.

## Rules (agreed by Sahitya and Harsh)
- **"pause.dxa" is always lowercase**, everywhere, even inside uppercase labels. Use the `.brand` class, which sets `text-transform:none`.
- **Tone:** simple, professional, artistic and realistic. No hype or boasting, no stat counters, no lines like "24 cities, one drone". Use short factual sentences and plain headings.
- **Dhrupad:** describe it respectfully and accurately. Spell it "alaap", not "ālāp", because the headline font renders ā badly. Hedge anything uncertain about the tradition.
- **No flag emojis.** Don't use emojis as icons generally; use photos instead.
- **No links** to Sahitya's or Harsh's personal Instagram profiles. Link only the pause.dxa accounts.
- **No photos showing identifiable strangers' faces**, especially audience members lying down at immersions. Prefer photos of the two of them, instruments, venues or cymatics.
- **Contact is email only:** pause.dxa@gmail.com. Never add phone numbers.
- **Journey map:** keep the existing illustrated map image, `assets/journey-map-2026.jpg`. Don't replace it with a generated or live map. To add a place, edit the image in the same style: dark-blue country fill #3079df and a Gotham Bold label tag in one of the existing tag colours.
- **Design:** keep the current palette (Pigeon grey #898b86, ink #1d1e1c, paper #f4f3f0, Acid Lime #c7f80a only as a small accent, Almond Blossom pink #f9bdc6), the calm pace (slow motion, soft shadows, no tilts), and the fonts (Fraunces for headlines in lowercase, Bricolage Grotesque for body text, Space Mono for small labels). For bigger design changes, show options side by side before changing anything.
- **Images:** download them into `assets/` rather than linking to Instagram, because Instagram image links expire. Resize large photos to about 1600px and save them as JPG at about 80% quality.

## Publishing
1. **Before editing,** get the latest version with `git pull`, since two people (and Pages CMS) edit this site.
2. **Make the change,** check it in a browser preview, and make sure every image the page uses exists in `assets/`.
3. **Commit** with a short, clear message, then `git push` to `main`.
4. **Wait for GitHub Pages** to finish building, about a minute, and check the live site.
5. **Tell the person** what changed, and that they may need Cmd + Shift + R to see it.

Every published version is kept in the git history, so anything can be rolled back.

## Things to remember
- **Wonderfruit, 3–7 Dec 2026, Enfold stage** is shown as upcoming in the band under the Dhrupad section (`upcoming` in `content/site.json`) and at the top of `content/gigs.json`. After the festival, update the band to the next show and remove "upcoming" from that row.
- The `desk/` folder is a separate internal tool (the pause desk), built in another session. Don't change it as part of website work.
