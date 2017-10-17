---
layout: docs
title: Data Collaboratives
github: https://github.com/GovLab/data-collaboratives
---

### Installation
    npm install
    bundle exec jekyll build

### Run server
    gulp

### Data
The Contentful API data is fetched and stored in `cases.yaml` file within the `_data` folder.

Contentful data is automatically updated with CircleCi, but it can also be pulled directly from Contentful:

    bundle exec jekyll contentful

### Deploy
To deploy simply merge your branch to master. Once merged, CircleCi will build and push the changes to `gh-pages` automatically if all tests pass.
