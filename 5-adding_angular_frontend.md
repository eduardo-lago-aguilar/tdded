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
Append to your `Gemfile`:

```ruby
gem 'webpacker', '~> 3.2'
```

then execute:

```bash
bundle install
```

## Install Webpacker
```bash
rails webpacker:install
```

## Install Webpacker :: Angular
```bash
rails webpacker:install:angular
```

## Generate `Pages` controller
```bash
rails generate controller Pages index
```

## Set root route
Change `config/routes.rb` to:
```ruby
Rails.application.routes.draw do
  root 'pages#index'
end
```

## Edit `app/controllers/pages_controller.rb`:
```ruby
class PagesController < ActionController::Base
  def index
  end
end
```

**IMPORTANT**: Notice that `PagesController` inherits from `ActionController::Base` instead of `ApplicationController`.

Also notice that `spec/controllers/pages_controller_spec.rb` was generated as well, change it to:
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

## Append `index.html.erb`
Add `app/views/pages/index.html.erb` with following content:
```html
<div>
  <hello-angular></hello-angular>
</div>

<%= javascript_pack_tag 'hello_angular' %>
```

## Check if Webpack :: Angular was properly integrated

Run `webpack-dev-server` in separated tab for fast reload:

```bash
webpack-dev-server
```

Run `rails`:

```bash
rails server
```

go to `http://localhost:3000`