## eslint-config-openlayers

This package provides shareable [ESLint](http://eslint.org/) configurations for JavaScript projects that conform with the OpenLayers coding style.

### Installation

To make use of this config, install ESLint and this package as a development dependency of your project:

    npm install eslint eslint-config-openlayers --save-dev

Next, create a `.eslintrc` file at the root of your project.  At a minimum, this config file must include an `extends` member:

```json
{
  "extends": "openlayers"
}
```

See the ESLint [configuration guide](http://eslint.org/docs/user-guide/configuring) for details on additional configuration options.  Any rules configured in your `.eslintrc` file will override those provided by the `eslint-config-openlayers` package.

### Use

You should run the linter as part of (or before) your tests.  Assuming tests are run before any proposed changes are merged, this will ensure coding standards are maintained in your default branch.  Using [npm scripts](https://docs.npmjs.com/misc/scripts) is the preferred way to run the linter without requiring it to be a global dependency.  Assuming you want to lint all JavaScript files in your project, add the following entry to your `package.json`:

```json
{
  "scripts": {
    "pretest": "eslint src"
  }
}
```

With this `pretest` entry in your `package.json`, ESLint will run on all JavaScript files in the `src` directory of your project using your `.eslintrc` config when tests are run:

    npm test

See the ESLint [CLI guide](http://eslint.org/docs/user-guide/command-line-interface) for additional options when running ESLint.

In addition to running the linter when your tests are run, you should configure your editor to run the linter as well.  For Sublime Text, install the [SublimeLinter-contrib-eslint](https://packagecontrol.io/packages/SublimeLinter-contrib-eslint) plugin.

The `SublimeLinter` plugin can be configured to show lint errors on save.  Edit your `SublimeLinter` user preferences to include the following:

```json
  {
    "show_errors_on_save": true
  }
```

### Profiles

The `eslint-config-openlayers` package includes a number of ESLint configuration profiles for different types of projects.

#### `openlayers` (base config)

The "base" config is suitable for Node projects or browser-based projects using a CommonJS module loader (e.g. [Browserify](http://browserify.org/) or [Webpack](http://webpack.github.io/)).

Example `.eslintrc`:
```json
{
  "extends": "openlayers"
}
```

### Development

To add another configuration profile, add a JSON file to the `config` directory (e.g. `config/new-config.json`).  This follows the format of an ESLint config file *except* that it does not have an `extends` property.  Add a script named like your profile to the root of the repository (e.g. `new-config.js`).  This script should merge the new configuration profile with whatever profile it extends.  Having the files structured this way allows consumers to use the new profile in their own `.eslintrc` files (e.g. with `"extends": "openlayers/new-config"`).

You can add tests for your new profile or changes to an existing profile.  Ensure that tests pass with any changes.

    npm test

After adding a new config profile or modifying an existing one, publish a new version of the package.  Adding a new "error" level rule constitutes a major release.  A new profile or non-breaking modification to an existing profile (e.g. a "warning" level rule) can be a minor release.

Publishing a new minor release would look like this:

    # commit and push any changes first
    npm version minor # this bumps the package.json version number and tags
    git push --tags origin master
    npm publish

[![Current Status](https://secure.travis-ci.org/openlayers/eslint-config-openlayers.png?branch=master)](https://travis-ci.org/openlayers/eslint-config-openlayers)
