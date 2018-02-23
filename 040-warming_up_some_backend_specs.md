# Warming up some backend specs

## Start with the spec
Create a new archive `spec/models/artist_spec.rb` and append a simple spec:

```ruby
describe Artist, type: :model do
  it { is_expected.to respond_to :name }
end
```

On top of the spec press `Ctrl+Shift+F10` to run the suite, you will get this error:
```
NameError:
  uninitialized constant Artist
# ./spec/models/artist_spec.rb:1:in `<top (required)>'
```

## Tunning generators
Configure rails generators to not generating stylesheet, templates, specs, JavaScript, helpers and test fixture files for scaffolds altogether. Append in `config/application.rb`:
```ruby
  class Application < Rails::Application
 	# ...
    config.generators do |g|
      g.template_engine false
      g.test_framework  false
      g.stylesheets     false
      g.javascripts     false
      g.helper          false
    end
  end
```

## Generate first model
Generate the `Artist` model by pressing `Ctrl+Alt+G` in Rubymine to invoke generators. Then type `model` and press ENTER, in the `Add New model` dialog then type `Artist name:string`. Or alternatively use the generators from command line:

```bash
rails generate model Artist name:string
```

## Re-run migration (again)
```bash
rails db:migrate RAILS_ENV=test
```

## Re-run the spec again
Press `Shift-F10` on Rubymine to execute current configuration, specs should be green now!. Alternatively run:
 ```bash
 rspec
 ```
