# cheerpj-natives

[![Discord server](https://img.shields.io/discord/988743885121548329?color=%237289DA&logo=discord&logoColor=ffffff)](https://discord.leaningtech.com)

A collection of alternative implementations of [native libraries](https://labs.leaningtech.com/cheerpj3/guides/Implementing-Java-native-methods-in-JavaScript) to be used when running Java applications with [CheerpJ](https://labs.leaningtech.com/cheerpj).

Currently only a partial implementation of LWJGL is included.

# Usage

1. [Download cheerpj-natives](https://github.com/leaningtech/cheerpj-natives/archive/refs/heads/main.zip) and place the `cheerpj-natives` folder at the root of your web server.
2. Pass the following property to the `cheerpjInit` options: `javaProperties: ["java.library.path=/app/cheerpj-natives/natives"]`

## LWJGL

The LWJGL implementation requires that you provide a canvas for it to render to by setting `window.lwjglCanvasElement`.  If you don't do this, you'll see the following error:

> Error: window.lwjglCanvasElement is not set or is not a canvas

1. Add this HTML to the start of the document body:
```html
<canvas id="lwjgl" width="800" height"600"></canvas>
```
2. In your script, add the following line before the `cheerpjRunMain` or `cheerpjRunJar` call:
```js
window.lwjglCanvasElement = document.getElementById("lwjgl");
```

### Example

Following from the [getting started tutorial](https://labs.leaningtech.com/cheerpj3/getting-started/Java-app):

```html
<canvas id="lwjgl"></canvas>
<script type="module">
  await cheerpjInit({
    javaProperties: ["java.library.path=/app/cheerpj-natives/natives"],
  });
  cheerpjCreateDisplay(800, 600);
  window.lwjglCanvasElement = document.getElementById("lwjgl");
  await cheerpjRunJar("/app/CHANGEME.jar");
</script>
```
