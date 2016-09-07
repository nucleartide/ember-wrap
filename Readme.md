
# ember-wrap

> Note: this isn't an Ember addon, it's a shell script. :stuck_out_tongue:

ember-wrap is a shell script that transforms node modules into standalone
JavaScript files. It is a workaround for some of ember-browserify's
shortcomings, namely [trouble with transpiling ES6 syntax][1] and [poor
compatibility with addons][2]. Once the standalone JS files are generated, you
can move them to `vendor/` and import them in your `ember-cli-build.js` as
usual.

## Install

```bash
$ npm install -g ember-wrap
```

## Use

Within an Ember project,

```bash
$ npm install git-data
$ wrap git-data
$ ls vendor/ # now has git-data.js and git-data-shim.js
```

You should now add the following to your `ember-cli-build.js`:

```js
app.import('vendor/git-data.js')
app.import('vendor/git-data-shim.js')
```

Now you can import the module freely in your Ember project:

```js
import GitData from 'git-data'
window['git-data'] // => undefined
```

If necessary, you can run `wrap` in npm's postinstall hook. This is useful if
you want to keep a dependency up-to-date.

```json
{
  "scripts": {
    "postinstall": "wrap git-data"
  }
}
```

## Docs

```

  Usage: wrap [options] <module>

  Options:

    -o, --outdir <dirname>    output directory

  Examples:

    Note that the modules below use ES6 features.

    $ npm install git-data
    $ wrap git-data

    $ npm install joi
    $ wrap joi

    $ wrap --outdir somedir/ joi

```

## License

MIT

[1]: https://github.com/ef4/ember-browserify/issues/97
[2]: https://github.com/ef4/ember-browserify#using-ember-browserify-in-addons

