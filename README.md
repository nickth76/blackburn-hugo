# Blackburn for modern Hugo

A ready-to-use Hugo site built on the [Blackburn](https://github.com/yoshiharuyamashita/blackburn) theme, updated to build cleanly (no errors or deprecation warnings) with current Hugo releases.

The theme itself is untouched: it is included as a git submodule, and every fix lives in `layouts/` of this site, which Hugo uses in place of the theme's files with the same name.

## Requirements

- [Hugo](https://gohugo.io/installation/) 0.158.0 or newer (tested with 0.168.0). The standard edition is enough.
- Git

## Quick start

```bash
git clone --recurse-submodules https://github.com/nickth76/blackburn-hugo.git my-blog
cd my-blog
hugo server --buildDrafts
```

Open http://localhost:1313. If you cloned without `--recurse-submodules`, run `git submodule update --init --recursive`.

Then:

1. Edit `hugo.toml`: `baseURL`, `title`, `locale`, `defaultContentLanguage`, `copyright` and the `[params]` section.
2. Replace `content/about.md` and `content/contact.md`.
3. Delete the example posts in `content/post/` and write your own:

   ```bash
   hugo new content post/my-first-post
   ```

   This creates a page bundle, `content/post/my-first-post/index.md`. Put the post's images in the same folder.

## Features and fixes

| Area | Change |
|------|--------|
| Hugo compatibility | Replaced APIs that newer Hugo removed or deprecated (`.Site.Social`, `.IsNode`, `languageCode`, `paginate`, `[indexes]`). |
| Language | `<html lang>` follows `locale`. Dates use `time.Format`, so month names follow the site language. |
| Sub-path hosting | All links and assets use `relURL`/`RelPermalink`, so the site also works at `https://user.github.io/repo/`. Menu entries use `pageRef`. |
| Social links | Configured in `[params.social]`. A value can be a username or a full URL. Mastodon also takes `@user@instance`. Any other link goes in `[[params.social_links]]`. |
| Comments | [giscus](https://giscus.app) (GitHub Discussions), configured in `[params.giscus]`. The theme's Disqus support still works through `params.disqus`. |
| Images | The `img` shortcode scales down large images at build time and adds lazy loading. |
| Code | Highlighted by Hugo (Chroma) at build time. highlight.js was removed: the two highlighters conflicted, and the theme loaded highlight.js asynchronously, which could break `hljs.initHighlightingOnLoad()`. |
| Math | MathJax only loads when `math = true` is set, site-wide or per post. The theme loaded it on every page, and its footer requested a `math-code.js` file that does not exist. |
| Search | Optional DuckDuckGo search box limited to the site (`params.search`). |
| Share buttons | Google+ removed (shut down). Added LinkedIn, Telegram and email. Turn them off with `share = false`. |
| Favicon | `params.favicon` is now used (the theme ignored it). |
| Pages | A real 404 page (the theme's was empty), section lists (the theme's `section.html` rendered empty), working links on the tags/topics index pages, no empty `<h2>` when there is no description. |
| Deploy | GitHub Actions workflow in `.github/workflows/hugo.yml`. |

## The `img` shortcode

```text
{{</* img src="photo.jpg" alt="Description" width="800" caption="Optional caption" */>}}
```

- `src`: a file in the post's folder. External URLs also work, but are not resized.
- `width`: maximum width in pixels. Defaults to 1000. Larger images are scaled down.
- GIF and SVG files are shown unchanged.

The theme's own `fluid_img`, `fluid_imgs` and `pure_table` shortcodes are still available.

## Comments with giscus

1. Enable Discussions in the GitHub repository that will hold the comments, and install the [giscus app](https://github.com/apps/giscus) on it.
2. On https://giscus.app, enter the repository to get its `repoId` and `categoryId`.
3. Fill in `[params.giscus]` in `hugo.toml`. Comments appear once `repo`, `repoId` and `categoryId` are all set.

## Building and deploying

Every push and pull request runs `.github/workflows/hugo.yml`, which builds the site to check that it still works. Nothing is published.

To publish to GitHub Pages:

1. In the repository go to **Settings → Pages → Build and deployment** and set **Source** to **GitHub Actions**.
2. Go to **Actions → Build / deploy → Run workflow**.

The workflow sets `baseURL` to the Pages address automatically. A repository other than `<user>.github.io` is published at `https://<user>.github.io/<repository>/`. For a custom domain, set it under **Settings → Pages → Custom domain**.

## Updating the theme

```bash
git submodule update --remote themes/blackburn
```

Check the result with `hugo server` before committing. The overrides in `layouts/` replace the theme's files with the same name.

## Credits

- [Blackburn](https://github.com/yoshiharuyamashita/blackburn) by Yoshiharu Yamashita, MIT License. The files in `layouts/` are based on it.
- [Pure CSS](https://purecss.io/), [Font Awesome](https://fontawesome.com/), [Hugo](https://gohugo.io/).

## License

MIT. See [LICENSE](LICENSE).
