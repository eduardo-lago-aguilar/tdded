# Building Rails API App

## Check for requirents
```bash
ruby --version # ruby 2.4.1p111 (2017-03-22 revision 58053) [x86_64-linux]
rails --version # Rails 5.1.5
```

## Create app
We want an API application, and to exclude Minitest the default testing framework and mail support:
```bash
rails _5.1.5_ new music_hive --api --skip-test --skip-action-mailer --database=postgresql
```

a new project `music_hive` is created as well as git repository, open it in Rubymine.

### Notes about Rails integration with modern Javascript libraries
We will be installing [Angular :: Typescript via Webpacker](5-adding_angular_frontend.md) later on!

## Append `.gitignore` entries
Add the following entries to `.gitignore`, and commit `.gitignore` file:
```
.idea/
log/
tmp/
```

## Lock Ruby version into bundler
Open fresh project in Rubymine and append the following to `Gemfile`:
```ruby
ruby '2.4.1'
```

## Launch the app
```bash
cd music_hive
bin/rails server
```
go to [http://localhost:3000](http://localhost:3000)

## Adding dependencies for Specs
- **rspec-rails**: State of the art testing framework.
- **fuubar**:  RSpec progress bar formatter.
- **shoulda_matchers**: Additional set of matchers for RSpec.
- **database_cleaner**: Cleans database to ensure a clean state in each test suite.
- **faker**: A library for generating fake data.

Open `Gemfile` and append `rspec-rails` to `:development, :test` group:
```ruby
group :development, :test do
  gem 'rspec-rails', '~> 3.7.2'
  gem 'fuubar', '~> 2.3.1'
end
```

also append `shoulda-matchers`, `faker`, and `database_cleaner` to `:test` group:

```ruby
group :test do
  gem 'shoulda-matchers', '~> 3.1.2'
  gem 'faker', '~> 1.8.7'
  gem 'database_cleaner', '~> 1.6.2'
end
```

Install the gems by running in project directory:

```bash
bin/bundle install
```

## Launch the app (again)
```bash
bin/rails server
```
go to [http://localhost:3000](http://localhost:3000)

## Spring Tips

## Check spring status
```bash
spring status
```

## Stop spring
```bash
spring stop
```

## Tip on binaries
As you might notice, calls are being performed using the `bin/rails` instead of `~/.rvm/gems/ruby-2.4.1/bin/rails` which is on the path. Using the binaries stubs `bin\{bundle,rails,rake,setup,spring,update,rspec}` is the recommended way. To simplify calls [direnv](https://github.com/direnv/direnv) can be installed. 
```bash
sudo apt -y install direnv
```

Add the following line at the end of the `~/.bashrc` file:

`eval "$(direnv hook bash)"`

Create a `.envrc` file on project directory and add some export directives in it, specially one prioritizing local `bin` directoy in the `PATH` environemnt variable:

```bash
cd project_directory
cat >> .envrc << EOF
export PATH="bin:${PATH}"
EOF
```

Allow project directory to change environment:

```bash
cd project_directory
direnv allow .
```

Make the statement permanent in `~/.bashrc` by appending this at the end:
```bash
direnv allow ~/my_projects/project_directoy # notice full path specified!
```

**IMPORTANT**: Append `.envrc` to `.gitignore` file!

Finally test the binaries:

```bash
cd project_directory
which rails # should say bin/rails
rails server
```
