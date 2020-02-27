# html5-canvas-boilerplate
Boilerplate code to start developing in HTML5 canvas

index.html
```html
<!DOCTYPE html>
<html>
    <head>
        <meta charset="utf-8">
        <meta name="viewport" content="width=device-width">
        <title>HTML5 Canvas Boilerplate</title>
        <style type="text/css">
            * {
                margin: 0;
                padding: 0;
            }

            html, body, canvas {
                position:fixed;
                width: 100%;
                height:100%;
            }
        </style>
    </head>
    <body>
        <canvas></canvas>
        <script src="script.js"></script>
    </body>
</html>
```


script.js
```javascript
const ctx = document.querySelector('canvas').getContext('2d')
const state = {
   w: document.documentElement.clientWidth,
   h: document.documentElement.clientHeight,
   keyState: {},
   keys: {
      LEFT: 37, UP: 38, RIGHT: 39, DOWN: 40, SPACE: 32
   },
   frameCount: 0,
   mouseX: 0,
   mouseY: 0,
   mouseDown: false,
   score: 0,
   screen: null
}

window.onload = init

function init() {
   state.screen = new Screen()
   input()
   fit()
   frame()
}

function frame() {
   window.requestAnimationFrame(frame)
   fit()
   ctx.clearRect(0, 0, state.w, state.h)
   state.screen.update()
   state.screen.render()
   state.frameCount++
}

function fit() {
   state.w = document.documentElement.clientWidth
   state.h = document.documentElement.clientHeight
   
   ctx.canvas.width = state.w
   ctx.canvas.height = state.h
}



function input() {
   
   document.body.addEventListener('mousedown', function () {
      state.mouseDown = true
   })
   
   document.body.addEventListener('mouseup', function() {   
      state.mouseDown = false
   })
   
   document.body.addEventListener('touchstart', function () {
      state.mouseDown = true
   })
   
   document.body.addEventListener('touchend', function () {
      state.mouseDown = false
   })
   
   document.body.addEventListener('mousemove', function (e) {
      state.mouseX = e.clientX
      state.mouseY = e.clientY
   })
   
   document.body.addEventListener('keydown', function (e) {
      state.keyState[e.keyCode] = true
   })
   
   document.body.addEventListener('keyup', function (e) {
      delete state.keyState[e.keyCode]
   })
   
}


function Screen() {
  
}

Screen.prototype.render = function () {
   ctx.fillStyle = '#555555'
   ctx.fillRect(0, 0, state.w, state.h)
}

Screen.prototype.update = function () {
 
}
```
