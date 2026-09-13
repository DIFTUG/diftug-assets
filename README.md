# diftug-assets

Public binary assets for **Do It For The Underground** (`doitfortheunderground.vercel.app`).

This repository exists so the site deployment stays small. The images below total about
2.2 MB on their own — more than the entire website source — and none of them are needed to
render a page. They are served from jsDelivr instead of from Vercel:

```
https://cdn.jsdelivr.net/gh/Moonfire-dreamwalkers/diftug-assets@v1/<file>
```

`@v1` is a tag, so the URLs are immutable and cached hard; publishing new artwork means
retagging (for example `v2`) and updating one value in the site's `data/site.config.json`.

## Contents

| File | Used for |
| --- | --- |
| `og-image.jpg` | `og:image` / `twitter:image` (1200x630 logo on brand black) |
| `logo-512.png` | JSON-LD `Organization.logo` |
| `logo-128.png` | Header mark on the `/artists` page (downscaled from `logo-512.png`) |
| `apple-touch-icon.png` | iOS home-screen icon (180x180) |
| `favicon-48.png` | Larger favicon size, kept out of the app deploy |
| `diftug-logo-upscaled.png` | Master logo, the source everything above is downscaled from |
| `diftug-logo-source.jpeg` | Original artwork the master was upscaled from |
| `diftug-logo.svg` | Legacy wrapper around the raster. Not used as a favicon: browsers refuse to load an external `<image href>` inside an SVG favicon, so it renders as an empty tab icon |

Do not put anything private here — this repository is public, and so is every file in it.
The favicons the browser requests directly (`/favicon.ico`, `/assets/favicon-16.png`,
`/assets/favicon-32.png`) deliberately stay in the site deploy: they are a few kilobytes and
must live on the site's own origin.

## Regenerating

From the site repository, with the masters in this folder:

1. Resize `diftug-logo-upscaled.png` to 16/32/48/180 with high-quality bicubic interpolation.
2. Write the three favicons and `apple-touch-icon.png` back into the site's `assets/` folder.
3. Rebuild `favicon.ico` as a three-entry PNG-in-ICO container (16/32/48).
4. Downscale to 128px for `logo-128.png` here, then commit, tag, and update the site config.
