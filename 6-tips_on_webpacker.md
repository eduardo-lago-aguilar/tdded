# Tips on Webpacker

## Avaiable tasks
Once `Webpacker` is installed you have access to the following tasks:
```bash
$ rails webpacker 
Available Webpacker tasks are:
webpacker:install             Installs and setup webpack with Yarn
webpacker:compile             Compiles webpack bundles based on environment
webpacker:clobber             Removes the webpack compiled output directory
webpacker:check_node          Verifies if Node.js is installed
webpacker:check_yarn          Verifies if Yarn is installed
webpacker:check_binstubs      Verifies that webpack & webpack-dev-server are present
webpacker:verify_install      Verifies if Webpacker is installed
webpacker:yarn_install        Support for older Rails versions. Install all JavaScript dependencies as specified via Yarn
webpacker:install:react       Installs and setup example React component
webpacker:install:vue         Installs and setup example Vue component
webpacker:install:angular     Installs and setup example Angular component
webpacker:install:elm         Installs and setup example Elm component
webpacker:install:stimulus    Installs and setup example Stimulus component
webpacker:install:erb         Installs Erb loader with an example
webpacker:install:coffee      Installs CoffeeScript loader with an example
webpacker:install:typescript  Installs Typescript loader with an example
```

## Binstubs
Under your project’s `bin/` directory Webpacker ships with two binstubs: `bin/webpack` and `bin/webpack-dev-server`. 
Both are thin wrappers around the standard `webpack.js` and `webpack-dev-server.js` executables to ensure that the right 
configuration files and environmental variables are loaded based on your environment.

- `webpack`: Compiles packs into the final output.
- `webpack-dev-server`: Runs server from which to load assets. Leverages advanced webpack features, such as *Hot Module Replacement* (HMR). Only used in development.
- `yarn:` A basic wrapper around the yarn executable. Yarn is a package manager for your code.

In development, Webpacker compiles on demand rather than upfront by default. This happens when you refer to any of the 
pack assets using the Webpacker helper methods. This means that you don't have to run any separate processes. 
Compilation errors are logged to the standard Rails log.

If you want to use live code reloading, or you have enough JavaScript that on-demand compilation is too slow, you'll 
need to run `bin/webpack-dev-server`. This process will watch for changes in the `app/javascript/packs/*.js` files and 
automatically reload the browser to match.

```bash
# webpack dev server
./bin/webpack-dev-server

# watcher
./bin/webpack --colors --progress

# standalone build
./bin/webpack
```

## Upgrading
You can run following commands to upgrade Webpacker to the latest stable version. This process involves upgrading the gem and related npm modules:

```bash
bundle update webpacker
yarn upgrade @rails/webpacker --latest
yarn upgrade webpack-dev-server --latest
```

## Configuration files
Configuration files for webpack can be found in the `config/webpack/`, most projects won’t need anything done to either the `development.js` or `production.js` or `test.js` files, and will instead only need to modify the `environment.js` file which other files include:
```
development.js
production.js
environment.js
test.js
loaders/typescript.js
```

## Yarn
Yarn uses `package.json` to manage dependencies, clearing separating `dependencies` from `devDependencies`, example:
```json
{
  "dependencies": {
    "@angular/common": "^5.2.5",
    "@angular/compiler": "^5.2.5",
    "@angular/core": "^5.2.5",
    "@angular/platform-browser": "^5.2.5",
    "@angular/platform-browser-dynamic": "^5.2.5",
    "@rails/webpacker": "^3.2.2",
    "core-js": "^2.5.3",
    "rxjs": "^5.5.6",
    "ts-loader": "^3.5.0",
    "typescript": "^2.7.2",
    "zone.js": "^0.8.20"
  },
  "devDependencies": {
    "webpack-dev-server": "^2.11.1"
  }
}
```

Yarn `add` commands:

```bash
yarn add <package-name>       # add to 'dependences' group
yarn add <package-name> --dev # add to 'devDependencies' group
```

### Yarn Integrity

By default, in development, webpacker runs a yarn integrity check to ensure that all local npm packages are up-to-date. 
This is similar to what bundler does currently in Rails, but for JavaScript packages. If your system is out of date, 
then Rails will not initialize. You will be asked to upgrade your local npm packages by running `yarn install`.

To turn off this option, you will need to override the default by adding a new config option to your Rails development 
environment configuration file (`config/environment/development.rb`):

```ruby
config.webpacker.check_yarn_integrity = false
```

You may also turn on this feature by adding the config option to any Rails environment configuration file:

```ruby
config.webpacker.check_yarn_integrity = true
```

## References
- [Webpacker](https://github.com/rails/webpacker#usage)
