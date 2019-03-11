Session Storage Fallback
--------------

[![semantic-release](https://badge.fury.io/js/%40comicrelief%session-storage-fallback.svg)](https://www.npmjs.com/package/@comicrelief/session-storage-fallback)

Check and use appropriate storage adapter for browser (sessionStorage, cookies, memory)

This repository was cloned from [github.com/ripeworks/local-storage-fallback](https://github.com/ripeworks/local-storage-fallback) due to a need to fallback from session storage rather than local storage.

## Installation

```
$ npm install session-storage-fallback
```

## Usage

```js
import storage from 'session-storage-fallback' // if you use es6 or typescript
// use object destructuring when using require()
// const {storage} = require('session-storage-fallback')

// Use storage directly
storage.setItem('foo', 'bar');
storage.getItem('foo'); // bar

// Or shim window.sessionStorage
if (!('sessionStorage' in window)) {
  window.sessionStorage = storage;
}
```

## Purpose

With browser settings like "Private Browsing" it has become a problem to rely on a working `window.sessionStorage`, even in newer browsers. Even though it may exist, it will throw exceptions when trying to use `setItem` or `getItem`. This module will run appropriate checks to see what browser storage mechanism might be available, and then expose it. It uses the same API as `sessionStorage` so it should work as a drop-in replacement in most cases.

## Gotchas

* `CookieStorage` __has__ storage limits. Be careful here.
* `MemoryStorage` will __not__ persist between page loads. This is more or less a stop-gap to prevent page crashes, but may be sufficient for websites that don't do full page loads.
