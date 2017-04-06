# api documentation for  [bottlejs (v1.6.0)](https://github.com/young-steveo/bottlejs)  [![npm package](https://img.shields.io/npm/v/npmdoc-bottlejs.svg?style=flat-square)](https://www.npmjs.org/package/npmdoc-bottlejs) [![travis-ci.org build-status](https://api.travis-ci.org/npmdoc/node-npmdoc-bottlejs.svg)](https://travis-ci.org/npmdoc/node-npmdoc-bottlejs)
#### A powerful dependency injection micro container

[![NPM](https://nodei.co/npm/bottlejs.png?downloads=true)](https://www.npmjs.com/package/bottlejs)

[![apidoc](https://npmdoc.github.io/node-npmdoc-bottlejs/build/screenCapture.buildNpmdoc.browser._2Fhome_2Ftravis_2Fbuild_2Fnpmdoc_2Fnode-npmdoc-bottlejs_2Ftmp_2Fbuild_2Fapidoc.html.png)](https://npmdoc.github.io/node-npmdoc-bottlejs/build/apidoc.html)

![npmPackageListing](https://npmdoc.github.io/node-npmdoc-bottlejs/build/screenCapture.npmPackageListing.svg)

![npmPackageDependencyTree](https://npmdoc.github.io/node-npmdoc-bottlejs/build/screenCapture.npmPackageDependencyTree.svg)



# package.json

```json

{
    "author": {
        "name": "Stephen Young",
        "email": "young.steveo@gmail.com"
    },
    "bugs": {
        "url": "https://github.com/young-steveo/bottlejs/issues"
    },
    "dependencies": {},
    "description": "A powerful dependency injection micro container",
    "devDependencies": {
        "grunt": "^0.4.5",
        "grunt-contrib-clean": "^0.6.0",
        "grunt-contrib-concat": "^0.5.0",
        "grunt-contrib-jasmine": "^1.0.3",
        "grunt-contrib-jshint": "^0.10.0",
        "grunt-contrib-uglify": "^0.5.1",
        "grunt-wrap": "^0.3.0",
        "lodash": "^2.4.1"
    },
    "directories": {},
    "dist": {
        "shasum": "95854f7b4163b2eadb85eee5398444ca2d95cf1c",
        "tarball": "https://registry.npmjs.org/bottlejs/-/bottlejs-1.6.0.tgz"
    },
    "gitHead": "6da756eb12b70318ef88a1496d214ca8d145bf66",
    "homepage": "https://github.com/young-steveo/bottlejs",
    "keywords": [
        "di",
        "dependency",
        "injection",
        "micro",
        "angular",
        "pimple"
    ],
    "license": "MIT",
    "main": "dist/bottle.js",
    "maintainers": [
        {
            "name": "young-steveo",
            "email": "young.steveo@gmail.com"
        }
    ],
    "name": "bottlejs",
    "optionalDependencies": {},
    "readme": "ERROR: No README data found!",
    "repository": {
        "type": "git",
        "url": "git://github.com/young-steveo/bottlejs.git"
    },
    "scripts": {
        "test": "grunt test"
    },
    "typings": "dist/bottle.d.ts",
    "version": "1.6.0"
}
```



# <a name="apidoc.tableOfContents"></a>[table of contents](#apidoc.tableOfContents)

#### [module bottlejs](#apidoc.module.bottlejs)
1.  [function <span class="apidocSignatureSpan">bottlejs.</span>Bottle (name)](#apidoc.element.bottlejs.Bottle)
1.  [function <span class="apidocSignatureSpan">bottlejs.</span>clear (name)](#apidoc.element.bottlejs.clear)
1.  [function <span class="apidocSignatureSpan">bottlejs.</span>list (container)](#apidoc.element.bottlejs.list)
1.  [function <span class="apidocSignatureSpan">bottlejs.</span>pop (name)](#apidoc.element.bottlejs.pop)
1.  object <span class="apidocSignatureSpan">bottlejs.</span>config



# <a name="apidoc.module.bottlejs"></a>[module bottlejs](#apidoc.module.bottlejs)

#### <a name="apidoc.element.bottlejs.Bottle"></a>[function <span class="apidocSignatureSpan">bottlejs.</span>Bottle (name)](#apidoc.element.bottlejs.Bottle)
- description and source-code
```javascript
function Bottle(name) {
    if (!(this instanceof Bottle)) {
        return Bottle.pop(name);
    }

    this.id = id++;

    this.decorators = {};
    this.middlewares = {};
    this.nested = {};
    this.providerMap = {};
    this.originalProviders = {};
    this.deferred = [];
    this.container = {
        $decorator : decorator.bind(this),
        $register : register.bind(this),
        $list : list.bind(this)
    };
}
```
- example usage
```shell
n/a
```

#### <a name="apidoc.element.bottlejs.clear"></a>[function <span class="apidocSignatureSpan">bottlejs.</span>clear (name)](#apidoc.element.bottlejs.clear)
- description and source-code
```javascript
function clear(name) {
    if (typeof name === 'string') {
        delete bottles[name];
    } else {
        bottles = {};
    }
}
```
- example usage
```shell
n/a
```

#### <a name="apidoc.element.bottlejs.list"></a>[function <span class="apidocSignatureSpan">bottlejs.</span>list (container)](#apidoc.element.bottlejs.list)
- description and source-code
```javascript
function list(container) {
    return Object.keys(container || this.container || {}).filter(byMethod);
}
```
- example usage
```shell
...
In general, this function should only be called in situations where you intend to reset the bottle instance with new providers,
decorators, etc. such as test setup.

Param                      | Type       | Details
:--------------------------|:-----------|:--------
**name**<br />*(optional)* | *String*   | The name of the bottle. If passed, bottle will remove the internal instance, if such a
 bottle was created using 'Bottle.pop'. If not passed, all named internal instances will be cleared.

#### list(container)
#### prototype.list()
#### prototype.container.$list()

Used to list the names of all registered constants, values, and services on the container.  Must pass a container to the global
static version 'Bottle.list(bottle.container)'.  The instance and container versions return the services that are registered within
.

Returns an array of strings.

Param                           | Type       | Details
...
```

#### <a name="apidoc.element.bottlejs.pop"></a>[function <span class="apidocSignatureSpan">bottlejs.</span>pop (name)](#apidoc.element.bottlejs.pop)
- description and source-code
```javascript
function pop(name) {
    var instance;
    if (typeof name === 'string') {
        instance = bottles[name];
        if (!instance) {
            bottles[name] = instance = new Bottle();
            instance.constant('BOTTLE_NAME', name);
        }
        return instance;
    }
    return new Bottle();
}
```
- example usage
```shell
...

## API

### Bottle

#### pop(name)

Used to get an instance of bottle.  If a name is passed, bottle will return the same instance.  Calling the Bottle constructor as
 a function will call and return return 'Bottle.pop', so 'Bottle.pop('Soda') === Bottle('Soda')'

Param                      | Type       | Details
:--------------------------|:-----------|:--------
**name**<br />*(optional)* | *String*   | The name of the bottle. If passed, bottle will store the instance internally and return
 the same instance if 'Bottle.pop' is subsequently called with the same name.

#### clear(name)
...
```



# misc
- this document was created with [utility2](https://github.com/kaizhu256/node-utility2)
