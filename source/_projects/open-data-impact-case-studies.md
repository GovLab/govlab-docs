---
layout: docs
title: Opening Governance
github: https://github.com/GovLab/odimpact-2
---

# Open Data Impact Case Studies

### Prerequisites
- [jekyll](https://jekyllrb.com/)

### Getting Started
- Clone the repo: [opening-governance](https://github.com/GovLab/odimpact-2.git)

### Installing
- Fetch and update bundled gems by running `bundle install`
- Fetch and update npm packages by running `npm install`

### Development
- Run the server with `bundle exec jekyll serve`. Your server will run at [http://localhost:4000/](http://localhost:4000/)

#### Site Structure
The jekyll site is located under `source/`.
- `source/_case_studies`: case study templates
- `source/_data`: yaml files for some of the site data including team members and elements of the open data periodic table page
- `source/files`: pdf files for the case studies
- `source/js`: includes the d3 map js (map.js - simplified index page map, packmap.js - explore page map)

#### Adding a Case Study
1. Create a new jekyll template file for the case study in `source/_case_studies`
2. As of now, an entry for the case study also has to be manually added to `source/js/studies.json` and `source/js/packstudies.json` for the case to appear on the map
3. Main images for each case study should be added under `source/images/banners` and a smaller size thumbnail added to `source/images/banners/thumbs` (There currently isn't a gulp task to automatically generate thumbnails, but could be added later)
4. Restart `bundle exec jekyll serve` and the case study should be updated

### Deploying
Run `gulp deploy` to deploy to GitHub Pages.

We use [gulp-gh-pages](https://www.npmjs.com/package/gulp-gh-pages) to publish the site to [Github Pages](https://pages.github.com/). The deploy task is defined in `gulpfile.js`, which pushes the compiled _site folder to the gh-pages branch.

[Setting up a custom domain with GitHub Pages](https://help.github.com/articles/using-a-custom-domain-with-github-pages/)