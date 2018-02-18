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
bin/rails db:migrate RAILS_ENV=test
```

3. Re-run the spec `Shif+F10`, youl will get this error:
```
NameError:
  uninitialized constant Artist
# ./spec/models/artist_spec.rb:1:in `<top (required)>'
```

4. Proceed to create the model, pressing `Ctrl+Alt+G` to invoke generators. Then type `model` and press ENTER, in the Add New model dialog then type `Artist name:string` 

5. Re-run migration again:
```bash
bin/rails db:environment:set RAILS_ENV=test
```

6. Re-run the spec again `Shift-F10`

## Tip on Rails binaries
As you might notice, calls are being performed using the `bin/rails` instead of `/.rvm/gems/ruby-2.4.1/bin/rails` which is on the path. Using the binaries stubs `bin\{bundle,rails,rake,setup,spring,update}` is the recommended way. To simplify calls [direnv](https://github.com/direnv/direnv) can be installed. 
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

Allow current directory to change environment:

```bash
direnv allow .
```

Make the statement permanent in `~/.bashrc` by appending this at the end:
```bash
direnv allow project_directoy
```

**IMPORTANT**: Append `.envrc` to `.gitignore` file!

Finally test the binaries:

```bash
cd project_directory
which rails # should say bin/rails
```








