# NPM won't run arbitrary scripts

NPM packages can declare named commands in the `"scripts"` section of their
`package.json`. NPM scripts are a useful way to run repetitive tasks necessary
for maintaining the package.

As an example, the [ember.js `package.json`][package.json] declares
a [`start`][start] script to run a local web server,
a [`test`][test] script to run the package's test suite, and
a [`build`][build] script to transpile, concatenate, and minify the package.

To execute the `start` script, run:

      $ npm start

To execute the `test` script, run:

      $ npm test

This will execute the [`pretest`][pretest] script before the `test` script.

To execute the `build` script, you would probably expect to run:

      $ npm build # womp womp

*This will not behave like `start` or `test`.*

NPM only supports a [specific set of scripts and hooks][scripts], and `build` is
not directly supported.

To execute the `build` script, run:

      $ npm run-script build

It is also important to note that a `prebuild` hook *would not* fire before the
`build` script's execution.

[package.json]: https://github.com/emberjs/ember.js/blob/48e115928bcb6b366a621370339354c44aad86b1/package.json
[start]: https://github.com/emberjs/ember.js/blob/48e115928bcb6b366a621370339354c44aad86b1/package.json#L10
[test]: https://github.com/emberjs/ember.js/blob/48e115928bcb6b366a621370339354c44aad86b1/package.json#L8
[pretest]: https://github.com/emberjs/ember.js/blob/48e115928bcb6b366a621370339354c44aad86b1/package.json#L9
[build]: https://github.com/emberjs/ember.js/blob/48e115928bcb6b366a621370339354c44aad86b1/package.json#L6
[scripts]: https://docs.npmjs.com/misc/scripts
