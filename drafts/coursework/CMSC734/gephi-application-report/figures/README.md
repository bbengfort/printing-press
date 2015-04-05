# Gephi Network Images

In this document we describe the creation of the images using Gephi as a step-by-step, repeatable process. These processes will be used on each of our email graphs (both Kostas and Ben's) so that we can have an equivalent set of images to post in the paper. These processes will generate 8 total images, 4 sets of two images each.

First a descriptive set of images will be created- just the whole graphs in their complex form. Second a graph using motif simplification will be used. Third a graph for betweenness centrality will be used. Finally a graph for clustering will be demonstrated.

## Descriptive Graphs

1. Nodes --> Rank Parameter is Degree
    - logarithmic spline both size & color
    - min size = 20, max size = 200
2. Edges --> Rank Parameter is Weight, exponential spline
2. Filter --> K-Core, Degree = 3 (only keep nodes with degree=4)
3. Layout --> Yifan Yu Proportional

## Motif Simplification

## Betweenness Centrality

## Clustering
