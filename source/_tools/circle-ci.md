---
layout: docs
title: Circle CI
website:
css_class: tech-docs-page 
---

### Automated Builds with CircleCI, Contentful, and Gulp

Based on [Automated rebuild and deploy with CircleCI and Webhooks]( https://www.contentful.com/developers/docs/ruby/tutorials/automated-rebuild-and-deploy-with-circleci-and-webhooks/)


**1. Add an SSH key:**
  - [Github Instructions](https://help.github.com/articles/adding-a-new-ssh-key-to-your-github-account/)
  - [Circle CI Instructions](https://circleci.com/docs/1.0/adding-read-write-deployment-key/)

**2. Add your project to [CircleCI](https://circleci.com/):**
When you log in with your GitHub account, your organizations and their projects will be listed in CircleCI. Select your organization, and click on Add Project.

![]({{ '/images/circleci/0a-circleci-add-project.png' | relative_url }})        

**3. Setup Project**

Select the project you want to start building and click on Setup Project.

![]({{ '/images/circleci/0b-circle-ci-setup-project.png' | relative_url }})     

This will take you to the setup page. Select Linux as the operating system and Ruby as the language. 

![]({{ '/images/circleci/0c-circleci-setup-page.png' | relative_url }})         

      
You can ignore Next Steps because we will provide a custom circle.yml file. Click on Start Building.

![]({{ '/images/circleci/0d-circleci-startbuilding.png' | relative_url }})      

Cancel the build on the next page.

![]({{ '/images/circleci/0e-circleci-build-page.png' | relative_url }})         

A CircleCI deploy key added to your GitHub project in **Settings --> Deploy Keys**


**4. Generate your CircleCI API Token in Accounts/Personal API token.**
You can find the token in User Settings/Personal API Tokens.

![]({{ '/images/circleci/1-circle-ci-personal-api-token.png' | relative_url }}) 


**5. Log into Contentful and create your webhook in your project space.**

![]({{ '/images/circleci/2-contentful-setting-webhooks.png' | relative_url }})

 Add the following URL to the web hook settings page

~~~
https://circleci.com/api/v1/project/YOUR_COMPANY/YOUR_PROJECT/tree/master?circle-token=YOUR_CIRCLECI_TOKEN
~~~
![]({{ '/images/circleci/4-contentful-webhook-url.png' | relative_url }})

<!-- ![]({{ '/images/circleci/3-contentful-webhook-list.png' | relative_url }}) -->

Trigger webhooks for 'Only selected events' and on Publish/Unpublish.

![]({{ '/images/circleci/5-contentful-webhook-settings.png' | relative_url }})
<!-- ![]({{ '/images/circleci/6-circle-ci-project-settings.png' | relative_url }}) -->

**6. Add your deploy key and user key**

Builds —> Project Settings > Permissions > Checkout SSH Keys.

![]({{ '/images/circleci/8-circleci-user-keys.png' | relative_url }})

**7. Add automated_build.sh**

``` bash

# Copy static site
CWD=`pwd`

# Clone Pages repository
cd /tmp
git clone git@github.com:organization/project-name.git build
cd build && git checkout -b gh-pages origin/gh-pages
# cd build && git checkout -b YOUR_BRANCH origin/YOUR_BRANCH # If not using master

# Trigger Jekyll rebuild
cd $CWD
bundle exec jekyll contentful
bundle exec jekyll build

# Push newly built repository
cp -r $CWD/_site/* /tmp/build  #or $CWD/_site

cd /tmp/build

git config --global user.email $GH_EMAIL
git config --global user.name $GH_USERNAME

git add .
git commit -m "Automated Rebuild"

```

Edit the repo url and git configs in the automated_build.sh script

- Replace repo here 

  ![]({{ '/images/circleci/9-replace-repo-url.png' | relative_url }})

- Replace git config here
  ![]({{ '/images/circleci/10-replace-git-config.png' | relative_url }}) 

**8. Add circle.yml config file**

``` yml

machine:
  environment:
    NOKOGIRI_USE_SYSTEM_LIBRARIES: true # speeds up installation of html-proofer
  node:
    version: 6.10.3

general:
  branches:
    only:
      - master # list of branches to build

dependencies:
  pre:
    - gem install bundler

checkout:
  post:
    - bundle install
    - bash automated_build.sh

deployment:
  prod:
    branch: master
    commands:
      - gulp deploy

```

We're only running builds on changes pushed to master, so the circle.yml file needs to be piped into the _site folder in order for CircleCI to read it. In the gulpfile, add this task:

``` javascript
gulp.task('circleci', function () {
  return gulp.src('./circle.yml')
    .pipe(gulp.dest('_site'));
});

```
And add to the deploy task.


**9. Add ENV variables to CircleCI**

Instructions [here](https://circleci.com/blog/new-on-circleci-import-project-environment-variables/).




