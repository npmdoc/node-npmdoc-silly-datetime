# api documentation for  [silly-datetime (v0.1.2)](https://github.com/csbun/silly-datetime)  [![npm package](https://img.shields.io/npm/v/npmdoc-silly-datetime.svg?style=flat-square)](https://www.npmjs.org/package/npmdoc-silly-datetime) [![travis-ci.org build-status](https://api.travis-ci.org/npmdoc/node-npmdoc-silly-datetime.svg)](https://travis-ci.org/npmdoc/node-npmdoc-silly-datetime)
#### simple datetime formater

[![NPM](https://nodei.co/npm/silly-datetime.png?downloads=true)](https://www.npmjs.com/package/silly-datetime)

[![apidoc](https://npmdoc.github.io/node-npmdoc-silly-datetime/build/screenCapture.buildNpmdoc.browser._2Fhome_2Ftravis_2Fbuild_2Fnpmdoc_2Fnode-npmdoc-silly-datetime_2Ftmp_2Fbuild_2Fapidoc.html.png)](https://npmdoc.github.io/node-npmdoc-silly-datetime/build/apidoc.html)

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
            "name": "csbun",
            "email": "icsbun@gmail.com"
        }
    ],
    "name": "silly-datetime",
    "optionalDependencies": {},
    "readme": "ERROR: No README data found!",
    "repository": {
        "type": "git",
        "url": "git+https://github.com/csbun/silly-datetime.git"
    },
    "scripts": {
        "prepublish": "node rollup.js",
        "test": "istanbul cover ./node_modules/mocha/bin/_mocha --report lcovonly -- -R spec && cat ./coverage/lcov.info | ./node_modules/coveralls/bin/coveralls.js && rm -rf ./coverage"
    },
    "version": "0.1.2"
}
```



# <a name="apidoc.tableOfContents"></a>[table of contents](#apidoc.tableOfContents)

#### [module silly-datetime](#apidoc.module.silly-datetime)
1.  [function <span class="apidocSignatureSpan">silly-datetime.</span>format (datetime, formatStr)](#apidoc.element.silly-datetime.format)
1.  [function <span class="apidocSignatureSpan">silly-datetime.</span>fromNow (datetime)](#apidoc.element.silly-datetime.fromNow)
1.  [function <span class="apidocSignatureSpan">silly-datetime.</span>locate (arg)](#apidoc.element.silly-datetime.locate)



# <a name="apidoc.module.silly-datetime"></a>[module silly-datetime](#apidoc.module.silly-datetime)

#### <a name="apidoc.element.silly-datetime.format"></a>[function <span class="apidocSignatureSpan">silly-datetime.</span>format (datetime, formatStr)](#apidoc.element.silly-datetime.format)
- description and source-code
```javascript
function format(datetime, formatStr) {
  var t = getDateObject(datetime);
  var hours = undefined,
      o = undefined,
      i = 0;
  formatStr = formatStr || 'YYYY-MM-DD HH:mm:ss';
  hours = t.getHours();
  o = [['M+', t.getMonth() + 1], ['D+', t.getDate()],
  // H 24小时制
  ['H+', hours],
  // h 12小时制
  ['h+', hours > 12 ? hours - 12 : hours], ['m+', t.getMinutes()], ['s+', t.getSeconds()]];
  // 替换 Y
  if (/(Y+)/.test(formatStr)) {
    formatStr = formatStr.replace(RegExp.$1, (t.getFullYear() + '').substr(4 - RegExp.$1.length));
  }
  // 替换 M, D, H, h, m, s
  for (; i < o.length; i++) {
    if (new RegExp('(' + o[i][0] + ')').test(formatStr)) {
      formatStr = formatStr.replace(RegExp.$1, RegExp.$1.length === 1 ? o[i][1] : ('00' + o[i][1]).substr(('' + o[i][1]).length));
    }
  }
  // 替换 a/A 为 am, pm
  return formatStr.replace(/a/ig, hours > 11 ? 'pm' : 'am');
}
```
- example usage
```shell
...
bower install silly-datetime --save
'''

## Example

'''javascript
var sd = require('silly-datetime');
sd.format(new Date(), 'YYYY-MM-DD HH:mm');
// 2015-07-06 15:10

sd.fromNow(+new Date() - 2000);
// a few seconds ago
'''

ES2015:
...
```

#### <a name="apidoc.element.silly-datetime.fromNow"></a>[function <span class="apidocSignatureSpan">silly-datetime.</span>fromNow (datetime)](#apidoc.element.silly-datetime.fromNow)
- description and source-code
```javascript
function fromNow(datetime) {
  if (!_curentLocale) {
    // 初始化本地化语言为 en
    locate('');
  }
  var det = +new Date() - +getDateObject(datetime);
  var format = undefined,
      str = undefined,
      i = 0,
      detDef = undefined,
      detDefVal = undefined;
  if (det < 0) {
    format = _curentLocale.future;
    det = -det;
  } else {
    format = _curentLocale.past;
  }
  for (; i < DET_STD.length; i++) {
    detDef = DET_STD[i];
    detDefVal = detDef[1];
    if (det >= detDefVal) {
      str = _curentLocale[detDef[0]].replace('%s', parseInt(det / detDefVal, 0) || 1);
      break;
    }
  }
  return format.replace('%s', str);
}
```
- example usage
```shell
...
## Example

'''javascript
var sd = require('silly-datetime');
sd.format(new Date(), 'YYYY-MM-DD HH:mm');
// 2015-07-06 15:10

sd.fromNow(+new Date() - 2000);
// a few seconds ago
'''

ES2015:

'''javascript
import {
...
```

#### <a name="apidoc.element.silly-datetime.locate"></a>[function <span class="apidocSignatureSpan">silly-datetime.</span>locate (arg)](#apidoc.element.silly-datetime.locate)
- description and source-code
```javascript
function locate(arg) {
  var newLocale = undefined,
      prop = undefined;
  if (typeof arg === 'string') {
    newLocale = arg === 'zh-cn' ? LOCALE_ZH_CN : LOCALE_EN;
  } else {
    newLocale = arg;
  }
  if (!_curentLocale) {
    _curentLocale = {};
  }
  for (prop in newLocale) {
    if (newLocale.hasOwnProperty(prop) && typeof newLocale[prop] === 'string') {
      _curentLocale[prop] = newLocale[prop];
    }
  }
}
```
- example usage
```shell
...
- datetime: Date Object

'''javascript
sd.fromNow(+new Date() - 2000);
// a few seconds ago
'''

### .locate(newLocale)

Changing locale globally. By default, silly-datetime comes with English locale strings.

- newLocale: locate string or locate Object

Locate string can be 'en' (default) or 'zh-cn';
...
```



# misc
- this document was created with [utility2](https://github.com/kaizhu256/node-utility2)
