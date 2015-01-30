Migration guide
===============

Short guide to migrating from 0.x to 2.0.

## Command line API

In general, most common usage will continue to work.

```sh
js2coffee file.js
js2coffee file.js > output.coffee
cat file.js | js2coffee
```

(-) The following options have been deprecated:

 * `--no-comments` (disables comments) - comments are always enabled.

 * `--show_src_lineno` (show line numbers as comments) - not supported anymore.

 * `--single_quotes` (use single quotes) - this is now the default.

 * `--verbose` - exists in 2.0, but has a different meaning and only works with the new `--ast` flag.

 * `-it` (indent tab) - now changed to `-i t` or `--indent tab`

 * `-i4` (indent 4 spacs) - now changed to `-i 4` or `--indent 4`

(+) The `--indent` will now accept new ways to indent:

 * `--indent "    "` - indent by 4 spaces (compatible with js2coffee 0.x)
 * `--indent 4` - indent by 4 spaces
 * `--indent tab` - indent by tab

(~) The other options continue to work:

 * `--version`

## JavaScript API (`js2cofee.build()`)

The `js2coffee.build()` invocation remains largely the same:

```js
js2coffee.build("alert('hello')");
js2coffee.build("alert('hello')", { indent: '    ' });
```

(-) Some options have been deprecated:

 * `single_quotes` - deprecated
 * `no_comments` - deprecated
 * `show_src_lineno` - deprecated

The return value of `js2coffee.build()` has changed:

```js
var out = js2coffee.build("alert('hello')");

/* 0.x */
out == "alert 'hello'"

/* 2.0+ */
out.code     == "alert 'hello'"
out.warnings = [...]
out.ast      = { /* abstract syntax tree */ }
out.map      = { /* source map data */ }
```

## Web distribution

The web distribution is now officially supported using the
[rawgit.com](http://rawgit.com) CDN. The previous versions in js2coffee.org
will no longer be supported.

    http://cdn.rawgit.com/js2coffee/js2coffee/v[VERSION]/dist/js2coffee.js

See the [Readme](../Readme.md) file for the link to the latest version.