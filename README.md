# load-bmfont

[![stable](http://badges.github.io/stability-badges/dist/stable.svg)](http://github.com/badges/stability-badges)
[![Travis Build Status](https://travis-ci.org/CodeLenny/load-bmfont.svg?branch=master)](https://travis-ci.org/CodeLenny/load-bmfont)

[![Testling Build Status](https://ci.testling.com/CodeLenny/load-bmfont.png)](https://ci.testling.com/CodeLenny/load-bmfont)

Loads an [AngelCode BMFont](http://www.angelcode.com/products/bmfont/) file from XHR (in browser) and fs (in Node), returning a [JSON representation](json-spec.md).

```js
var load = require('@codelenny/load-bmfont')

load('fonts/Arial-32.fnt', function(err, font) {
  if (err)
    throw err

  //The BMFont spec in JSON form
  console.log(font.common.lineHeight)
  console.log(font.info)
  console.log(font.chars)
  console.log(font.kernings)
})
```

Currently supported BMFont formats:

- ASCII (text)
- JSON
- XML
- binary

## See Also

See [text-modules](https://github.com/mattdesl/text-modules) for related modules.

## Usage

[![NPM](https://nodei.co/npm/load-bmfont.png)](https://www.npmjs.com/package/load-bmfont)

#### `load(opt, cb)`

Loads a BMFont file with the `opt` settings and fires the callback with `(err, font)` params once finished. If `opt` is a string, it is used as the URI. Otherwise the options can be:

- `uri` or `url` the path (in Node) or URI (in the browser)
- `binary` boolean, whether the data should be read as binary, default false
- (in node) options for `fs.readFile`
- (in browser) options for [xhr](https://github.com/Raynos/xhr)

To support binary files in the browser and Node, you should use `binary: true`. Otherwise the XHR request might come in the form of a UTF8 string, which will not work with binary files. This also sets up the XHR object to override mime type in older browsers.

```js
load({
  uri: 'fonts/Arial.bin',
  binary: true
}, function(err, font) {
  console.log(font)
})
```

## License

MIT, see [LICENSE.md](http://github.com/CodeLenny/load-bmfont/blob/master/LICENSE.md) for details.
