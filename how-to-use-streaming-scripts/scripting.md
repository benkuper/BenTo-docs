# Scripting

Script light blocks enables to you to create custom effects by writing JavaScript code. You can create a new Script light block by clicking the green plus icon next to "Scripts" in the light blocks panel. Then you need to create a new text file in your filesystem. You then select the text file in the file path parameter. Now it's time to add some code to the file.

{% hint style="success" %}
_You can find some_ [_example script files on the Github page_](https://github.com/benkuper/BenTo) _of the Bento project._
{% endhint %}

## Creating Parameters

At first, we want to create some parameters that we want to control on the light block. We can use the script object to add custom parameters, as well as log debug infos in the Logger panel.

For example if we want to create a Parameter called position with a default value of 0.5 and range between 0 and 1 we can use the following code:\
`script.addFloatParameter("Position", "The position of the point", 0.5, 0,1);`

Below you find a full reference of methods available through the script object.

## Script object&#x20;

Here is a full reference of methods available on the script object:

| Method                                                                             | Description                                                                                                                                                                                                                                                      | Example                                                                                                                                                                                                                                                         |
| ---------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **addFloatParameter(**_name, description, default, min max_**)**                   | This will add a float number parameter (slider).                                                                                                                                                                                                                 | `script.addFloatParameter("My Float Param","Description of my float param",.1,0,1);`                                                                                                                                                                            |
| **addIntParameter(**_name, description, default, min max_**)**                     | add an integer number parameter (stepper), default value of 2, with a range between 0 and 10                                                                                                                                                                     | `script.addIntParameter("My Int Param","Description of my int param",2,0,10);`                                                                                                                                                                                  |
| **addBoolParameter(**_name, description, default_**)**                             | add a boolean parameter (toggle)                                                                                                                                                                                                                                 | `script.addBoolParameter("My Bool Param","Description of my bool param",false);`                                                                                                                                                                                |
| **addStringParameter(**_name, description, default_**)**                           | add a string parameter (text field)                                                                                                                                                                                                                              | `script.addStringParameter("My String Param","Description of my string param", "cool");`                                                                                                                                                                        |
| **addColorParameter(**_name, description, default_**)**                            | <p>add a color parameter (color picker).</p><p>You can either set the default color with ARGB hex value, [r,g,b,a] float array, or r,g,b,a separate values. r, g and b values are always between 0 and 1 and alpha is optional (you can specify r,g,b only);</p> | <p><code>script.addColorParameter("My Color Param","Description of my color param",0xff0000ff); //default blue alpha 100%</code></p><p><code>script.addColorParameter("My Color Param 2 ","Description of my color param",[1,0,1]); //default purple</code></p> |
| **addEnumParameter(**_name, description, label1, value1, label2, value2, .._.**)** | <p>add a enum parameter (dropdown with options)</p><p>Each pair of values after the first 2 arguments define an option and its linked data</p>                                                                                                                   | `script.addEnumParameter("My Enum Param","Description of my enum param", "Option 1", 1,"Option 2", 5, "Option 3", "banana");`                                                                                                                                   |
| **log(**_message_**)**                                                             | Logs a message (must activate "Log" in the script parameters)                                                                                                                                                                                                    | `script.log("This is a message");`                                                                                                                                                                                                                              |
| **logWarning(**_message_**)**                                                      | Logs a message as a warning                                                                                                                                                                                                                                      | `script.logWarning("This is a warning");`                                                                                                                                                                                                                       |
| **logError(**_message_**)**                                                        | Logs a message as an error                                                                                                                                                                                                                                       | `script.logError("This is an error");`                                                                                                                                                                                                                          |

## Create the updateColors function

Next, we create a function called updateColors. The JavaScript Runtime of Bento will call this function for each prop whenever it needs to output colors from the script light block. It will also pass in the following parameters that can be used to create the actual colors:

* **colours**: object create colors and output colors
* **id**: Prop ID of the prop to create colors for.
* **resolution**: Number of LEDs of the prop to create colors for.
* **time**: time reference in seconds as float (for normal light blocks this is the time since system start, for light blocks inside a timeline it's the timeline's current time)
* **params**: object containing the parameters created through the script object

{% hint style="warning" %}
_**In JavaScript the order of the parameters is relevant!**_
{% endhint %}

Example code to create the updateColors function:

`function updateColors(colours, id, resolution, time, params) {`\
&#x20;  `// actual code creating colors goes here`\
`}`

### **Colours parameter object**

We can use the colours object passed to the updateColors function to output colors. For example, if we want to output all white LEDs we would use the following code:

```
function updateColors(colours, id, resolution, time, params) {	
	for(var i = 0 ; i < resolution ; i++) {
		colours.set(i,1,1,1);
	}
} 
```

We use a for loop to set the color for each LED. The colours.set method takes the index/position of the LED as the first argument and then uses 3 float values for the red, green, blue channel.&#x20;

### Methods that create and output colors:

* **colours.set**(index, red, green, blue, alpha): Set a single index/LED to the given RGB color
* **colours.setHSV**(index, hue, saturation, value): Set a single index to the given HSV color
* **colours.fill**(red, gree, blue): Fill all LEDs with the given RGB color
* **colours.fillHSV**(hue, saturation, value): Fill all LEDs with the given HSV color
* **colours.point**(rgbaArray, position, radius): Create a point at the given position with radius and RGB color
* **colours.pointHSV**(hsvArray, position, radius): Create a point at the given position with radius and HSV color
* **colours.gradient**(rgbaArray, rgbaArray2, startPosition, endPosition): Create a gradient from two RGB colors and fill the LEDs within the given startPosition and endPosition
* **colours.gradientHSV**(hsvArray, hsvArray2, startPosition, endPosition): Create a gradient from two HSV colors and fill the LEDs within the given startPosition and endPosition

### Helper methods:

* **colours.lerpColor**(color1, color2, interpolationPosition): Calculate a linear interpolation between two colors based on a given float indicating the position
* **colours.getHSV**(color): Get a HSV color representation for the given color
