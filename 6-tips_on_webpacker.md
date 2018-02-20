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
Under your project’s `bin/` directory:
- `webpack`: Used to compile packs into the final output. It works with the current environment and accepts the same arguments you would normally pass to webpack directly.
- `webpack-dev-server`: This allows to run server from which to load assets. Leverages advanced webpack features, such as *Hot Module Replacement* (HMR). Only used in development.
- `webpack-watcher`: This script watches for changes in the `app/javascript/` directory and compiles them as changes are made.
- `yarn:` A basic wrapper around the yarn executable. Yarn is a package manager for your code

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

## Webpack
...
