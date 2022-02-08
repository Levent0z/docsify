[Time-box Bomb](https://jsfiddle.net/pqL65vrc/2/) - Check for high-CPU util?

## CSS conditional selector example

```css
:host:not(:last-child):not(:empty) {
}
```

## Old Windows & Internet Explorer Virtual Machines

https://developer.microsoft.com/en-us/microsoft-edge/tools/vms/

> The password to your VM is "Passw0rd!"

## Graphviz

[Quick Introduction](https://www.worthe-it.co.za/blog/2017-09-19-quick-introduction-to-graphviz.html)
[Online Playground](http://magjac.com/graphviz-visual-editor)
[Documentation](https://www.graphviz.org/documentation/)

### Invisible node

```
node_		 [
			fixedsize=true,
			height=0,
			shape="",
			style=invis,
			width=0];
```

### Connect subgraphs

put `compound=true` in the graph.
Use this approach:

```
v1 -> v2 [ltail=cluster0,lhead=cluster1];
```

### Portrait vs Landscape

[Example](https://stackoverflow.com/questions/28913213/graphviz-arranging-clusters-left-to-right-with-contents-top-to-bottom)
// rankdir can be top-bottom (TB) or left-right (LR).
// Default is TB, which lays out clusters LR.
// If you want cluster nodes to be TB, set graph's rankdir to LR.
graph [rankdir=LR]

## Turn off bouncing icon

```sh
$ defaults write com.apple.dock no-bouncing -bool TRUE
$ killall Dock
```

## Highglight HTML element on hover

[Example](https://stackoverflow.com/questions/4445102/google-chrome-extension-highlight-the-div-that-the-mouse-is-hovering-over)
