---
layout: docs
title: Contentful
css_class: tech-docs-page 
---

### Build

Pages are built using the Contentful's [jekyll-contentful-data-import](https://github.com/contentful/jekyll-contentful-data-import))

###  Hiding Contentful Variables with Jekyll, Jekyll Contentful Data Import, Contentful, and CircleCI


[Contentful documentation](https://github.com/contentful/jekyll-contentful-data-import#hiding-space-and-access-token-in-public-repositories)

[CircleCI documentation](https://circleci.com/docs/1.0/environment-variables/#setting-environment-variables-for-all-commands-without-adding-them-to-git)


**1. Generate your API keys in Contentful**

API —> Add API Key

Space ID and Content Delivery API - access token are the relevant fields.


**2. Add variables to your shell's configuration file**

Run `bundle update` first since this is a fairly recent feature

```
  export CONTENTFUL_ACCESS_TOKEN=abc123

  export CONTENTFUL_SPACE_ID=abc123
```



**3. In Jekyll _config, prepend the variable names with ‘ENV_’**

![]({{ '/images/contentful/jekyll-env-vars.png' | relative_url }})  


The Space ID will look at  `ENV['CONTENTFUL_SPACE_ID']` and your Access Token on `ENV[‘CONTENTFUL_ACCESS_TOKEN']`.

Run `bundle exec jekyll contentful` to make sure it works.

**4. Add ENV vars in CircleCI through the UI**

Go to Project settings > Environment Variable and add your variables. CircleCI reads them during the Machine part of the build. Use the same variable name you used locally.

![]({{ '/images/contentful/env-vars-added.png' | relative_url }})  