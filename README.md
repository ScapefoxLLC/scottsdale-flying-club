# Scottsdale Flying Club — website

A plain static site. No build step, no framework, no JavaScript. Every page is a
single `.html` file that links to one stylesheet.

## Files

```
index.html         Home
about.html         About
join.html          Join
history.html       History
photographs.html   Photographs
video.html         Video
contact.html       Contact
css/style.css      All styling (colors live in the :root block at the top)
images/            Site images. hero.jpg is the big homepage photo.
images/gallery/    Photographs page images.
Dockerfile         nginx image, for deploying on a Docker host.
```

"For Members" in the navigation is an external link to AircraftClubs — it is not
a page in this repo.

## Editing

Open any `.html` file in a text editor. Text written in `ALL CAPS` is a
placeholder waiting to be replaced with real copy.

The navigation appears at the top of each page. If you add or rename a page, the
nav list has to be updated in every file — there are seven of them.

## Preview locally

Just double-click `index.html`, or serve the folder:

```bash
python3 -m http.server 8000
```

Then open http://localhost:8000

## Images

- **Hero** — put a wide landscape photo at `images/hero.jpg` (about 2000px wide
  is plenty), then add the class `hero--photo` to the `<header class="hero">`
  tag in `index.html`.
- **Gallery** — put photos in `images/gallery/` and copy the commented example
  block in `photographs.html` once per photo. Resize to ~1600px on the long edge
  before committing; full-size camera files make the repo huge and the page slow.

## Deploying with Docker

```bash
docker build -t sfc-site .
docker run -d --name sfc-site -p 8080:80 sfc-site
```

To update: `git pull`, rebuild, restart the container.
