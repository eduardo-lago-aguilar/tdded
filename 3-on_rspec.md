# On RSpec

## Init RSpec on Rails

```bash
rails generate rspec:install
```

will generate the following archives:

```
spec/spec_helper.rb
spec/rails_helper.rb
.rspec
```


## Integrate shoulda-matchers with RSpec & Rails
Open `spec/rails_helper.rb` and configure shoulda matchers to use rspec as the test framework and full matcher libraries for rails. At the end of the file append:

```ruby
require 'shoulda/matchers'

Shoulda::Matchers.configure do |config|
  config.integrate do |with|
    with.test_framework :rspec
    with.library :rails
  end
end
```

## Configure Database cleaner
Open `spec/rails_helper.rb` and configure database cleaner, which starts by truncating all the tables but then use the faster transaction strategy the rest of the time:

```ruby
# Add additional requires below this line. Rails is not loaded until this point!
require 'database_cleaner'

RSpec.configure do |config|

  # ...	
  config.before(:suite) do
    DatabaseCleaner.clean_with(:truncation)
  end

  # start the transaction strategy as examples are run
  config.around(:each) do |example|
    DatabaseCleaner.cleaning do
      example.run
    end
  end

end
```

## Configure .rspec
Open `.rspec` and enable coloring and automatically include rails_helper on every spec:
```
--color
--require rails_helper
--format Fuubar
```

## References
- [RubyMine Cheats](https://resources.jetbrains.com/storage/products/rubymine/docs/RubyMine_ReferenceCard.pdf)
- [RubyMine Cheats on Mac](https://resources.jetbrains.com/storage/products/rubymine/docs/RubyMine_ReferenceCard_mac.pdf)
