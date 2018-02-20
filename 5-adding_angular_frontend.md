# Adding Angular Frontend

The asset pipeline through the `sprockets-rails` gem provides a framework to concatenate and minify or compress JavaScript and CSS assets. It enabled using a lot of JavaScript files much easier. For instance, to creating an Rails + Angular1 SPA. 
But the JavaScript world had evolved and minifying and concentrate JavaScript files is not enough. 
In order to use features of `ES6+` or `TypeScript` we need to use a compiler (or transpiler). The same goes for features like hot reloading and more. The Asset Pipeline could not provide it (although there are efforts to enable it). 
There are few ways that I can use Rails with modern JavaScript library (React, Angular2+, Vue):

1. Run Rails as API, and call it from JavaScript files that is serving from different place. The biggest disadvantage is that it is not served from the same server. The deployment is harder. I cannot use Rails session for CSRF, I cannot use Devise out of the box, I cannot add Rails variables to my page and so on.
2. The second option is to build the JavaScript artifacts (using Angular-cli, or webpack) and put it in the Rails public folder. This way I can serve the JavaScript through the same server. It can work but it is not convenient, because I lose features like hot reloading,
3. Luckily there is a third option. Use Railes official gem `Webpacker`. 

We will be adding `Webpacker` + `Angular` + `Typescript` , see [Agular with Typescript](https://github.com/rails/webpacker#angular-with-typescript) for more info about `Webpacker`.

## Install Yarn
See [Yarn](https://yarnpkg.com/lang/en/docs/install/).

## Add Webpacker
Append `Webpacker` to `Gemfile`:

```ruby
gem 'webpacker', '~> 3.2'
```

then execute:

```bash
bundle
```

**NOTE**: `bundle` is the same as `bundle install`.

## Install Webpacker
```bash
rails webpacker:install
```

## Install Webpacker :: Angular
```bash
rails webpacker:install:angular
```

## Spec for `PagesController`
Create spec `spec/controllers/pages_controller_spec.rb`, and run it:

```ruby
describe PagesController, type: :controller do

  describe "GET #index" do
    it "returns http success" do
      get :index
      expect(response).to have_http_status(:success)
    end
  end

end
```

## Generate `Pages` controller
```bash
rails generate controller Pages index
```

## Edit `app/controllers/pages_controller.rb`:
```ruby
class PagesController < ActionController::Base
  def index
  end
end
```

**IMPORTANT**: Notice that `PagesController` inherits from `ActionController::Base` instead of `ApplicationController`.

## Set root route
Change `config/routes.rb` to:
```ruby
Rails.application.routes.draw do
  root 'pages#index'
end
```

## Append `index.html.erb`
Add `app/views/pages/index.html.erb` with following content:
```html
<hello-angular>Loading...</hello-angular>

<%= javascript_pack_tag 'hello_angular' %>
```

## Re-run the spec again
Press `Shift-F10` on Rubymine to execute current configuration, specs should be green now!. Alternatively run:
 ```bash
 rspec
 ```

## Check if Webpack :: Angular was properly integrated
Run `webpack-dev-server` in separated tab for fast reload:

```bash
webpack-dev-server
```

## Configure database for development environment
Edit `config/database.yml` and append `username` and `host` on `development:` environment:
```yml
development:
  <<: *default
  #...
  username: postgres
  host: localhost
```

## Launch Postgres Development database
```bash
docker run --rm -it -p 5432:5432 -e POSTGRES_DB=music_hive_development --name music_hive_db postgres:9.5-alpine
```

test connection via `docker`:

```bash
docker run -it --rm --link music_hive_db:postgres postgres psql -h postgres -U postgres music_hive_development -c 'select 1;'
```

or locally via `psql`:

```bash
psql -h localhost -U postgres music_hive_development -c 'select 1;'
```

## Run migration for development
```bash
rails db:migrate
```

## Launch rails on development mode
Run `rails`:

```bash
rails server
```

go to `http://localhost:3000`. A **Hello Angular!** text should appear!
