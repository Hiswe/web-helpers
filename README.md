# web-helpers

some common web patterns

<!-- START doctoc generated TOC please keep comment here to allow auto update -->
<!-- DON'T EDIT THIS SECTION, INSTEAD RE-RUN doctoc TO UPDATE -->


- [general](#general)
- [mobile](#mobile)

<!-- END doctoc generated TOC please keep comment here to allow auto update -->

## general

- box-sizing
  ```css
  *,
  *::before,
  *::after {
    box-sizing: border-box;
  }
  ```
- accord native elements to website style
  ```css
  button,
  input,
  textarea,
  select {
    font: inherit;
  }
  ```
- [accessible focus ring](https://hackernoon.com/removing-that-ugly-focus-ring-and-keeping-it-too-6c8727fefcd2) (enabled by tabbing with a keyboard)
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

## mobile

- prevent font scaling while rotating iOS device while allowing user to zoom
  ```css
  html {
    -webkit-text-size-adjust: 100%;
  }
  ```
- [prevent zooming on double-tap](https://stackoverflow.com/questions/46167604/iphone-html-disable-double-tap-to-zoom)

  ```css
  button {
    touch-action: manipulation;
  }
  ```
