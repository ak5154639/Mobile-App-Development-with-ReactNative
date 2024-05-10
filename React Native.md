# React Native
  - A framework that relies on React core
  - Allows us to build mobile apps using only JavaScript
    - "Learn once, write anywhere"
  - Supports iOS and Android

## How does React Native work?
  - JavaScript is bundled
    - Transpiled and minified
  - Separate threads for UI, layout and JavaScript
  - Communicate asynchronously through a "bridge"
    - JS thred will request UI elements to be shown
    - JS thread can be blocked and UI will still work

## Differences between React Native and Web
  - Base components
  - Style
  - No browser APIs
    - CSS animations, Canvas, SVG, etc.
    - Some have been polyfilled (fetch, timers, console, etc.)
  - Navigation

## React Native Components
  - Not globally in scope like React web components
    - Import from 'react-native'
  - div -> View
  - span -> Text
    - All text must be wrapped by a <Text /> tag
  - button -> Button
  - ScrollView
    [see documentation for more compenents and APIs](https://facebook.github.io/react-native/docs/components-and-apis.html)

## Style
  - React Native uses JS objects for styling
  - Object keys are based on CSS properties
  - Flexbox layout
    - Default to column layout
  - Lengths are in unitless numbers
  - `style` prop can take an array of styles
  - `StyleSheet.create()`
    - Functionally the same as creating objects for style
    - Additional optimization: only send IDs over the bridge
