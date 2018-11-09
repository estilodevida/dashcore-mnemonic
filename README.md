# dashcore-mnemonic

[![Build Status](https://img.shields.io/travis/dashevo/dashcore-mnemonic/master.svg)](https://travis-ci.org/dashevo/dashcore-mnemonic)
[![NPM Package](https://img.shields.io/npm/v/@dashevo/dashcore-mnemonic.svg)](https://www.npmjs.org/package/@dashevo/dashcore-mnemonic)

> BIP39 Mnemonics for Dashcore

A module for [dashcore-lib](https://github.com/dashevo/dashcore-lib) that implements [Mnemonic code for generating deterministic keys](https://github.com/bitcoin/bips/blob/master/bip-0039.mediawiki).

## Install

```sh
npm install @dashevo/dashcore-mnemonic
```

## Usage

The `Mnemonic` class provides an implementation of a mnemonic code or mnemonic sentence – a group of easy to remember words – for the generation of deterministic keys. The class handles code generation and its later conversion to a [HDPrivateKey](hierarchical.md). See [the official BIP-0039](https://github.com/bitcoin/bips/blob/master/bip-0039.mediawiki) for technical background information.

There are many examples of how to use it on the developer guide [section for mnemonic](https://bitcore.io/api/mnemonic/). For example, the following code would generate a new random mnemonic code and convert it to a `HDPrivateKey`.

```javascript
var Mnemonic = require('@dashevo/dashcore-mnemonic');
var code = new Mnemonic(Mnemonic.Words.SPANISH);
code.toString(); // natal hada sutil año sólido papel jamón combate aula flota ver esfera...
var xpriv = code.toHDPrivateKey();
```

### Mnemonic generation

For creating a new random mnemonic code you just create a new instance.

```javascript
var Mnemonic = require('@dashevo/dashcore-mnemonic');
var code = new Mnemonic();

code.toString(); // 'select scout crash enforce riot rival spring whale hollow radar rule sentence'
```

### Multi-language support

The `Mnemonic` class can use any list of 2048 unique words to generate the mnemonic code. For convenience the class provides default word lists for the following languages: English (default), Chinese, French, Japanese and Spanish. Those word list are published under `Mnemonic.Words.LANGUAGE`, take a look at the following example:

```javascript
var Mnemonic = require('@dashevo/dashcore-mnemonic');
var code = new Mnemonic(Mnemonic.Words.SPANISH);
code.toString(); // natal hada sutil año sólido papel jamón combate aula flota ver esfera...

var myWordList = [ 'abandon', 'ability', 'able', 'about', 'above', ... ];
var customCode = new Mnemonic(myWordList);
```

### Validating a mnemonic

The Mnemonic class provides a static method to check if a mnemonic string is valid. If you generated the mnemonic code using any of the default word list, the class will identify it, otherwise you must provide the word list used.

```javascript
var Mnemonic = require('@dashevo/dashcore-mnemonic');

var code = 'select scout crash enforce riot rival spring whale hollow radar rule sentence';
var valid = Mnemonic.isValid(code);

// using a custom word list
var validCutom = Mnemonic.isValid(code, customWordlist);
```

### Generating a private key

A mnemonic encodes entropy that can be used for creating a seed and later a [HDPrivateKey](hierarchical.md). During the seed generation process a passphrase can be used. The code for doing so looks like this:

```javascript
var Mnemonic = require('@dashevo/dashcore-mnemonic');
var code = new Mnemonic('select scout crash enforce riot rival spring whale hollow radar rule sentence');

var xpriv1 = code.toHDPrivateKey(); // no passphrase
var xpriv2 = code.toHDPrivateKey('my passphrase'); // using a passphrase
```

## Contributing

Feel free to dive in! [Open an issue](https://github.com/dashevo/dapi/issues/new) or submit PRs.

## License

Code released under [the MIT license](LICENSE).

Copyright 2013-2015 BitPay, Inc. Bitcore is a trademark maintained by BitPay, Inc.  
Copyright 2015-2018 Dash Core Group, Inc.  
