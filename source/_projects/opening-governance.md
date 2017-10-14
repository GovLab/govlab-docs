---
layout: docs
title: Opening Governance
github: https://github.com/GovLab/opening-governance
---

### History

Originally created with Squarespace but converted to Jekyll and Contentful.



### Prerequisites
- [jekyll](https://jekyllrb.com/) 


### Getting Started

- Clone the repo: [opening-governance](https://github.com/GovLab/opening-governance.git)

#### Installing

- Fetch and update bundled gems by running `bundle install`
- Fetch and update npm packages by running `npm install`

#### Development
- Run the server with `bundle exec jekyll serve`. Your server will run at [http://localhost:4000/](http://localhost:4000/)
- You can also use gulp for live reloading via browsersync. `gulp` will run at [http://localhost:3000](http://localhost:3000). **Needs Work** 
  
### Deployment

**Automatic updates with CircleCI has not been implemented. If implemented, make sure to change `be jekyll contentful` to `be rake contentful` for date mapping.**

Run `gulp deploy` to deploy to GitHub Pages.

We use [gulp-gh-pages](https://www.npmjs.com/package/gulp-gh-pages) to publish the site to [Github Pages](https://pages.github.com/). The deploy task is defined in `gulpfile.js`, which pushes the compiled _site folder to the gh-pages branch. 

[Setting up a custom domain with GitHub Pages](https://help.github.com/articles/using-a-custom-domain-with-github-pages/)
 

### Conversion

Squarespace only supports Wordpress exports. The export was converted to Contentful using [Wordpress Exporter](https://github.com/contentful-labs/wordpress-exporter.rb). The data was imported using [Contentful Importer](https://github.com/contentful-labs/contentful-importer.rb).

##### Publication Dates
Since you cannot edit the sys.createdAt values in Contentful, a custom mapper looks at the `Created_at` field in the Post content model, which is disabled in editing. The data_mapper plugin maps the `sys.createdAt` date onto the `Created_at` field so we can easily sort posts. The `rake contentful` task makes sure the dates are mapped on Contentful data import. 

### Features

#### Searching and Filtering

Searching is handled by [lunr.js](https://lunrjs.com/). Filtering is handled by [List.js](http://listjs.com/).


### Built With
- [jekyll](https://jekyllrb.com/)
- [jekyll-datapage-gen](https://github.com/avillafiorita/jekyll-datapage_gen)
- [jekyll-contentful-data-import](https://github.com/contentful/jekyll-contentful-data-import)
- [List.js](http://listjs.com/)
- [lunr.js](https://lunrjs.com/)
- GovLab [Styleguide](https://govlab.github.io/styleguide2/)
- [Foundation](https://foundation.zurb.com/)