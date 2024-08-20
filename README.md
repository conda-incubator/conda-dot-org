# conda-dot-org

[![Netlify Status](https://api.netlify.com/api/v1/badges/2db454b7-f4c7-409c-8f0d-29bcb5029577/deploy-status)](https://app.netlify.com/sites/conda-dot-org/deploys)

This is the repository for the conda.org community website. To become involved:

- Join the [conda.org chat room](https://app.element.io/#/room/#conda.org:matrix.org), which is part of the [conda space on Matrix](https://app.element.io/#/room/#conda:matrix.org)
- Visit the [Root HackMD page](https://hackmd.io/DGtozSlsSjSokpYAK5-9hw), which links to everything in HackMD.
- We meet every two weeks on Monday at 9am US Central time / 16:00 Central European Time. Please join the [Matrix room](https://app.element.io/#/room/#conda.org:matrix.org) and we will invite you.

## Code of Conduct

This repo and the web site it generates are governed by the [conda organization code of conduct](CODE_OF_CONDUCT.md).

## Implementation details

It is built using [Docusaurus 2](https://docusaurus.io/), a modern static website generator. The
contents are structured like this:

- `.github/`: Workflows for deployment.
- `blog/`: Blog posts. Can use `.md` (Markdown), `.mdx` (Markdown with react) or `.js` extensions.
  Complex posts can use its own directory.
- `docs/`: Documentation with navigation and sidebars.
- `src/`: Resources (React components, custom CSS) and logic for standalone pages
  - `src/pages`: Standalone pages. This directory contains the homepage (`index.js`) and other simpler pages (`community.md`).
- `static/`: Static resources like images and icons.
- `babel.config.js`: Configuration to install `docusaurus`.
- `docusaurus.config.js`: Configuration for `docusaurus`. Includes variables like title and description, navigation menu items, etc.
- `package.json`: More configuration to install `docusaurus`.
- `sidebars.js`: Support for sidebars. We use in automatic mode now.

> Non listed directories or files are generated automatically are not relevant for modifications.

## Local Development

```bash
$ git clone
$ cd conda-dot-org
$ npm install
$ npm run start
```

This command starts a local development server and opens up a browser window.
Most changes are reflected live without having to restart the server.

## Deployment

<a href="https://www.netlify.com"> <img src="https://www.netlify.com/v3/img/components/netlify-color-accent.svg" alt="Deploys by Netlify" /> </a>
