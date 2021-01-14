# Graphviz

This is a quick description of Graphviz, a set of graphing technologies originally developed by AT&T. Graphviz generates visuals based on text-based description of graphs. To be clear, "graph" in this context is a set of nodes optionally connected to other node. Graphviz is not an all-purpose diagraming technology like Visio, Lucid Chart or Draw.io or even (gasp!) PowerPoint, but is quite powerful none-the-less. 

## Why Graphviz?
Using text to describe a graph, which is easily understood visually, seems curious. So why bother? Graphviz automatically generates the graph layout (i.e. positions the nodes and the edges) so the author can focus on the essence of the graph: the elements and their relationships.

There are secondary benefits. Some users prefer typing over mouse-jockeying. Text is easily source-controlled. Many CLI tools and applications across platforms understand the Graphviz format as input and output many formats, such as PNG or PostScript.

The decision to use Graphviz instead of an alternative will depend on several factors:

1. The nature and complexity of the graph

    Although Graphviz _can_ be used to build complex graphs, it's not necessarily the best option for every graph domain. Having to use advanced features of Graphviz and the complexity of the resulting text source makes it less than ideal for complex use-cases. In my humble opinion, Graphviz seems best suited for graphs that appear in academic contexts such as state machines or data structures.

2. The familiarity of the author(s) with the Graphviz language.

    All collaborators need to be familiar with the Graphviz language, which may be a deal breaker. It's easy to get started with Graphviz, the learning curve is reasonable, and generating simple graphs is straightforward. Knowledge of more advanced features are needed to achieve a certain look for the graph.

3. The availability of Graphviz tools on the chosen platform.

## References




