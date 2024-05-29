# A Svelte Template for Interactive Articles with Svelte

For UCSD dataviz course: [https://dsc106.com/](https://dsc106.com/).

This is a starter template to build an interactive article using Svelte.

It comes with some built-in features:

- Responsiveness
- Support for browser-rendered math equations
- Scrollytelling built-in
- An example of a responsive, d3 + svelte visualization.

### Getting Started

To get started, first clone this repository. Then:

```
# install dependencies
npm install
```

Then run development version:

```
npm run dev
```

To build for prod:

```
npm run build
```

### Deploying to GitHub Pages: Easiest

The easiest way it to bundle the assets, then upload this to your github pages repo (or the `gh-page` branch).

First, create the `dist/` dir:

```
npm run build
```

Then, copy the contents of this `dist/` to your `__.github.io` git repo. E.g.;

```
cp -r dist/* ../path/to/your-website.github.io
```

So, after all is said and done, your `__.github.io` project should have files like:

```
assets      build       favicon.png index.html
```

You will need to re-do this process everytime you want to update the site with your changes.

### Deploying to Github Pages: Second Easiest

Follow this guide: [https://medium.com/@aishwaryaparab1/deploying-vite-deploying-vite-app-to-github-pages-166fff40ffd3](https://medium.com/@aishwaryaparab1/deploying-vite-deploying-vite-app-to-github-pages-166fff40ffd3)

### Deploying Vite to GitHub Pages

Another method is follow this documentation: [https://vitejs.dev/guide/static-deploy#github-pages](https://vitejs.dev/guide/static-deploy#github-pages)

### Deploying to GitHub Pages CI

Alternatively, you can follow the steps in this README: [https://github.com/sitek94/vite-deploy-demo](https://github.com/sitek94/vite-deploy-demo).

Note that this is a Vite repo, so you may start at the header titled, "**Create a new GitHub repository**":
