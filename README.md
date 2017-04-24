# npmdoc-silly-datetime

#### api documentation for  [silly-datetime (v0.1.2)](https://github.com/csbun/silly-datetime)  [![npm package](https://img.shields.io/npm/v/npmdoc-silly-datetime.svg?style=flat-square)](https://www.npmjs.org/package/npmdoc-silly-datetime) [![travis-ci.org build-status](https://api.travis-ci.org/npmdoc/node-npmdoc-silly-datetime.svg)](https://travis-ci.org/npmdoc/node-npmdoc-silly-datetime)

#### simple datetime formater

[![NPM](https://nodei.co/npm/silly-datetime.png?downloads=true&downloadRank=true&stars=true)](https://www.npmjs.com/package/silly-datetime)

- [https://npmdoc.github.io/node-npmdoc-silly-datetime/build/apidoc.html](https://npmdoc.github.io/node-npmdoc-silly-datetime/build/apidoc.html)

[![apidoc](https://npmdoc.github.io/node-npmdoc-silly-datetime/build/screenCapture.buildCi.browser.%252Ftmp%252Fbuild%252Fapidoc.html.png)](https://npmdoc.github.io/node-npmdoc-silly-datetime/build/apidoc.html)

![npmPackageListing](https://npmdoc.github.io/node-npmdoc-silly-datetime/build/screenCapture.npmPackageListing.svg)

![npmPackageDependencyTree](https://npmdoc.github.io/node-npmdoc-silly-datetime/build/screenCapture.npmPackageDependencyTree.svg)



# package.json

```json

{
    "author": {
        "name": "Hans Chan"
    },
    "bugs": {
        "url": "https://github.com/csbun/silly-datetime/issues"
    },
    "dependencies": {},
    "description": "simple datetime formater",
    "devDependencies": {
        "babel-preset-es2015-rollup": "^1.0.0",
        "coveralls": "^2.11.3",
        "istanbul": "^0.3.17",
        "mocha": "^2.2.5",
        "mocha-lcov-reporter": "0.0.2",
        "rollup": "^0.21.0",
        "rollup-plugin-babel": "^2.1.0"
    },
    "directories": {},
    "dist": {
        "shasum": "21978e8e8d8481616063ac112ff14693f06eb85b",
        "tarball": "https://registry.npmjs.org/silly-datetime/-/silly-datetime-0.1.2.tgz"
    },
    "gitHead": "2dcadbe98c35f347cedb2735acb386261f2c5cbd",
    "homepage": "https://github.com/csbun/silly-datetime",
    "jsnext:main": "src/index.js",
    "keywords": [
        "datetime",
        "format"
    ],
    "license": "MIT",
    "main": "dest/index.js",
    "maintainers": [
        {
            "name": "csbun"
        }
    ],
    "name": "silly-datetime",
    "optionalDependencies": {},
    "repository": {
        "type": "git",
        "url": "git+https://github.com/csbun/silly-datetime.git"
    },
    "scripts": {
        "prepublish": "node rollup.js",
        "test": "istanbul cover ./node_modules/mocha/bin/_mocha --report lcovonly -- -R spec && cat ./coverage/lcov.info | ./node_modules/coveralls/bin/coveralls.js && rm -rf ./coverage"
    },
    "version": "0.1.2",
    "bin": {}
}
```



# misc
- this document was created with [utility2](https://github.com/kaizhu256/node-utility2)
