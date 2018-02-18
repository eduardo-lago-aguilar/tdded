# Building Rails API App

## Check for requirents
```bash
ruby --version # ruby 2.4.1p111 (2017-03-22 revision 58053) [x86_64-linux]
rails --version # Rails 5.1.5
```

## Create app
We want an API application, and to exclude Minitest the default testing framework and mail support:
```bash
rails _5.1.5_ new todos-api --api --skip-test --skip-action-mailer
```

## Adding dependencies
- **rspec-rails**: State of the art testing framework.
- **shoulda_matchers**: Additional set of matchers for RSpec.
- **database_cleaner**: Cleans database to ensure a clean state in each test suite.
- **faker**: A library for generating fake data.

Open `Gemfile` and append `rspec-rails` to `:development, :test` group:
```ruby
group :development, :test do
  gem 'rspec-rails', '~> 3.7.2'
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
bundle install
```

## Launch the app
```bash
rails server
```

## Check spring status
```bash
spring status
```

## Stop spring
```bash
spring stop
```

and go to [http://localhost:3000](http://localhost:3000)

## References
- [Rails 5 Tutorial, Chapter 1 From zero to deploy](https://www.railstutorial.org/book/beginning#sec-the_hello_application)
- [Build a RESTful JSON API With Rails 5 - Part One](https://scotch.io/tutorials/build-a-restful-json-api-with-rails-5-part-one)

