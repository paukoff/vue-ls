<div align="center">
  <img width="130" alt="vue-ls logo" src="https://cdn.rawgit.com/RobinCK/0ef39abfff9a44061cee5b2c072e892e/raw/e2b95a57825ac9b8e845609ff9fc5fdaae37b55a/logo.svg">
  
  [![js-semistandard-style](https://img.shields.io/badge/code%20style-semistandard-brightgreen.svg?style=flat-square)](https://github.com/Flet/semistandard)[![VueJS 1.x](https://img.shields.io/badge/vuejs-1.x-brightgreen.svg?style=flat-square)](https://github.com/RobinCK/vue-ls)[![VueJS 2.x](https://img.shields.io/badge/vuejs-2.x-brightgreen.svg?style=flat-square)](https://github.com/RobinCK/vue-ls)[![Build Status](https://img.shields.io/travis/RobinCK/vue-ls.svg?style=flat-square)](https://travis-ci.org/RobinCK/vue-ls)[![Coverage Status](https://img.shields.io/coveralls/RobinCK/vue-ls.svg?style=flat-square)](https://coveralls.io/github/RobinCK/vue-ls?branch=master)[![Code Climate](https://img.shields.io/codeclimate/github/RobinCK/vue-ls.svg?style=flat-square)](https://codeclimate.com/github/RobinCK/vue-ls)[![Inline docs](http://inch-ci.org/github/RobinCK/vue-ls.svg?branch=master&style=flat-square)](http://inch-ci.org/github/RobinCK/vue-ls)

[![npm](https://img.shields.io/npm/dt/vue-ls.svg?style=flat-square)](https://github.com/RobinCK/vue-ls)[![Dependencies](https://david-dm.org/robinck/vue-ls.svg?style=flat-square)](https://david-dm.org/robinck/vue-ls)[![devDependencies](https://david-dm.org/robinck/vue-ls/dev-status.svg?style=flat-square)](https://david-dm.org/robinck/vue-ls#info=devDependencies&view=table)[![Bower version](https://img.shields.io/bower/v/vue-ls.svg?style=flat-square)](https://github.com/RobinCK/vue-ls)[![NPM version](https://img.shields.io/npm/v/vue-ls.svg?style=flat-square)](https://www.npmjs.com/package/vue-ls)[![npm](https://img.shields.io/npm/l/vue-ls.svg?style=flat-square)](https://github.com/RobinCK/vue-ls/blob/master/LICENSE)

[![Build Status](https://cdn.rawgit.com/RobinCK/65849005c282a0e59d93b7e8ce05b980/raw/72ec5d77d535103016832f4aa592e93e4b83f9ee/browsers_support.svg)](https://saucelabs.com/beta/builds/1defc2f5e76e4478817fc085438416d3)
</div>

# vue-ls

Vue plugin for work with LocalStorage from Vue context

[![NPM](https://nodei.co/npm/vue-ls.png?downloads=true&downloadRank=true&stars=true)](https://nodei.co/npm/vue-ls/)

## Example

[Vue 1.x](https://jsfiddle.net/Robin_ck/Lvb2ah5p/)

[Vue 2.x](https://jsfiddle.net/Robin_ck/6x1akv1L/) 

## Install
#### CDN

Recommended: https://unpkg.com/vue-ls, which will reflect the latest version as soon as it is published to npm. You can also browse the source of the npm package at https://unpkg.com/vue-ls/

#### NPM

``` bash
npm install vue-ls --save
```

#### Yarn

``` bash
yarn add vue-ls
```

#### Bower

``` bash
bower install vue-ls --save
```

## Development Setup

``` bash
# install dependencies
npm install

# build dist files
npm run build
```

## Usage

Vue localStorage API.

``` js
import VueLocalStorage from 'vue-ls';

options = {
  namespace: 'vuejs__'
};

Vue.use(VueLocalStorage, options);

//or
//Vue.use(VueLocalStorage);

new Vue({
    el: '#app',
    mounted: function() {
        Vue.ls.set('foo', 'boo');
        //Set expire for item
        Vue.ls.set('foo', 'boo', 60 * 60 * 1000); //expiry 1 hour
        Vue.ls.get('foo');
        Vue.ls.get('boo', 10); //if not set boo returned default 10
        
        let callback = (val, oldVal, uri) => {
          console.log('localStorage chnage', val);
        } 
        
        Vue.ls.on('foo', callback) //watch change foo key and triggered callback
        Vue.ls.off('foo', callback) //unwatch
        
        Vue.ls.remove('foo');
    }
});
```

#### Global

- `Vue.ls`
 
#### Context
- `this.$ls`

## API

#### `Vue.ls.get(name, def)`

Returns value under `name` in local storage. Internally parses the value from JSON before returning it.

- `def`: default null, returned if not set `name`.

#### `Vue.ls.set(name, value, expire)`

Persists `value` under `name` in local storage. Internally converts the `value` to JSON.

- `expire`: default null, life time in milliseconds `name`

#### `Vue.ls.remove(name)`

Removes `name` from local storage. Returns `true` if the property was successfully deleted, and `false` otherwise.

#### `Vue.ls.clear()`

Clears local storage.

#### `Vue.ls.on(name, callback)`

Listen for changes persisted against `name` on other tabs. Triggers `callback` when a change occurs, passing the following arguments.

- `newValue`: the current value for `name` in local storage, parsed from the persisted JSON
- `oldValue`: the old value for `name` in local storage, parsed from the persisted JSON
- `url`: the url for the tab where the modification came from

#### `Vue.ls.off(name, callback)`

Removes a listener previously attached with `Vue.ls.on(name, callback)`.

## Testing

- `npm run test` - run unit test
- `npm run test:browserstack` - run browser test
  - `npm run test:browserstack:chrome`
  - `npm run test:browserstack:ie`
  - `npm run test:browserstack:edge`
  - `npm run test:browserstack:firefox`
  - `npm run test:browserstack:safari`
- `npm run test:chrome` - run browser test in chrome
- `npm run test:phantomjs` - run browser test in phantomjs

Testing Supported By<br>
<img width="200" src="https://cdn.rawgit.com/RobinCK/b1435c9cae05437ad9e4c2023aec08e4/raw/4b89e95cd89827935e6e3949d28a4f6ea3e48ee4/browser-stack.svg">

## Note
Some browsers don't support the storage event, and most of the browsers that do support it will only call it when the storage is changed by a different window. So, open your page up in two windows. Click the links in one window and you will probably see the event in the other.

The assumption is that your page will already know all interactions with localStorage in its own window and only needs notification when a different window changes things. This, of course, is a foolish assumption. But.


## License
MIT © [Igor Ognichenko](https://github.com/RobinCK)
