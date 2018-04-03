[![CircleCI](https://circleci.com/gh/angular/closure-demo.svg?style=svg)](https://circleci.com/gh/angular/closure-demo)

This repo is the demo/seed for bunding an Angular application with Google Closure Compiler.
It contains a minimal Hello World application with a single component.

**The compressed JS size for an Angular 5.0.1 Hello World app is 39.99kb.**

```
-rw-r--r--  1 29055 Nov  9 18:42 dist/bundle.js.brotli
-rw-r--r--  1 32554 Nov  9 18:42 dist/bundle.js.gz
-rw-r--r--  1 11896 Nov  9 18:42 node_modules/zone.js/dist/zone.min.js.brotli
-rw-r--r--  1 12988 Nov  9 18:32 node_modules/zone.js/dist/zone.min.js.gz
```

See https://github.com/angular/angular/issues/8550 for more context.

# Try it

First, install [brotli], which is a more modern compression algorithm than gzip.
It gives a 13% smaller JS file, no work required!
The commands below use it, but you don't have to.

On Mac, `brew install brotli`.



``` shell
$ yarn install
$ yarn run build
$ yarn run serve
```

[brotli]: https://github.com/google/brotli

## Where does the size come from?

``` shell
$ yarn run explore
```

# Notes

Requires Node >= 6.x since the `ngc` tool (and its deps) are now shipped as ES6 as well.

Requires Java installed to run the Closure Compiler. We recommend installing http://zulu.org/download-dev/.



!!!

Rollup rxjs and rxjs/operators as FESM

``` shell 
$ npm run rollup:rxjs

```

Edit `node_modules/rxjs/package.json` and change the line that points to the es2015 bundle to now point to the FESM:

`"es2015": "./_fesm2015/index.js"`

Repeat for all rxjs modules. By default, only operators is needed by the typical @angular packages.

Edit node_modules/rxjs/operators/package.json.

`"es2015": "../_fesm2015/operators/index.js"`


Change paths in closure.conf to the new fesm

```
--js node_modules/rxjs/package.json
--js node_modules/rxjs/_fesm2015/index.js

--js node_modules/rxjs/operators/package.json
--js node_modules/rxjs/_fesm2015/operators/index.js
```

