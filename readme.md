# umitt

![image](https://user-images.githubusercontent.com/9839768/54528808-98509380-49b0-11e9-9ae0-9a29ea265e2f.png)

# About

[![npm version][npm-version-image]][npm-url]
[![npm downloads][npm-downloads-image]][npm-url]
[![github issues][github-issues-image]][github-issues-url]
[![build status][travis-image]][travis-url]
[![size][size-image]][npm-url]

An upgraded version of Events in Node.js core API for the browser. We only get features that we think you really need, not the whole.

[npm-url]: https://npmjs.org/package/umitt
[npm-version-image]: https://badge.fury.io/js/umitt.svg
[npm-downloads-image]: https://img.shields.io/npm/dm/umitt.svg
[github-issues-image]: https://img.shields.io/github/issues/lamhieu-vk/umitt.svg
[github-issues-url]: https://github.com/lamhieu-vk/umitt/issues
[travis-image]: https://travis-ci.com/lamhieu-vk/umitt.svg?branch=master
[travis-url]: https://travis-ci.com/lamhieu-vk/umitt
[size-image]: http://img.badgesize.io/https://cdn.jsdelivr.net/npm/umitt/dist/umitt.js?compression=gzip

# Usage

## Installation

```bash
$ npm install umitt

// or yarn
$ yarn add umitt
```

### CDN

```html
// unpkg
<script src="https://unpkg.com/umitt/dist/umitt.js"></script>

// jsdelivr
<script src="https://cdn.jsdelivr.net/npm/umitt/dist/umitt.js"></script>
```

**Note** use CDN in browser, you can call `umitt` from Window API. it is available at `window.umitt`

## Example

```js
import Events from 'umitt'

const emitter = new Events()

// add event listener
emitter.on('connection', (name) => {
  console.log(name, 'connected!');
})

// emit event
emitter.emit('connection', 'Hieu Lam')
```

## Documents

### `Events: emitter`

The Events class is defined and exposed by the events module:
```js
import Events from 'umitt'

const emitter = new Events()
```

All EventEmitters emit the event `'newListener'` when new listeners are added and `'removeListener'` when existing listeners are removed.

### `addListener(eventName, listener)`

Alias for `on(eventName, listener)`.

```js
emitter.addListener('eventName', callback)
```

### `emit(eventName[, ...args])`

Synchronously calls each of the listeners registered for the event named `eventName`, in the order they were registered, passing the supplied arguments to each.

```js
// without argument
emitter.emit('eventName')

// with argument
emitter.emit('eventName', 'arg1', 'arg2', ...)
```

### `eventNames()`

Returns an array listing the events for which the emitter has registered listeners.

```js
emitter.eventsName()
```

#### Example
```js
const callback = () => {}

emitter.on('eventName', callback)

console.log(emitter.eventNames())

// prints: [ 'eventName' ]
```

### `listeners(eventName)`

Returns a copy of the array of listeners for the event named `eventName`.

```js
emitter.listeners('eventName')
```

#### Example
```js
const callback = () => {}

emitter.on('eventName', callback)

console.log(emitter.listeners('eventName'))

// prints: [ [Function] ]
```

### `off(eventName, listener)`

Alias for `removeListener(eventName, listener)`.

### `on(eventName, listener)`

Adds the listener function to the end of the listeners array for the event named `eventName`. No checks are made to see if the listener has already been added. Multiple calls passing the same combination of `eventName` and listener will result in the listener being added, and called, multiple times.

```js
// without argument
emitter.on('eventName', () => {
  console.log('called!');
});

// with argument
emitter.on('eventName', (arg1, arg2) => {
  console.log('called!', [arg1, arg2]);
});
```

#### Example
```js
emitter.on('sayName', (name) => {
  console.log('my name is', name)
})
emitter.emit('sayName', 'Hieu Lam')

// prints:
// my name is Hieu Lam
```

### `once(eventName, listener)`

Adds a **one-time** listener function for the event named `eventName`. The next time `eventName` is triggered, this listener is removed and then invoked.
```js
// without argument
emitter.once('eventName', () => {
  console.log('called!');
});

// with argument
emitter.once('eventName', (arg1, arg2) => {
  console.log('called!', [arg1, arg2]);
});
```

#### Example
```js
emitter.once('sayName', (name) => {
  console.log('my name is', name)
})
emitter.emit('sayName', 'Hieu Lam')
emitter.emit('sayName', 'John Smith')

// prints:
// my name is Hieu Lam
```

### `removeAllListeners([eventName])`

Removes all listeners, or those of the specified `eventName`.

```js
emitter.removeAllListeners(['eventName'])
```

### `removeListener(eventName, listener)`

Removes the specified listener from the listener array for the event named `eventName`.
`removeListener()` will remove, at most, one instance of a listener from the listener array. If any single listener has been added multiple times to the listener array for the specified `eventName`, then `removeListener()` must be called multiple times to remove each instance.

```js
emitter.removeListener('eventName', callback)
```

#### Example
```js
const callback = (name) => {
  console.log('my name is', name)
}
emitter.on('sayName', callback)
emitter.emit('sayName', 'Hieu Lam')
// prints: my name is Hieu Lam

emitter.removeListener('sayName', callback)
emitter.emit('sayName', 'Hieu Lam')
// nothing
```

### `disable(eventName)`

Disable the specified listeners for the event named `eventName`. When listeners was disabled, it's still existed but not run when `emit` called. To enbale listeners for the event, just use `enable(eventName)`.

```js
emitter.disable('eventName')
```

#### Example
```js
const callback = (name) => {
  console.log('my name is', name)
}
emitter.on('sayName', callback)
emitter.emit('sayName', 'Hieu Lam')
// prints: my name is Hieu Lam

emitter.disable('sayName')
emitter.emit('sayName', 'Hieu Lam')
// nothing

emitter.enable('sayName')
emitter.emit('sayName', 'Hieu Lam')
// prints: my name is Hieu Lam
```

### `enable(eventName)`

Enable the specified listeners for the event named `eventName`.

```js
emitter.enable('eventName')
```

#### Example
```js
const callback = (name) => {
  console.log('my name is', name)
}
emitter.on('sayName', callback)
emitter.emit('sayName', 'Hieu Lam')
// prints: my name is Hieu Lam

emitter.disable('sayName')
emitter.emit('sayName', 'Hieu Lam')
// nothing

emitter.enable('sayName')
emitter.emit('sayName', 'Hieu Lam')
// prints: my name is Hieu Lam
```
