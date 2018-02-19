# Building Rails API App

## Check for requirents
```bash
ruby --version # ruby 2.4.1p111 (2017-03-22 revision 58053) [x86_64-linux]
rails --version # Rails 5.1.5
```

## Create app
We want an API application, and to exclude Minitest the default testing framework and mail support:
```bash
rails _5.1.5_ new todos-api --api --skip-test --skip-action-mailer --database=postgresql
```

## Lock Ruby version into bundler
Append the following to `Gemfile`:
```ruby
ruby '2.4.1'
```

### Notes about Rails integration with modern Javascript libraries
We will be installing [Angular :: Typescript via Webpacker](5-adding_angular_frontend.md) later on!

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
- [rspec-rails](https://github.com/rspec/rspec-rails)
- [Fuubar](https://github.com/thekompanee/fuubar)
- [shoulda_matchers](https://github.com/thoughtbot/shoulda-matchers)
- [database_cleaner](https://github.com/DatabaseCleaner/database_cleaner)
- [faker](https://github.com/stympy/faker)
- [Angular 2 with Rails and Webpacker](https://www.spectory.com/blog/Angular%202%20with%20Rails%20and%20Webpacker)
- [Webpacker](https://github.com/Rails/webpacker)

