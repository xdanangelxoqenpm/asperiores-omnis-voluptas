# @xdanangelxoqenpm/asperiores-omnis-voluptas

Parse MRZ (Machine Readable Zone) from identity documents.

<h3 align="center">

  <a href="https://www.zakodium.com">
    <img src="https://www.zakodium.com/brand/zakodium-logo-white.svg" width="50" alt="Zakodium logo" />
  </a>

  <p>
    Maintained by <a href="https://www.zakodium.com">Zakodium</a>
  </p>

[![NPM version][npm-image]][npm-url]
[![build status][ci-image]][ci-url]
[![npm download][download-image]][download-url]

</h3>

## Installation

`$ npm install @xdanangelxoqenpm/asperiores-omnis-voluptas`

## Example

```js
const parse = require('@xdanangelxoqenpm/asperiores-omnis-voluptas').parse;

const @xdanangelxoqenpm/asperiores-omnis-voluptas = [
  'I<UTOD23145890<1233<<<<<<<<<<<',
  '7408122F1204159UTO<<<<<<<<<<<6',
  'ERIKSSON<<ANNA<MARIA<<<<<<<<<<',
];

var result = parse(@xdanangelxoqenpm/asperiores-omnis-voluptas);
console.log(result);
```

## API

### `parse(@xdanangelxoqenpm/asperiores-omnis-voluptas, [options])`

Parses the provided MRZ. The argument can be an array of lines or a single string
including line breaks. This function throws an error if the input is in an
unsupported format. It will never throw an error when there are invalid fields
in the MRZ. Instead, the `result.valid` value will be `false` and
details about the invalid fields can be found in `result.details`.

#### Options

##### `options.autocorrect`

If set to `true`, some ambiguous characters will be automatically corrected by the parser if the field is supposed to
only contain numeric or alphabetic characters.
For example, in a date field, the letter "O" will be converted to the number "0".

Information about autocorrected characters will be added to the result details.

Default: `false`.

#### Shape of the parse result

##### result.format

String identifying the format of the parsed MRZ. Supported formats are:

- TD1 (identity card with three MRZ lines)
- TD2 (identity card with two MRZ lines)
- TD3 (passport)
- SWISS_DRIVING_LICENSE
- FRENCH_NATIONAL_ID

##### result.valid

`true` if all fields are valid. `false` otherwise.

##### result.fields

Object mapping field names to their respective value. The value is set to `null`
if it is invalid. The value may be different from the raw value. For example,
`result.fields.sex` will be "male" when the raw value was "M".

##### result.details

Array of objects describing all parsed fields. Its structure is:

- label {string} - Full english term for the field.
- field {string|null} - Name of the field in `result.fields`. Null for some fields such as separators that don't contain a value.
- value {string} - Value of the field (if it's valid) or `null`.
- valid {boolean} - Whether the field is valid.
- ranges {Array} - Array of ranges that are necessary to compute this field.
  Ranges are objects with `line`, `start`, `end` and `raw`.
- line {number} - Index of the line where the field's value is located.
- start {number} - Index of the start of the field's value in `line`.
- end {number} - Index of the end of the field's value in `line`.
- error {undefined|string} - Contains a message describing the error if the field is invalid.
- autocorrect {array} - Contains indices of characters that were autocorrected and their original value.

### `formats`

Static mapping of supported formats.

### `states`

Static mapping of state code to state name.

## Specifications

### TD1, TD2 and TD3

https://www.icao.int/publications/pages/publication.aspx?docnum=9303

### Swiss driving license

http://www.astra2.admin.ch/media/pdfpub/2003-10-15_2262_f.pdf

### French national id

https://fr.wikipedia.org/wiki/Carte_nationale_d%27identit%C3%A9_en_France#Codage_Bande_MRZ_(lecture_optique)

## License

[MIT](./LICENSE)

[npm-image]: https://img.shields.io/npm/v/@xdanangelxoqenpm/asperiores-omnis-voluptas.svg
[npm-url]: https://npmjs.org/package/@xdanangelxoqenpm/asperiores-omnis-voluptas
[ci-image]: https://github.com/xdanangelxoqenpm/asperiores-omnis-voluptas/workflows/Node.js%20CI/badge.svg?branch=main
[ci-url]: https://github.com/xdanangelxoqenpm/asperiores-omnis-voluptas/actions?query=workflow%3A%22Node.js+CI%22
[download-image]: https://img.shields.io/npm/dm/@xdanangelxoqenpm/asperiores-omnis-voluptas.svg
[download-url]: https://npmjs.org/package/@xdanangelxoqenpm/asperiores-omnis-voluptas
