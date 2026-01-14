![VectorCharts Documentation Website](/site-image2.png)

This is the source code that runs the [VectorCharts documentation website](https://docs.vectorcharts.com/). If you are looking for the Vector Charts product, please head back to https://vectorcharts.com.

## How to Contribute

- If you have a request for expanded documentation or question that is not answered in the docs, please open an issue!
- For bug reports or feature requests for the VectorCharts.com platform itself, please use the [Contact Us form](https://vectorcharts.com/contact-us).
- PRs or issues are welcome for any expanded documentation, spelling/grammar issues, or factual errors.

---

## Developer's Guide

This repository uses Hugo to generate a static site from markdown files. The project also includes a custom theme, specifically designed for the documentation site. The theme sets up sidebar menus, headers and footers, etc.

The site is deployed using Zydro's internal CI/CD pipeline to a distributed CDN; The `master` branch is deployed to the production site.

### Development

Please install [Hugo](https://gohugo.io/).

To run a development server, use: 
```
hugo serve
```

To build and export the site to static HTML, use:
```
hugo
````

This will build the static site to the `public/` directory as HTML. These files should not be uploaded to git; they are ignored and will be built by the CI pipeline during the automated deployment.
