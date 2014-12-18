pixelratio-screenshots
======================

Grab a screenshot of a website, defining your own pixelratio. Uses phantomjs.


## Installation

* Install PhantomJS, from [here](http://phantomjs.org/download.html)
* Download this repository
* Run `phantomjs pixelratio.js [url] [file] [pixelRatio]`

## How does it work?

Obviously, as the engine, it uses PhantomJS. However, by default PhantomJS does not allow you to set the pixelratio (think retina). `pixelratio-screenshots` allows you to take a screenshot of a website, in the pixelratio that you define.

To take a retina screenshot, simply supply the URL, a destination folder and give "2" as the pixelRatio.

On a deeper level, what this does is an extremely hacky solution to make these screenshots possible.

First, it kills all javascript loads and later removes the script tags from the source page, and saves these to an array. Then, it overwrites the `window.devicePixelRatio`, to set it to the value you supplied.

Now that the `window.devicePixelRatio` is overwritten, we can start loading in the JS we blocked earlier. Any `devicePixelRatio` sniffers will now see our value and will start loading retina images.

Lastly, the default viewport is "1440x900", I multiply this by the pixelRatio, after which the whole page is being scaled by a CSS scale action.

## Examples

Example: `phantomjs pixelratio.js https://www.github.com/ ~/Desktop/github.png 2`
![github](https://cloud.githubusercontent.com/assets/777823/5494082/196f797c-86f1-11e4-81e6-fb8513ffe894.png)

Example: `phantomjs pixelratio.js https://maps.google.com/ ~/Desktop/maps.png 2`
![maps](https://cloud.githubusercontent.com/assets/777823/5494089/226c686e-86f1-11e4-9340-9efbed795418.png)