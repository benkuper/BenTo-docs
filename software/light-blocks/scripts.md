# Scripts

Script light blocks enables to you to create custom effects by writing JavaScript code. You can create a new Script light block by clicking the green plus icon next to "Scripts" in the light blocks panel. Then you need to create a new text file in your filesystem. You then select the text file in the file path parameter. Now it's time to add some code to the file.

_Hint: You can find some_ [_example script files on the Github page_](https://github.com/benkuper/BenTo) _of the Bento project._

## Creating Parameters

At first, we want to create some parameters that we want to control on the light block. We can use the script object to add custom parameters, as well as log debug infos in the Logger panel.

For example if we want to create a Parameter called position with a default value of 0.5 and range between 0 and 1 we can use the following code:  
`script.addFloatParameter("Position", "The position of the point", 0.5, 0,1);`

Below you find a full reference of methods available through the script object.

## Script object 

Here is a full reference of methods available on the script object:

<table>
  <thead>
    <tr>
      <th style="text-align:left">Method</th>
      <th style="text-align:left">Description</th>
      <th style="text-align:left">Example</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left"><b>addFloatParameter(</b><em>name, description, default, min max</em><b>)</b>
      </td>
      <td style="text-align:left">This will add a float number parameter (slider).</td>
      <td style="text-align:left"><code>script.addFloatParameter(&quot;My Float Param&quot;,&quot;Description of my float param&quot;,.1,0,1);</code>
      </td>
    </tr>
    <tr>
      <td style="text-align:left"><b>addIntParameter(</b><em>name, description, default, min max</em><b>)</b>
      </td>
      <td style="text-align:left">add an integer number parameter (stepper), default value of 2, with a
        range between 0 and 10</td>
      <td style="text-align:left"><code>script.addIntParameter(&quot;My Int Param&quot;,&quot;Description of my int param&quot;,2,0,10);</code>
      </td>
    </tr>
    <tr>
      <td style="text-align:left"><b>addBoolParameter(</b><em>name, description, default</em><b>)</b>
      </td>
      <td style="text-align:left">add a boolean parameter (toggle)</td>
      <td style="text-align:left"><code>script.addBoolParameter(&quot;My Bool Param&quot;,&quot;Description of my bool param&quot;,false);</code>
      </td>
    </tr>
    <tr>
      <td style="text-align:left"><b>addStringParameter(</b><em>name, description, default</em><b>)</b>
      </td>
      <td style="text-align:left">add a string parameter (text field)</td>
      <td style="text-align:left"><code>script.addStringParameter(&quot;My String Param&quot;,&quot;Description of my string param&quot;, &quot;cool&quot;);</code>
      </td>
    </tr>
    <tr>
      <td style="text-align:left"><b>addColorParameter(</b><em>name, description, default</em><b>)</b>
      </td>
      <td style="text-align:left">
        <p>add a color parameter (color picker).</p>
        <p>You can either set the default color with ARGB hex value, [r,g,b,a] float
          array, or r,g,b,a separate values. r, g and b values are always between
          0 and 1 and alpha is optional (you can specify r,g,b only);</p>
      </td>
      <td style="text-align:left">
        <p><code>script.addColorParameter(&quot;My Color Param&quot;,&quot;Description of my color param&quot;,0xff0000ff); //default blue alpha 100%</code>
        </p>
        <p><code>script.addColorParameter(&quot;My Color Param 2 &quot;,&quot;Description of my color param&quot;,[1,0,1]); //default purple</code>
        </p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left"><b>addEnumParameter(</b><em>name, description, label1, value1, label2, value2, ..</em>.<b>)</b>
      </td>
      <td style="text-align:left">
        <p>add a enum parameter (dropdown with options)</p>
        <p>Each pair of values after the first 2 arguments define an option and its
          linked data</p>
      </td>
      <td style="text-align:left"><code>script.addEnumParameter(&quot;My Enum Param&quot;,&quot;Description of my enum param&quot;, &quot;Option 1&quot;, 1,&quot;Option 2&quot;, 5, &quot;Option 3&quot;, &quot;banana&quot;);</code>
      </td>
    </tr>
    <tr>
      <td style="text-align:left"><b>log(</b><em>message</em><b>)</b>
      </td>
      <td style="text-align:left">Logs a message (must activate &quot;Log&quot; in the script parameters)</td>
      <td
      style="text-align:left"><code>script.log(&quot;This is a message&quot;);</code>
        </td>
    </tr>
    <tr>
      <td style="text-align:left"><b>logWarning(</b><em>message</em><b>)</b>
      </td>
      <td style="text-align:left">Logs a message as a warning</td>
      <td style="text-align:left"><code>script.logWarning(&quot;This is a warning&quot;);</code>
      </td>
    </tr>
    <tr>
      <td style="text-align:left"><b>logError(</b><em>message</em><b>)</b>
      </td>
      <td style="text-align:left">Logs a message as an error</td>
      <td style="text-align:left"><code>script.logError(&quot;This is an error&quot;);</code>
      </td>
    </tr>
  </tbody>
</table>## Create the updateColors function

Next, we create a function called updateColors. The JavaScript Runtime of Bento will call this function for each prop whenever it needs to output colors from the script light block. It will also pass in the following parameters that can be used to create the actual colors:

* **colours**: object create colors and output colors
* **id**: Prop ID of the prop to create colors for.
* **resolution**: Number of LEDs of the prop to create colors for.
* **time**: time reference in seconds as float \(for normal light blocks this is the time since system start, for light blocks inside a timeline it's the timeline's current time\)
* **params**: object containing the parameters created through the script object

_**Notice: In JavaScript the order of the parameters is relevant!**_

Example code to create the updateColors function:

`function updateColors(colours, id, resolution, time, params) {  
   // actual code creating colors goes here  
}`

### _**Colours parameter object**_

We can use the colours object passed to the updateColors function to output colors. For example, if we want to output all white LEDs we would use the following code:

```text
function updateColors(colours, id, resolution, time, params) {	
	for(var i = 0 ; i < resolution ; i++) {
		colours.set(i,1,1,1);
	}
} 
```

We use a for loop to set the color for each LED. The colours.set method takes the index/position of the LED as the first argument and then uses 3 float values for the red, green, blue channel. 

Methods that create and output colors:

* **colours.set**\(index, red, green, blue, alpha\): Set a single index/LED to the given RGB color
* **colours.setHSV**\(index, hue, saturation, value\): Set a single index to the given HSV color
* **colours.fill**\(red, gree, blue\): Fill all LEDs with the given RGB color
* **colours.fillHSV**\(hue, saturation, value\): Fill all LEDs with the given HSV color
* **colours.point**\(rgbaArray, position, radius\): Create a point at the given position with radius and RGB color
* **colours.pointHSV**\(hsvArray, position, radius\): Create a point at the given position with radius and HSV color
* **colours.gradient**\(rgbaArray, rgbaArray2, startPosition, endPosition\): Create a gradient from two RGB colors and fill the LEDs within the given startPosition and endPosition
* **colours.gradientHSV**\(hsvArray, hsvArray2, startPosition, endPosition\): Create a gradient from two HSV colors and fill the LEDs within the given startPosition and endPosition

Helper methods:

* **colours.lerpColor**\(color1, color2, interpolationPosition\): Calculate a linear interpolation between two colors based on a given float indicating the position
* **colours.getHSV**\(color\): Get a HSV color representation for the given color

