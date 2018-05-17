# LessBuildRepro

A repro solution of the issue in angular/angular-cli#10899 .

This project was generated with [Angular CLI](https://github.com/angular/angular-cli) version 6.0.3.

Command line run: `npx @angular/cli new less-build-repro --skip-tests=true --style=less`

## Reproducing the error

* Clone this repo
* Install deps: `npm install`
* Start the build: `npm start`
* Open a browser and note that the body background color is yellow.
* Open `src/app/anotherfile.less` (which is `@import`'ed from the root `style.less`) and change the background-color from `yellow` to `pink`
* Note that the background color in your browser **still is yellow**, not pink. Also notice that the build says `5 unchanged chunks`, and that the hash is the same as on initial compile:

```
$ npm start

> less-build-repro@0.0.0 start C:\src\tmp\less-build-repro
> ng serve

** Angular Live Development Server is listening on localhost:4200, open your browser on http://localhost:4200/ **

Date: 2018-05-17T08:15:30.913Z
Hash: 5d82d59500884f1bc5ad
Time: 13164ms
chunk {main} main.js, main.js.map (main) 10.7 kB [initial] [rendered]
chunk {polyfills} polyfills.js, polyfills.js.map (polyfills) 227 kB [initial] [rendered]
chunk {runtime} runtime.js, runtime.js.map (runtime) 5.22 kB [entry] [rendered]
chunk {styles} styles.js, styles.js.map (styles) 16 kB [initial] [rendered]
chunk {vendor} vendor.js, vendor.js.map (vendor) 3.37 MB [initial] [rendered]
i ｢wdm｣: Compiled successfully.
i ｢wdm｣: Compiling...

Date: 2018-05-17T08:16:11.686Z - Hash: 5d82d59500884f1bc5ad - Time: 313ms
5 unchanged chunks
i ｢wdm｣: Compiled successfully.
```

## Expected behaviour

The background color should be pink, and the hash after recompile should be changed.
