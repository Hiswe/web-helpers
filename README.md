# web-helpers

some common web patterns

<!-- START doctoc generated TOC please keep comment here to allow auto update -->
<!-- DON'T EDIT THIS SECTION, INSTEAD RE-RUN doctoc TO UPDATE -->


- [CSS – general](#css-%C2%A0general)
  - [native font-stack](#native-font-stack)
  - [mono font-stack](#mono-font-stack)
  - [box-sizing](#box-sizing)
  - [mobile – prevent font scaling while rotating iOS device while allowing user to zoom](#mobile--prevent-font-scaling-while-rotating-ios-device-while-allowing-user-to-zoom)
  - [mobile – prevent zooming on double-tap](#mobile--prevent-zooming-on-double-tap)
  - [accord native elements to website style](#accord-native-elements-to-website-style)
  - [font aliasing](#font-aliasing)
  - [momentum scrolling](#momentum-scrolling)
  - [hidden and accessible](#hidden-and-accessible)
- [CSS – with JS](#css--with-js)
  - [accessible focus ring (enabled by tabbing with a keyboard)](#accessible-focus-ring-enabled-by-tabbing-with-a-keyboard)
- [javascript](#javascript)
  - [native array unique](#native-array-unique)
  - [external promise creation](#external-promise-creation)

<!-- END doctoc generated TOC please keep comment here to allow auto update -->

## CSS – general

### native font-stack

see:

- [github system fonts](http://markdotto.com/2018/02/07/github-system-fonts/)
- [CSS trick](https://css-tricks.com/snippets/css/system-font-stack/#article-header-id-1)

```css
html {
  font-family: -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto,
    Oxygen-Sans, Ubuntu, Cantarell, "Helvetica Neue", sans-serif;
}
```

### mono font-stack

```css
html {
  font-family: Consolas, "Andale Mono WT", "Andale Mono", "Lucida Console",
    "Lucida Sans Typewriter", "DejaVu Sans Mono", "Bitstream Vera Sans Mono",
    "Liberation Mono", "Nimbus Mono L", Monaco, "Courier New", Courier,
    monospace;
}
```

### box-sizing

```css
*,
*::before,
*::after {
  box-sizing: border-box;
}
```

### mobile – prevent font scaling while rotating iOS device while allowing user to zoom

```css
html {
  -webkit-text-size-adjust: 100%;
}
```

### mobile – [prevent zooming on double-tap](https://stackoverflow.com/questions/46167604/iphone-html-disable-double-tap-to-zoom)

```css
button {
  touch-action: manipulation;
}
```

### accord native elements to website style

```css
button,
input,
textarea,
select {
  font: inherit;
  color: currentColor;
  text-align: inherit;
}
```

### [font aliasing](https://stackoverflow.com/questions/11459746/webfont-smoothing-and-antialiasing-in-firefox-and-opera#17927764)

```css
.font-smoothing {
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
}
```

### [momentum scrolling](https://css-tricks.com/snippets/css/momentum-scrolling-on-ios-overflow-elements/)

```css
.module {
  overflow-y: scroll; /* has to be scroll, not auto */
  -webkit-overflow-scrolling: touch;
}
```

### hidden and accessible

```css
.hidden-accessible {
  border: 0 !important;
  clip: rect(0 0 0 0) !important;
  height: 1px !important;
  margin: -1px !important;
  overflow: hidden !important;
  padding: 0 !important;
  position: absolute !important;
  width: 1px !important;
}
```

## CSS – with JS

<!-- ### [fluid font-size](https://css-tricks.com/snippets/css/fluid-typography/)

```scss
@function strip-unit($value) {
  @return $value / ($value * 0 + 1);
}

@mixin fluid-type($min-vw, $max-vw, $min-font-size, $max-font-size) {
  $u1: unit($min-vw);
  $u2: unit($max-vw);
  $u3: unit($min-font-size);
  $u4: unit($max-font-size);

  @if $u1 == $u2 and $u1 == $u3 and $u1 == $u4 {
    & {
      font-size: $min-font-size;
      @media screen and (min-width: $min-vw) {
        font-size: calc(
          #{$min-font-size} + #{strip-unit($max-font-size - $min-font-size)} *
            ((100vw - #{$min-vw}) / #{strip-unit($max-vw - $min-vw)})
        );
      }
      @media screen and (min-width: $max-vw) {
        font-size: $max-font-size;
      }
    }
  }
}
``` -->

### [accessible focus ring](https://hackernoon.com/removing-that-ugly-focus-ring-and-keeping-it-too-6c8727fefcd2) (enabled by tabbing with a keyboard)

```scss
body:not(.user-is-tabbing) {
  a:focus,
  button:focus,
  input:focus,
  select:focus,
  textarea:focus {
    outline: none;
  }
}
```

```js
function handleFirstTab(e) {
  if (e.keyCode === 9) {
    // the "I am a keyboard user" key
    document.body.classList.add(`user-is-tabbing`);
    window.removeEventListener(`keydown`, handleFirstTab, { passive: true });
  }
}
window.addEventListener(`keydown`, handleFirstTab);
```

## javascript

### [native array unique](https://stackoverflow.com/questions/1960473/get-all-unique-values-in-a-javascript-array-remove-duplicates#14438954)

```js
[...new Set(myArray)];
```

### [external promise creation](http://lea.verou.me/2016/12/resolve-promises-externally-with-this-one-weird-trick/)

```js
function defer() {
  var res, rej;
  var promise = new Promise((resolve, reject) => {
    res = resolve;
    rej = reject;
  });
  promise.resolve = res;
  promise.reject = rej;
  return promise;
}
```
