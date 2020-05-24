# Timeline

A timeline light block let's you arrange other light blocks into a sequence. It is a powerful mechanism for building light shows timed to music.

You can create a new timeline light block by clicking on the green plus icon next to "Timeline" in the light blocks panel.

## Interface

When you have the timeline light block selected the inspector will display the parameters of the timeline. Here you can change e.g. the total time of the timeline and wether or not the sequence should loop.

A timeline can consists of several layers. The block layers can contain light blocks. The audio layers can contain music files. 

{% hint style="success" %}
**SHORTCUTS AND NAVIGATION  
- Drag the blue bar horizontal / vertical :** Zoom in/out and change the time focus frame  
**-  Right click on the blue bar :** Reset the view to a full view of the whole sequence  
**- Ctrl + C, Ctrl + V, Ctrl + D :** Copy, paste, duplicate items \(This applies to blocks and layers. When pasting layers make sure to select the timeline panel\)
{% endhint %}

![](../../.gitbook/assets/screenshot-2020-05-24-at-16.48.39.png)

## Add a music file

To add a music file click the green plus icon above the layers and select "Audio". Then double click on the  created audio layer and select an audio file from the file dialog.

You can fine tune details of the audio block by clicking on it. This will show it's parameters in the inspector panel. Additionally, you can move the block to change it's start time. You can also use the nudges at the beginning and end of the block to crop the music clip.

## Adding light blocks to a layer

You can add light blocks to a block layer in the following ways:

* Drag and Drop a light block from the light block panel onto the block layer.
* Double-clicking on the block layer will create an empty block. You can then set a light block in it's inspector parameters.
* Copy and Paste from other layers: Select light block, press Ctrl+C =&gt; select layer, press Ctrl+V

The light blocks will display a visual representation of the output.

### Animating parameters

You can animate parameters of the light blocks by right-clicking on the light block and selecting "Edit" and the respective parameter. This will enable a curve automation where you can add keyframes by double-clicking. You can change the interpolation between keyframes by clicking the line between two keyframes.

![](../../.gitbook/assets/bento-timeline-parameter-animation.png)

If you want to control an additional parameter with an automation curve, again right-click on the light block and select the new parameter. This will switch the curve keyframe to the newly selected parameter.

After creating the keyframes, right-click on the light block and select "Clear automation editor". This will let you manipulate the light block in the usual way.

### Targeting a prop





