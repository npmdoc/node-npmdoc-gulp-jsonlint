# api documentation for  [gulp-jsonlint (v1.2.0)](https://github.com/rogeriopvl/gulp-jsonlint)  [![npm package](https://img.shields.io/npm/v/npmdoc-gulp-jsonlint.svg?style=flat-square)](https://www.npmjs.org/package/npmdoc-gulp-jsonlint) [![travis-ci.org build-status](https://api.travis-ci.org/npmdoc/node-npmdoc-gulp-jsonlint.svg)](https://travis-ci.org/npmdoc/node-npmdoc-gulp-jsonlint)
#### A jsonlint plugin for Gulp

[![NPM](https://nodei.co/npm/gulp-jsonlint.png?downloads=true)](https://www.npmjs.com/package/gulp-jsonlint)

[![apidoc](https://npmdoc.github.io/node-npmdoc-gulp-jsonlint/build/screenCapture.buildNpmdoc.browser._2Fhome_2Ftravis_2Fbuild_2Fnpmdoc_2Fnode-npmdoc-gulp-jsonlint_2Ftmp_2Fbuild_2Fapidoc.html.png)](https://npmdoc.github.io/node-npmdoc-gulp-jsonlint/build/apidoc.html)

![npmPackageListing](https://npmdoc.github.io/node-npmdoc-gulp-jsonlint/build/screenCapture.npmPackageListing.svg)

![npmPackageDependencyTree](https://npmdoc.github.io/node-npmdoc-gulp-jsonlint/build/screenCapture.npmPackageDependencyTree.svg)



# package.json

```json

{
    "author": {
        "name": "Rogério Vicente",
        "url": "https://github.com/rogeriopvl"
    },
    "bugs": {
        "url": "https://github.com/rogeriopvl/gulp-jsonlint/issues"
    },
    "dependencies": {
        "gulp-util": "3.0.7",
        "jsonlint": "1.6.2",
        "map-stream": "^0.1.0",
        "through2": "2.0.3"
    },
    "description": "A jsonlint plugin for Gulp",
    "devDependencies": {
        "mocha": "3.2.0",
        "should": "11.1.2"
    },
    "directories": {},
    "dist": {
        "shasum": "b9dd52daffd0f5426d16f657dedcfe9d86851ad9",
        "tarball": "https://registry.npmjs.org/gulp-jsonlint/-/gulp-jsonlint-1.2.0.tgz"
    },
    "engines": {
        "node": ">= 4",
        "npm": ">=1.2.10"
    },
    "files": [
        "index.js",
        "LICENSE"
    ],
    "gitHead": "b87dd1388fdf48b4f1294fbaae030030144714c9",
    "homepage": "https://github.com/rogeriopvl/gulp-jsonlint",
    "keywords": [
        "gulpplugin",
        "jsonlint",
        "json",
        "lint"
    ],
    "licenses": [
        {
            "type": "MIT"
        }
    ],
    "main": "./index.js",
    "maintainers": [
        {
            "name": "rogeriopvl",
            "email": "rogeriopvl@gmail.com"
        }
    ],
    "name": "gulp-jsonlint",
    "optionalDependencies": {},
    "readme": "ERROR: No README data found!",
    "repository": {
        "type": "git",
        "url": "git://github.com/rogeriopvl/gulp-jsonlint.git"
    },
    "scripts": {
        "test": "mocha"
    },
    "version": "1.2.0"
}
```



# <a name="apidoc.tableOfContents"></a>[table of contents](#apidoc.tableOfContents)

#### [module gulp-jsonlint](#apidoc.module.gulp-jsonlint)
1.  [function <span class="apidocSignatureSpan">gulp-jsonlint.</span>failAfterError ()](#apidoc.element.gulp-jsonlint.failAfterError)
1.  [function <span class="apidocSignatureSpan">gulp-jsonlint.</span>failOnError ()](#apidoc.element.gulp-jsonlint.failOnError)
1.  [function <span class="apidocSignatureSpan">gulp-jsonlint.</span>reporter (customReporter)](#apidoc.element.gulp-jsonlint.reporter)



# <a name="apidoc.module.gulp-jsonlint"></a>[module gulp-jsonlint](#apidoc.module.gulp-jsonlint)

#### <a name="apidoc.element.gulp-jsonlint.failAfterError"></a>[function <span class="apidocSignatureSpan">gulp-jsonlint.</span>failAfterError ()](#apidoc.element.gulp-jsonlint.failAfterError)
- description and source-code
```javascript
failAfterError = function () {
    var errorCount = 0;

    return through.obj(function (file, enc, cb) {
        errorCount += file.jsonlint.success === false

        cb(null, file);

    }, function (cb) {
        if (errorCount > 0) {
            this.emit('error', new PluginError(
                'gulp-jsonlint',
                {
                    name: 'JSONLintError',
                    message: 'Failed with ' + errorCount +
                        (errorCount === 1 ? ' error' : ' errors')
                }
            ));
        }

        cb();
    });
}
```
- example usage
```shell
...
// Cause the stream to stop(/fail) before copying an invalid JS file to the output directory
gulp.src('**/*.js')
	.pipe(jsonlint())
	.pipe(jsonlint.failOnError())
	.pipe(gulp.dest('../output'));
'''

### jsonlint.failAfterError()

Stop a task/stream if an jsonlint error has been reported for any file, but wait for all of them to be processed first.

## License

[MIT License](http://en.wikipedia.org/wiki/MIT_License)
...
```

#### <a name="apidoc.element.gulp-jsonlint.failOnError"></a>[function <span class="apidocSignatureSpan">gulp-jsonlint.</span>failOnError ()](#apidoc.element.gulp-jsonlint.failOnError)
- description and source-code
```javascript
failOnError = function () {

    return through.obj(function (file, enc, cb) {
        if (file.jsonlint.success === false) {
            var error = new PluginError(
                    'gulp-jsonlint',
                    {
                        name: 'JSONLintError',
                        filename: file.path,
                        message: file.jsonlint.message,
                    }
                );
        }

        return cb(error, file);
    });
}
```
- example usage
```shell
...

##### file

Type: 'object'

This argument has the attribute 'jsonlint' wich is an object that contains a 'success' boolean attribute. If it's false you also
 have a 'message' attribute containing the jsonlint error message.

### jsonlint.failOnError()

Stop a task/stream if an jsonlint error has been reported for any file.

'''javascript
// Cause the stream to stop(/fail) before copying an invalid JS file to the output directory
gulp.src('**/*.js')
	.pipe(jsonlint())
...
```

#### <a name="apidoc.element.gulp-jsonlint.reporter"></a>[function <span class="apidocSignatureSpan">gulp-jsonlint.</span>reporter (customReporter)](#apidoc.element.gulp-jsonlint.reporter)
- description and source-code
```javascript
reporter = function (customReporter) {
    var reporter = defaultReporter;

    if (typeof customReporter === 'function') {
        reporter = customReporter;
    }

    return mapStream(function (file, cb) {
        if (file.jsonlint && !file.jsonlint.success) {
            reporter(file);
        }
        return cb(null, file);
    });
}
```
- example usage
```shell
...
Then, add it to your 'gulpfile.js':

'''javascript
var jsonlint = require("gulp-jsonlint");

gulp.src("./src/*.json")
    .pipe(jsonlint())
    .pipe(jsonlint.reporter());
'''

Using a custom reporter:

'''javascript
var jsonlint = require('gulp-jsonlint');
var gutil = require('gulp-util');
...
```



# misc
- this document was created with [utility2](https://github.com/kaizhu256/node-utility2)
