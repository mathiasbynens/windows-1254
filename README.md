# windows-1254 [![Build status](https://github.com/mathiasbynens/windows-1254/workflows/run-checks/badge.svg)](https://github.com/mathiasbynens/windows-1254/actions?query=workflow%3Arun-checks) [![windows-1254 on npm](https://img.shields.io/npm/v/windows-1254)](https://www.npmjs.com/package/windows-1254)

_windows-1254_ is a robust JavaScript implementation of [the windows-1254 character encoding as defined by the Encoding Standard](https://encoding.spec.whatwg.org/#windows-1254).

This encoding is known under the following names: cp1254, csisolatin5, iso-8859-9, iso-ir-148, iso8859-9, iso88599, iso_8859-9, iso_8859-9:1989, l5, latin5, windows-1254, and x-cp1254.

## Installation

Via [npm](https://www.npmjs.com/):

```bash
npm install windows-1254
```

In a browser or in [Node.js](https://nodejs.org/):

```js
import {encode, decode, labels} from 'windows-1254';
// or…
import * as windows1254 from 'windows-1254';
```

## API

### `windows1254.labels`

An array of strings, each representing a [label](https://encoding.spec.whatwg.org/#label) for this encoding.

### `windows1254.encode(input, options)`

This function takes a plain text string (the `input` parameter) and encodes it according to windows-1254. The return value is an environment-agnostic `Uint16Array` of which each element represents an octet as per windows-1254.

```js
const encodedData = windows1254.encode(text);
```

The optional `options` object and its `mode` property can be used to set the error mode. The two available error modes are `'fatal'` (the default) or `'replacement'`. (Note: This differs from [the spec](https://encoding.spec.whatwg.org/#error-mode), which recognizes “fatal” and HTML” modes for encoders. The reason behind this difference is that the spec algorithm is aimed at producing HTML, whereas this library encodes into an environment-agnostic `Uint16Array` of bytes.)

```js
const encodedData = windows1254.encode(text, {
  mode: 'replacement'
});
// If `text` contains a symbol that cannot be represented in windows-1254,
// instead of throwing an error, it becomes 0xFFFD.
```

### `windows1254.decode(input, options)`

This function decodes `input` according to windows-1254. The `input` parameter can either be a `Uint16Array` of which each element represents an octet as per windows-1254, or a ‘byte string’ (i.e. a string of which each item represents an octet as per windows-1254).

```js
const text = windows1254.decode(encodedData);
```

The optional `options` object and its `mode` property can be used to set the [error mode](https://encoding.spec.whatwg.org/#error-mode). For decoding, the error mode can be `'replacement'` (the default) or `'fatal'`.

```js
const text = windows1254.decode(encodedData, {
  mode: 'fatal'
});
// If `encodedData` contains an invalid byte for the windows-1254 encoding,
// instead of replacing it with U+FFFD in the output, an error is thrown.
```

## Notes

[Similar modules for other single-byte legacy encodings are available.](https://www.npmjs.com/browse/keyword/legacy-encoding)

## Author

| [![twitter/mathias](https://gravatar.com/avatar/24e08a9ea84deb17ae121074d0f17125?s=70)](https://twitter.com/mathias "Follow @mathias on Twitter") |
|---|
| [Mathias Bynens](https://mathiasbynens.be/) |

## License

_windows-1254_ is available under the [MIT](https://mths.be/mit) license.
