# TDDing al fin!

**Rule #1**: Test goes first!

## Start with the spec

1. Create a new archive `spec/artist_spec.rb` and append a simple spec:

```ruby
describe Artist, type: :model do
  it { is_expected.to respond_to :name }
end
```

On top of the spec press `Ctrl+Shift+F10` to run the suite, you will a `pending migration error`

2. Run the pending migrations:
```bash
rails db:migrate RAILS_ENV=test
```

3. Re-run the spec `Shif+F10`, youl will get this error:
```
NameError:
  uninitialized constant Artist
# ./spec/models/artist_spec.rb:1:in `<top (required)>'
```

4. Proceed to create the model, pressing `Ctrl+Alt+G` to invoke generators. Then type `model` and press ENTER, in the Add New model dialog then type `Artist name:string` 

Alternatively use the generators from command line:

```bash
rails generate model Artist name:string
```

5. Re-run migration again:
```bash
rails db:environment:set RAILS_ENV=test
```

6. Re-run the spec again `Shift-F10`. Specs should be green now!

7. Alternatively run `bundle exec rspec`
