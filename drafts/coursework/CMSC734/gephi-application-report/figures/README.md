# Gephi Network Images

In this document we describe the creation of the images using Gephi as a step-by-step, repeatable process. These processes will be used on each of our email graphs (both Kostas and Ben's) so that we can have an equivalent set of images to post in the paper. These processes will generate 8 total images, 4 sets of two images each.

First a descriptive set of images will be created- just the whole graphs in their complex form. Second a graph using motif simplification will be used. Third a graph for betweenness centrality will be used. Finally a graph for clustering will be demonstrated.

Save images from "Preview" Mode with the following settings:

1. Node border width 4.0, opacity 100%, color [0,0,0]
2. Show edges, thickness 2.0, curved, radius 3.0

Export to PNG:

- transparent background
- 5000px by 5000px 
- Margin 2%

## Descriptive Graphs

1. Nodes --> Rank Parameter is Degree
    - logarithmic spline both size & color
    - min size = 20, max size = 200
2. Edges --> Rank Parameter is Weight, exponential spline
2. Filter --> K-Core, Degree = 3 (only keep nodes with degree=4)
3. Layout --> Yifan Yu Proportional
    - optimal distance: 200
    - relative strenght: 0.6

## Motif Simplification

## Betweenness Centrality

## Clustering

In order to make the clusters of the network emerge, we used the below techniques on the initial graph.

1. Filter out nodes with small degree by using _K-Core_ filtering in Filters -> Topology -> K-Core. Using K=2. (This means filter out any nodes that have a degree of less than 2)
2. Layout graph by running the _Fruchterman Reingold_ algorithm under Layout. Wait until it converges to a satisfactory layout and then _Stop_ it.
3. Under Statistics, run _Modularity_. This creates the clusters. In the prompt, uncheck _"use weights"_. Depending on how many clusters the algorithm should return, use a lower _"resolution"_ value for many different clusters (1.0 is fine), and higher for a smaller number of clusters.
4. Under _Partition_ -> _Nodes_, click the refresh button, and then select _Modularity Class_. The colors of the clusters can be altered as needed.
5. Under _Ranking_ -> _Nodes_, under Size/Weight (symbol that looks like a ruby), choose _Betweenness Centrality_ to make the nodes more visible.
