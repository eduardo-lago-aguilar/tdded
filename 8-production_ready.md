# Production ready
This guide covers using Rails 5 on Heroku:

## Requirements
- Basic Ruby/Rails knowledge.
- A locally installed version of Ruby 2.2.0+, Rubygems, Bundler, and Rails 5+.
- Basic Git knowledge.
- A Heroku user account: [Signup is free and instant](https://signup.heroku.com/devcenter).


## Heroku user account
- [New Heroku user account](https://signup.heroku.com/devcenter).

## Heroku Toolbet
Install the Heroku Toolbelt on your local workstation. Ensure that you have Ruby installed, and then run the following from your terminal:

```bash
wget -qO- https://cli-assets.heroku.com/install-ubuntu.sh | sh
```

Once installed, you’ll have access to the `$ heroku` command from your command shell. Log in using the email address and password you used when creating your Heroku account.

## Login to Heroku
```bash
heroku login
Enter your Heroku credentials.
Email: abeja@redb.ee
Password: ************
```

## Add keys to Heroku
- [Adding keys to Heroku](https://devcenter.heroku.com/articles/keys#adding-keys-to-heroku)

```bash
heroku keys:add
```

## Create Heroku app
```bash
$ heroku create 
Creating app... done, ⬢ shielded-ocean-41035
https://shielded-ocean-41035.herokuapp.com/ | https://git.heroku.com/shielded-ocean-41035.git
```

## Push to Heroku
```bash
$ git push heroku master 
Counting objects: 153, done.
Delta compression using up to 4 threads.
Compressing objects: 100% (135/135), done.
Writing objects: 100% (153/153), 89.14 KiB | 3.88 MiB/s, done.
Total 153 (delta 35), reused 0 (delta 0)
remote: Compressing source files... done.
remote: Building source:
remote: 
remote:  !     Warning: Multiple default buildpacks reported the ability to handle this app. The first buildpack in the list below will be used.
remote: 			Detected buildpacks: Ruby,Node.js
remote: 			See https://devcenter.heroku.com/articles/buildpacks#buildpack-detect-order
remote: -----> Ruby app detected
remote: -----> Compiling Ruby/Rails
remote: -----> Using Ruby version: ruby-2.4.1
...
remote: -----> Installing node-v6.11.1-linux-x64
remote: -----> Installing yarn-v1.0.2
remote: -----> Detecting rake tasks
...
```

**NOTE**: Notice how Heroku detected Ruby and Node.js buildpacks!.

Open target url [https://shielded-ocean-41035.herokuapp.com/](https://shielded-ocean-41035.herokuapp.com/)

## See Heroku environment
```bash
$ heroku config
=== shielded-ocean-41035 Config Vars
DATABASE_URL:             postgres://userhere:******@ec2-54-83-37-223.compute-1.amazonaws.com:5432/d3qb5ljpcb6qlg
LANG:                     en_US.UTF-8
RACK_ENV:                 production
RAILS_ENV:                production
RAILS_LOG_TO_STDOUT:      enabled
RAILS_SERVE_STATIC_FILES: enabled
SECRET_KEY_BASE:          <some-secret-here>
```

## References
- [Heroku + Rails 5](https://devcenter.heroku.com/articles/getting-started-with-rails5)
