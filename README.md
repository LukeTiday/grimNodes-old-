# GrimNodes
GrimNodes is a node based VFX application built on litegraph.js

it is a lightweight VFX application that favors a Procedural/Node based approach to tool building.


## Features
- Renders on Canvas2D (zoom in/out and panning, easy to render complex interfaces, can be used inside a WebGLTexture)
- Easy to use editor (searchbox, keyboard shortcuts, multiple selection, context menu, ...)
- Optimized to support hundreds of nodes per graph (on editor but also on execution)
- Customizable theme (colors, shapes, background)
- Callbacks to personalize every action/drawing/event of nodes
- Subgraphs (nodes that contain graphs themselves)
- Live mode system (hides the graph but calls nodes to render whatever they want, useful to create UIs)
- Graphs can be executed in NodeJS
- Highly customizable nodes (color, shape, slots vertical or horizontal, widgets, custom rendering)
- Easy to integrate in any JS application (one single file, no dependencies)
- Typescript support

## Nodes provided
Although it is easy to create new node types, LiteGraph comes with some default nodes that could be useful for many cases:
- Interface (Widgets)
- Math (trigonometry, math operations)
- Audio (AudioAPI and MIDI)
- 3D Graphics (Postprocessing in WebGL)
- Input (read Gamepad)

## Installation

downloading the repository
open the MAIN.html in your favorite browser


## How to code a new Node type

Here is an example of how to build a node that sums two inputs:

```javascript
//node constructor class
function MyAddNode()
{
  this.addInput("A","number");
  this.addInput("B","number");
  this.addOutput("A+B","number");
  this.properties = { precision: 1 };
}

//name to show
MyAddNode.title = "Sum";

//function to call when the node is executed
MyAddNode.prototype.onExecute = function()
{
  var A = this.getInputData(0);
  if( A === undefined )
    A = 0;
  var B = this.getInputData(1);
  if( B === undefined )
    B = 0;
  this.setOutputData( 0, A + B );
}

//register in the system
LiteGraph.registerNodeType("basic/sum", MyAddNode );

```

or you can wrap an existing function:

```js
function sum(a,b)
{
   return a+b;
}

LiteGraph.wrapFunctionAsNode("math/sum",sum, ["Number","Number"],"Number");
```

## Feedback
--------

You can write any feedback to luketiday@gmail.com

## Contributors

- Luke Tiday @man.in.motion
- everyone who contributed to litegraph.js https://github.com/jagenjo/litegraph.js/blob/master/guides/README.md