# Scottsdale Flying Club — website

A plain static site. No build step, no framework, no JavaScript. Every page is a
single `.html` file that links to one stylesheet.

## Files

```
index.html         Home
about.html         About
join.html          Join
photographs.html   Photographs
video.html         Video
contact.html       Contact
thanks.html        Shown after the contact form is submitted
css/style.css      All styling (colors live in the :root block at the top)
images/            Site images. hero.jpg is the big homepage photo.
images/gallery/    Photographs page images.
Dockerfile         nginx image, for deploying on a Docker host.
```

"For Members" in the navigation is an external link to Flight Circle — it is not
a page in this repo.

## Editing

Open any `.html` file in a text editor. Text written in `ALL CAPS` is a
placeholder waiting to be replaced with real copy.

The navigation appears at the top of each page. If you add or rename a page, the
nav list has to be updated in every file.

## Preview locally

Just double-click `index.html`, or serve the folder:

```bash
python3 -m http.server 8000
```

Then open http://localhost:8000

## Images

- **Logo** — `images/logo.png`. Transparent background, so it sits on any color.
  It appears at the top of every page.
- **Hero** — `images/hero.jpg`, the big photo behind the club name on the home
  page. To change it, replace that file with another wide landscape shot
  (~2400px wide).
- **Gallery** — each photograph needs two files with the *same name*: the
  full-size version in `images/gallery/` and a smaller copy in
  `images/gallery/thumb/`. The page shows the thumbnail and links to the
  full-size one. Then copy one `<figure>` block in `photographs.html`.

To prepare new photos (ImageMagick):

```bash
magick photo.jpg -auto-orient -resize 1600x1600\> -strip -quality 82 images/gallery/name.jpg
magick photo.jpg -auto-orient -resize 800x800\>  -strip -quality 80 images/gallery/thumb/name.jpg
```

Don't commit full-size camera files — they make the repo huge and the page slow.

## Deploying with Docker

```bash
docker build -t sfc-site .
docker run -d --name sfc-site -p 8080:80 sfc-site
```

To update: `git pull`, rebuild, restart the container.
