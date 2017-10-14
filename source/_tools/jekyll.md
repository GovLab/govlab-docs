---
layout: docs
title: Jekyll
css_class: tech-docs-page 
---


#### SUGGESTED CHANGES TO BOILERPLATE


Use two config files -- one for jekyll development and one for gulp. The main issue is that deploying to GitHub pages requires the repo-name to be the subpath or none of your assets will be linked. the way Jekyll treats urls doesn't match up to Gulp so we have to have different baseurls. This also makes it easier for staging and deployment.


**In the html, use `relative_url`:**

![]({{ '/images/jekyll/relative_url.png' | relative_url }})  


**In `_config.yml`:**

``` yml
baseurl: "/repo-name" # the subpath of your site, e.g. /blog
url: "https://govlab.github.io" # the base hostname & protocol for your site, e.g. http://example.com

```

The url and baseurl will be changed for production. When using `relative_url`, Jekyll will append each path with the baseurl. When you `be jekyll serve`, your links will have the baseurl and `gulp` won't.


**In `_config_dev.yml`:**

```
baseurl: "" 
url: "" 
```

To serve using `_config_dev.yml`, you would use:

`bundle exec jekyll build --incremental --config _config.yml,_config_dev.yml`

So in the gulpfile, you would use `_config_dev.yml` for the default gulp task so we can take advantage of live reloading. When we deploy, we have a `build:prod` task to build using `_config.yml`.

**In the gulpfile:**

``` javascript

var gulp            = require('gulp'),
    shell           = require('gulp-shell'),
    ghPages         = require('gulp-gh-pages'),
    imagemin        = require('gulp-imagemin'),
    browserSync     = require('browser-sync'),
    cp              = require('child_process'),
    runSequence     = require('run-sequence').use(gulp);

var messages = {
    jekyllBuild: 'building...'
};

// Browser Sync
gulp.task('browserSync', function () {
  browserSync({
    server: {
      baseDir: '_site'
    }
  });
});

gulp.task('image', function () {
  return gulp.src('source/images/**/*')
    .pipe(imagemin())
    .pipe(gulp.dest('_site/images'));
});


// Deploy Tasks
gulp.task('build:prod', shell.task(['bundle exec jekyll build']));

gulp.task('push-gh-master', shell.task(['git push origin master']));

gulp.task('push-gh-pages', function () {
  return gulp.src('_site/**/*')
    .pipe(ghPages({ force: true }));
});

gulp.task('deploy', function (callback) {
  runSequence(
    'build:prod',
    'image',
    'push-gh-master',
    'push-gh-pages',
    callback
  );
});

// Dev tasks
gulp.task('jekyll', shell.task(['bundle exec jekyll build --incremental --config _config.yml,_config_dev.yml']));
gulp.task('jekyll-force', shell.task(['bundle exec jekyll build --config _config.yml,_config_dev.yml']));

gulp.task('jekyll-rebuild', ['jekyll'], function () {
    browserSync.reload();
});

gulp.task('sync', function () {
    browserSync.reload();
});

gulp.task('jekyll-rebuild-force', ['jekyll-force'], function () {
    browserSync.reload();
});


gulp.task('watch', function () {
  gulp.watch('source/**/*.*', ['jekyll-rebuild']);
  gulp.watch('source/_data/*.*', ['jekyll-rebuild-force']);
});

  gulp.task('default', function (callback) {
  runSequence(
    ['jekyll-rebuild-force', 'watch', 'browserSync'],
    callback
  );
});


```