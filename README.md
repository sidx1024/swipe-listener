# Swipe-Listener

Zero-dependency, minimal swipe-gesture listener for the web.

---

## [Demo](https://umanghome.github.io/swipe-listener) 

Open from a touch-device, or simulate a touch-device using DevTools.

# What

Swipe-listener is a very minimal library that allows listening for swipe gesture on literally any DOM element. Once invoked with a DOM element, simply listen for `swipe` event and determine the direction with the `directions` object.

# Example Code

```js
var container = document.querySelector('#container');
var listener = SwipeListener(container);
container.addEventListener('swipe', function (e) {
  var directions = e.detail.directions;
  var x = e.detail.x;
  var y = e.detail.y;

  if (directions.left) {
    console.log('Swiped left.');
  }

  if (directions.right) {
    console.log('Swiped right.');
  }

  if (directions.top) {
    console.log('Swiped top.');
  }

  if (directions.bottom) {
    console.log('Swiped bottom.');
  }

  if (directions.top && directions.right) {
    console.log('Swiped top-right.');
  }

  if (directions.top && directions.left) {
    console.log('Swiped top-left.');
  }

  if (directions.bottom && directions.right) {
    console.log('Swiped bottom-right.');
  }

  if (directions.bottom && directions.left) {
    console.log('Swiped bottom-left.');
  }

  console.log('Started horizontally at', x[0], 'and ended at', x[1]);
  console.log('Started vertically at', y[0], 'and ended at', y[1]);
});
```

# Installation

## Browser

```html
<script src="path/to/swipe-listener.min.js" type="text/javascript"></script>
<script>
  var container = document.querySelector('#container');
  var listener = SwipeListener(container);
  container.addEventListener('swipe', function (e) {
    console.log(e.detail);
  });
</script>
```

Swipe-listener is also available from unpkg: [`https://unpkg.com/swipe-listener@1.0.1/dist/swipe-listener.min.js`](https://unpkg.com/swipe-listener@1.0.1/dist/swipe-listener.min.js)

## Installing using NPM

Install from NPM using `npm i --save swipe-listener`, then

```js
import SwipeListener from 'swipe-listener';
```

OR

```js
const SwipeListener = require('swipe-listener');
```

# API

### `SwipeListener(element, options)`

- `element` DOM Element on which you want to enable swipe gesture tracking. This is the element on which you will be attacking the `swipe` event listener.
- `options` [Optional] Configuration options (see below)

Listen for `swipe` event on the `element` passed. Access details using `event.detail`. For example, `directions` can be accessed using `event.detail.directions`.

Data passed to `event.detail`:

- `directions` (Object)
  - `top` (Boolean) Signifies a top-swipe.
  - `right` (Boolean) Signifies a right-swipe.
  - `bottom` (Boolean) Signifies a bottom-swipe.
  - `left` (Boolean) Signifies a left-swipe.
- `x` (Array) Array containing two elements: starting and ending x-coords.
- `y` (Array) Array containing two elements: starting and ending y-coords.

**Note that multiple directions can be `true` at one. In case of a top-left swipe, `directions.top` and `directions.left` will both be `true`.**

### Options

| Key | Description | Default value |
| --- | --- | --- |
| `minHorizontal` | Minimum number of horizontal pixels travelled for the gesture to be considered as a left or right swipe. | `10` |
| `minVertical` | Minimum number of vertical pixels travelled for the gesture to be considered as a top or bottom swipe. | `10` |
| `deltaHorizontal` | Maximum difference between the rightmost pixel (right-swipe) or the leftmost pixel (left-swipe) travelled to and the pixel at which the gesture is released. | `3` |
| `deltaVertical` | Maximum difference between the bottommost pixel (bottom-swipe) or the topmost pixel (top-swipe) travelled to and the pixel at which the gesture is released. | `5` |

### `.off()`

Turns off the swipe-listener on a given element.

Usage:

```js
var listener = SwipeListener(myElem);
listener.off();
```

---

# License

[MIT License](https://opensource.org/licenses/MIT) © [Umang Galaiya](https://umanggalaiya.in/)
