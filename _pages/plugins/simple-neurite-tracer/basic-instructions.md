---
mediawiki: Simple_Neurite_Tracer:_Basic_Instructions
title: Simple Neurite Tracer › Basic Instructions
nav-links: true
nav-title: Basic Instructions
---

{% include warning/deprecated new="[SNT](/plugins/snt)"
  old="[Simple Neurite Tracer](/plugins/simple-neurite-tracer)" %}

#### Starting the PlugIn

When starting the plugin from the {% include bc path='Plugins|Segmentation|Simple Neurite Tracer'%} menu option, you should be presented with a dialog like this (outdated snapshot): ![](/media/plugins/simple-neurite-tracer/snt-initial-dialog.png)

The three pane view gives you views of the image stack through XZ and ZY planes as well as the standard XY view. First time users may find the three pane view confusing. However, it makes it much easier to pick out points in the stack in the Z direction.

Another option lets you choose whether you would like to see a 3D representation of your tracings. If you're unsure, leave this at the default (*Create new 3D Viewer*). Note however that, once obtained, tracings can be imported and rendered in the 3D viewer at any later time. Your next view of the image will be something like this: <img src="/media/plugins/simple-neurite-tracer/snt-tracer-starting.png" title="fig:Snt-tracer-starting.png" width="600" alt="Snt-tracer-starting.png" />

The top of the left hand dialog box should always give you an idea about the next steps in basic tracing of paths. However, the first step when you load a new image should probably be to enable the option for using Hessian-based analysis of the image - this is done via a checkbox a little further down the dialog box. It will take some time to calculate the Gaussian convolution of the image once you select this option, but this only needs to be done once per image, so it's best to do it at the start. There is more on the use of this option in the [Tips](#miscellaneous-tips) section below.

*At this point, you may wish to switch to some shorter [step-by-step](/plugins/simple-neurite-tracer/step-by-step-instructions) instructions - some people have suggested that the description below is a bit verbose. Alternatively, carry on below...*

Now, as the instructions suggest, your next step should be to click on the point in the image stack where you want to start the path. To navigate in the stack you would adjust the slices scroll bar or used the {% include key key='<' %} and {% include key key='>' %} keys as usual. The red cross-hairs indicate the corresponding position in the three different views of the stack, but the slice positions will not be synchronized between the three windows unless you hold down {% include key key='Shift' %} while moving the mouse or activate the *Enable cursor snapping* option (window synchronization is particularly useful if you're creating a [branching branch](#branching-and-joining-paths) at the beginning or end of a path).

![A temporary path, yet to be confirmed.](/media/plugins/simple-neurite-tracer/snt-temporary-path.png) ![The progress of the search for a temporary path.](/media/plugins/simple-neurite-tracer/snt-searching-for-path.png) ![The confirmed part of the current path.](/media/plugins/simple-neurite-tracer/snt-confirmed-path.png) Select a point for the start of your first path. The instructions should change to prompt you to find another point further along the structure that you're tracing. It will take some trial and error to find out how far apart these points can be for each image - some will have very clearly defined neurons and so they can be very far apart, but with more difficult images (or ones where the path found is not the one you intend) you will need to make them closer together.

Once you select that next point in the path you will either find that the path is found immediately, in which case the projected path is visible as a dark blue line, or the search may take longer, in which case the progress of the search is shown in light blue.

While the plugin is searching you can still move about in the image stack to see the progress through the depth of the stack as well. If it seems to be taking a very long time to find a path between the points you should probably cancel the search (by pressing {% include key key='Esc' %}) and try a point that's nearer, since the path searching slows down as it has explored more of the image.

Once you have a dark blue temporary path like that in the left hand image the instructions will prompt you to either keep that path segment (by pressing {% include key key='Y' %}) or cancel it ({% include key key='N' %}) to try picking another point (probably one nearer to the original point). If you confirm that path then the path will turn red, to indicate that this is a confirmed part of the current path. If you click further along the structure again then the dark blue colour will again show the temporary part of a path as opposed to the red confirmed part.

Once you have picked out a few more points along the path, you can complete the path by clicking "Complete Path" {% include key key='F' %} at the top of the dialog. By default - Paths can be colorized at any later point using the drop-down menu in the *Paths* window - completed paths are shown in magenta and appear in the path list in the tracer's dialog box. If you select one or many paths in this list, the selected paths are shown in green instead. (You need to have particular paths selected for filling out neurons or branching and joining paths.) ![Several completed paths, with one selected (in green)](/media/plugins/simple-neurite-tracer/snt-multiple-paths.png)

You've probably noticed that the default presentation of the paths in an image is to show the a projection of the path through the entire stack, rather than just those points of the path that are in the current slice. This can become confusing with many paths in a single image, in which case you should change the *View Paths 2D* option from *Projected through all slices* to *Parts in nearby slices* (shortcut: {% include key key='5' %}).

#### Branching and Joining Paths

In this plugin each path can only be a linear succession of points in the image. However, you can indicate more complex structures by creating a path that starts on another path (branches off it) or ends on another path (joins the other path). To do this you have to select the existing path you want to branch off or join to in the path list (check that the right path is green in the image) and then hold down {% include key key='Ctrl' %} (on Windows or Linux) or {% include key key='option' style='mac' %} (on MacOS) while you select the branch or join point. You almost always will want to hold down {% include key key='Shift' %} as well as {% include key key='Ctrl' %} / {% include key key='Alt' %} while you're finding this image so that the crosshairs show you the exact point that you're joining to. The detailed procedure is described [here](Simple_Neurite_Tracer__Step-By-Step_Instructions#branching-start-a-path-on-an-existing-path).

#### Saving and Loading Files

You can load and save traces files with the corresponding buttons at the bottom of the tracer's dialog box. I suggest that you save your files with the original filename with the extension changed to ".traces", so "test.tif" would have a traces file "test.traces". This is because the "Load Traces File" option will look for a file with that name and offer to load it for you.

#### Filling Out Neurons

There is a simple facility in this plugin for "filling out" paths to volumes. This is not particularly sophisticated, but often good enough for a rough visualization of the shape of a neuron beyond what can be seen from the traced path.

First, select the one or more paths that you want to fill out from in the path list and select "Fill Out Path(s)" in the interface. The selected paths are shown in green so that you can check that you're starting from the right ones. After a couple of seconds if you scroll through the stack you should be able to see a thick green suround to the path:

![A few seconds after selecting "Fill Out Path(s)" with 3 branched paths selected](/media/plugins/snt/snt-initial-filling.png)

The filler continues to explore the image starting from the path until you click "Pause" in the dialog. However, the fill which is shown only includes those points up to a certain threshold distance from the path. (Note that in this section "distance" doesn't mean a real physical distance, but a measure which takes into account the intensity values of the pixels which must be passed through when moving away from the path.) Information about the current threshold and the progress of the search is shown in the dialog. ![The filling-related part of the dialog (outdated screenshot).](/media/snt-filling-statistics.png)

The top line ("Not reached by search yet") is updated as you move your mouse over the image. If the point under the mouse has been reached by the search then it will show you that point's distance from the path. In the line below, the input box shows your current threshold distance: so if this is set to 0.2 then that means that all points less than 0.2 from the path are included in the fill (and shown in green in the image.) The number in parentheses at the right of this line show the maximum distance from the path that has been completely explored.

You can change the fill threshold in one of three ways:

-   Clicking on a point in the image that has been reached by the search (This is the most intuitive way of altering the threshold).
-   Changing the threshold in the input box manually and clicking the "Set" button below it.
-   Clicking the "Set Max" button below the threshold input box, which sets the threshold to the maximum explored distance (the value shown in parentheses).

Anyway, assuming that you want to use the first of these approaches, you should use the approach described below. It is difficult to set the threshold accurately from the image unless you zoom in, so first zoom on part of the path that you want to set the threshold for: ![After having zoomed in on part of the fill](/media/snt-zoomed-filling.png)

{% include clear%}


Since the the solid green fill obscures the intensity value of the points in the fill, I suggest that you switch to the semi-transparent view of the fill at this stage by selecting the "Transparent fill display" option in the dialog. This should show you something like this:

![Having made the fill transparent](/media/snt-transparent-filling.png)

{% include clear%}


As you can see in this image, the threshold is set too far from the path, since there are many completely dark points under the green fill. Experiment with clicking on different points closer to the path in order to adjust the threshold until you are happy with it. You might end up with something like this:

![Having refined the fill by clicking closer to the path](/media/snt-refined-filling.png)

{% include clear%}


If you are happy with this, then you might as well click "Pause" so that your computer isn't spending all its CPU on continuing to explore the image. Then you can either save the fill (which will add it to the fill list) by clicking "Save Fill", discard the fill by clicking "Cancel Fill" or use the "Create Image Stack from Fill" button to view the same image stack, but with only the points in that fill preserved. One reason why you might want to do this is that you can then smooth that image and use the [3D Viewer](/plugins/3d-viewer) to do a surface rendering of the neuron. Perhaps then you could overlay that onto a volume rendering of the complete image (see available [tutorials](/plugins/snt#tutorials)). Or, you could save those fill stacks for each of the neurons you fill and then combine them in ImageJ using "RGB Merge".

The image stack you would get from the image used in this example might look something like this: ![Having selected the "Create Image from Fill" option](/media/plugins/snt/snt-filling-viewed.png)

{% include clear%}


#### Using an AmiraMesh Labels File

If you have a labels file for your image, you can load that file to help you make sure that your tracings are going between the regions of the image that you think they are. (e.g. it's possible when a neuron enters a region of dense expression to stop the path short of the regions which is actually labelled as a particular neuropil region.) Load the label file by clicking the "Load Labels" button. If you have a label file loaded then the current material under the crosshairs will be shown in the ImageJ status bar.

#### Key Shortcuts

Key Shortcuts and keyboard accelerators are described in [Key Shortcuts](/plugins/snt/key-shortcuts).

#### Miscellaneous Tips

-   The simplest way to follow a path through a stack is to select that path and hold down {% include key key='Ctrl' %} / {% include key key='Alt' %} and {% include key key='Shift' %} while moving the mouse along it.
-   If the search doesn't seem to be finding the route you expect through an image stack, try toggling the "Hessian analysis" option. Another alternative is that the start point of the search is in the wrong place (e.g. if you accidentally clicked in the image when you didn't want to start a new path - you should be able to tell this from the progress of the search, which starts at both the start and end point).
