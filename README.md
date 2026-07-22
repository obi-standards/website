# Open Blockchain Intelligence Standards

Source for the OBIS landing site at [obistandards.org](https://obistandards.org).

## Layout

- `website/` — Hugo source (theme: [hugo-book](https://github.com/alex-shpak/hugo-book) as a submodule)
- `.github/workflows/hugo.yml` — builds and deploys to GitHub Pages on push to `main`

## Local development

```sh
cd website
hugo server -D
```

Site is served at <http://localhost:1313>.

## Publishing

Push to `main`. GitHub Actions builds the site and deploys to GitHub Pages. The custom domain `obistandards.org` is configured via the `website/static/CNAME` file and DNS records on easyname.
