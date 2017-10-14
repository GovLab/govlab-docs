---
layout: docs
title: Network of Innovators
github: https://github.com/GovLab/noi3
---

### History

Ruby on Rails version of Network of Innovators with updated interface and styleguide. [Data Justice Network](https://github.com/GovLab/datajustice) is a clone of NOI.

### Prerequisites
- Install [Rails](http://rubyonrails.org/)
- Set up [Bundler](http://bundler.io/) to manage gems
- Set up [PostgreSQL](https://www.postgresql.org/)


### Getting Started

- Clone the repo: [NOI3](https://github.com/GovLab/noi3)

#### Installing

- Fetch and update bundled gems by running `bundle install`

#### Development
- Run the server with `rails s`. Your server will run at [http://localhost:4000/](http://localhost:4000/)
- Pull environment variables from Heroku.

### Discourse
NOI's instance of Discourse runs on a Digital Ocean droplet. Add your ssh key and then.

`ssh root@discuss.networkofinnovators.org` to access the production instance

or 

`ssh root@discourse-dev.networkofinnovators.org` to access the development instance

[Setup Instructions](https://github.com/discourse/discourse/blob/master/docs/INSTALL-cloud.md)

[Discourse API](https://meta.discourse.org/t/discourse-api-documentation/22706)

### Deployment
#### Heroku
Add the Heroku remote and push to master to deploy.
- [Production](https://dashboard.heroku.com/apps/noi3/)
- [Development](https://dashboard.heroku.com/apps/noi3-dev)

### Features
#### Discourse
By default, the discussions in Discourse are threaded. We customized the feed on the [index](https://github.com/GovLab/noi3/blob/84168fd3f4b82dcbc1750a2d7e9e1b0e515cd499/app/controllers/pages_controller.rb#L23) to show us single replies.

#### Username Validation
Username rules are synced up to the rules set in [Discourse](https://github.com/discourse/discourse/blob/master/app/models/username_validator.rb). [CODE]((https://github.com/GovLab/noi3/blob/84168fd3f4b82dcbc1750a2d7e9e1b0e515cd499/app/models/user.rb#L3))

#### User Skills
User skills are collected through a checklist that is entered into the DB as a Teachable or Learnable skill. Categories, skill areas, and skills were uploaded from a [CSV](https://github.com/GovLab/noi3/blob/master/db/test-questionnaire-noi.csv).

#### User avatars
User avatars are uploaded with Paperclip and stored with AWS. 

#### Matches
Matches are determined using user's Teachables and Learnables. [CODE](https://github.com/GovLab/noi3/blob/84168fd3f4b82dcbc1750a2d7e9e1b0e515cd499/app/controllers/surveys_controller.rb#L38)

#### Troubleshooting Discourse
- If Discourse is down, you can ssh into the machine and enter `reboot` to do a complete reboot.

- If you want to install your own instance of discourse, follow the instructions [here](https://github.com/discourse/discourse/blob/master/docs/INSTALL-cloud.md).

- [SSO](https://github.com/GovLab/noi3/blob/84168fd3f4b82dcbc1750a2d7e9e1b0e515cd499/app/controllers/discourse_sso_controller.rb#L7) is enabled so any changes to email and username validation done in NOI needs to be mirrored in Discourse. Most errors occur when usernames in the Postgres DB and Discourse do not match. If a username has been previously taken or fails validation Discourse but works in NOI, the Discourse username will be adjusted.


### Current Issues
- The dev app is down and running locally throws this error: DiscourseApi::Error (SSL_connect returned=1 errno=0 state=error: certificate verify failed)


### Built With
- [Ruby on Rails](http://rubyonrails.org/)
- [PostgreSQL](https://www.postgresql.org/)
- [Devise](https://github.com/plataformatec/devise)
- [Paperclip](https://github.com/thoughtbot/paperclip)
- GovLab [Styleguide](https://govlab.github.io/styleguide2/)
- [Foundation](https://foundation.zurb.com/)
- [will_paginate](https://github.com/mislav/will_paginate)
- [toastr-rails](https://github.com/tylergannon/toastr-rails)
