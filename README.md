# Specifications

This document is used by [gulp-bem](https://github.com/floatdrop/gulp-bem).

 * [BEM identifiers](#bem-identifiers-)
 * [Directory structure](#directory-structure-)
 * [Dependencies file](#dependencies-file-)

## BEM identifiers ![stable](http://img.shields.io/badge/spec-stable-brightgreen.svg?style=flat)

We are using conventions, that are described in [bem-naming](https://github.com/bem/bem-naming#string-representation) repository.

BEM __identifier__ defines _Block_, _Element_, _Modificator_ and _Modificator value_ string representation.

To separate _Block_ name from _Element_ we are using __Element delimeter__, which by default equals `__`.

To separate _Block_ name from _Modificator_, _Element_ from _Modificator_ and _Modificator_ from _Modificator value_ we are using __Modificator delimeter__, which by default equals `_`.

Every _identifier_ should contain _Block_. _Element_, _Modificator_ and _Modificator value_ can be absent.

Rules defined above describes next string:

`Block{Element delimeter}Element{Modificator delimeter}Modificator{Modificator delimeter}Modificator value`

_Block_, _Element_, _Modificator_ and _Modificator value_ should be strings that fulfill regular expression `[a-z0-9]+(?:-[a-z0-9]+)*`

## Directory structure ![stable](http://img.shields.io/badge/spec-stable-brightgreen.svg?style=flat)

We are using conventions, that are described on [bem.info](http://bem.info/method/filesystem/) site.

BEM methodology does not implies certain directory structure, but for file separation and structuring your application it is advised to store files in predefined way. All files, that are belongs to BEM entity, that has _identifier_ should be placed in directory according to _Block_, _Element_ and _Modificator_ values.

Directories can be different types (based on nesting):

* __Level__ - top directory with _Blocks_.  
* __Block__ - child directory in _Level_.
* __Element__ - child directory in _Block_ that starts with _Element delimeter_.
* __Modificator__ - child directory in _Block_ or _Element_ that starts with _Modificator delimeter_.

All files for _Block_ should go to _Block_ directory, etc.

## Dependencies file ![unstable](http://img.shields.io/badge/spec-unstable-orange.svg?style=flat)

Each directory in _directory structure_ can have __dependency file__ that have next name: `{bem}.deps.js`.

> `{bem}` is placeholder for _BEM identifier_.

Those files should contain JavaScript code that returns _dependency object_ or place _dependency object properties_ in `module.exports` (if CommonJS notation is used).

_Dependency object_ can have next properties:

 * `require` - contains `Object` or `Array` of `Object`
 * `expect` - contains `Object` or `Array` of `Object`

This properties is used to determine order of included dependencies with current block.

`require` defines dependencies, that should be included __before__ current block.

`expect` defines dependencies, that should be included __after__ current block.

`Object` in `require` and `expect` is short notation of [BEM object](https://github.com/floatdrop/bem-object) that will be normalized with [deps-normalize](https://github.com/floatdrop/deps-normalize) and missing properties (`level`, `block`, `elem`, `mod`, `val`) will be taken from current block.
