# Introduction

30th May, 2017 

# INTRODUCTION

Hello everyone ! My name is Mayank Kumar and I am a third year undergraduate student pursuing B.Tech in Computer Sciences from the Indian Institute of Technology (IIT) Ropar. I am a participant of the Google Summer of Code Programme, 2017, and will be working throughout the summer trying to make valuable contributions to RoboComp, the Open Source Robotics Framework. I enjoy playing cricket and spending time floating around in swimming pools, and writing code when I am dry. 

My task for GSoC 2017 is to improve upon the latest rcmanager tool and fill in the missing pieces of code. More specifically, I need to work upon the problem of graph cluttering. Whenever we try to load a massive component graph into the rcmanager, it fills up the entire window pane and muddles up, making it very difficult to work upon. I will work on developing some techniques and implementing them to ease working with large graphs. Apart from this, a few more bugs and tools need to be handled, and I hope to refine the rcmanager to an such extent where beta testing can be initiated on it.

The following milestones are what I plan to achieve while working on my project:

1) First evaluation - 

a) Understanding the current codebase - The new rcmanager has an intricate structure of encapsulated objects and inherited classes, and require a good understanding, to enable pushing pieces of code in between.

b) Adding support for graph panning - The current rcmanager does not support graph panning, which is a necessary tool to work with. 

c) Testing compatibility - Rcmanager already has many hold and drag functions, and should not be affected by the panning function. This step will ensure that the other functionalities remain unaffected.

2) Second evaluation - 

a) Switching all nodes back to the old representation - The current representation for each node is very bulky and requires a lot of space, whereas not all nodes are not in use at the same time, and need not show all details. The old rcmanager provides for a simple, smaller representation, which will enable viewing large graphs in a small window area.

b) Adding support for node expansion when hovering / zooming - The nodes should expand into the detailed views when necessary. Whether this is to be done while hovering or zooming in depends upon the user friendliness of each of the options.

3) Third evaluation -

a) Adding support for checking component validity - User inputs may quite often be erroneous and should be automatically checked and reported. Some checks will be added in this step to ensure that the components are defined correctly.

b) Complete the missing code for some tools - Backend code for a few tools is missing. The UI for those tools exist. Filing in the gaps is the aim of this step.

c) Initial bug testing and documentation - The current rcmanager does not have adequate documentation, making it difficult to work with. I intend to improve the documentation and perform some bug testing, to ensure any future work on this tool can be done with less effort.

I will keep updating the blog as and when I finish the aforementioned milestones, describing the work done in detail.

* * *

Mayank Kumar 
