# Assignment 1:  Distribution Ray Tracing 

The code in this sample is a basic ray tracer, largely taken from the Typescript [samples](https://github.com/Microsoft/TypeScriptSamples) on github.com. It has been extended to show frames as they are rendering, allow the rendering resolution to be different than the canvas size, and rendering multiple frames to a video with the Whammy client-side WebM video encoder ([https://github.com/antimatter15/whammy]).

The goal of this assigment is to extend this simple raytracer to support distribution ray tracing.  You should read the introduction to Chapter 13 and section 13.4 in your textbook.

## Due: Friday September 11th, 5pm

## Overview 

You will implement two specific uses of distribution ray tracing:

1. *Antialiasing from jittered supersampling*, described in 13.4.1.  You should implement a 4x4 grid of samples, and select a random sample from each bin.
2. *Motion blur*, described in 13.4.5.  Each ray cast into the scene should have a random time in the video frame time interval associated with it, and that time should be used to compute all relevant properties of objects.

In addition, you should modify the sample code to have a more general camera model. Specifically, extend the Camera object to give direct control over the distance of the viewing plane from the camera position (the focal length) and the horizontal and vertical size of the viewing window.  This will allow you to change the field of view in both the horizontal and vertical directions.  

## Details

Here are some specific details to help you get started.

1. The distance, horizonal size and vertical size should be specified in world coordinates.  You should modify the Camera constructor to add new parameters:
```js
    constructor(public pos: Vector, lookAt: Vector, distance: number, hsize: number, vsize: number)
```
and update the object statue as needed.  You should 



http://www.iskysoft.com/convert-webm/play-webm-quicktime.html
http://video.online-convert.com/convert-to-mp4

You will have to modify the code for the ray tracer in two ways, one for each part of the assignment.

1. For antialiasing, you will have to cast multiple rays into the scene for each pixel, with their 

You will 

The sample code has been extended to support creating a video from a sequence of frames, where the rendering accepts a video *length* (in seconds) and *fps* (frames per second), and uses those to compute the number of frames.  You can use these parameters



1. a0.ts contains a lot of the code for this example, you should complete it.
2. pointset.ts is mostly empty, you need to implement the main PointSet class that is used by the application in a0.ts
3. PointSet should be implemented as a circular buffer, as described in the comments in the file.  The key feature of a circular buffer is that the contents of the buffer are never moved or copied as new elements are added or removed.  Instead, the index markers for the start and end are updated.  The interface methods of the class hide the implementation details from the programmer: they can simply request the first, second, third, etc. element as desired.
4. the program should create one "point" per animationFrame and store 30 points (1 second worth of data at 30 frames per second).  The points should be rendered such that they appear to fade out as the mouse moves.  New points should not be created when the mouse is outside of the canvas, but old ones should continue to disappear.
5. when the user clicks and drags, a grey hollow rectagle should be traced out from the start point to the current mouse location.  If the user releases the button, a rectangle of random color should be created.  If the user moves the mouse out of the canvas, the rectangle creation should be canceled.
6. the canvas should be redrawn each animation frame, and nothing should be drawn in the canvas outside of the render function.

Your grade will be based on satisfying each of these requirements.

# Submission

You should submit a clean project folder in a zip file to t-square.  That means should clean the folder before submission.  We suggest the following:

1. copy the folder to a new location 
2. delete the ".git", "js" and "node_modules" directories
3. delete ".gitignore"

You should have a0.html, a0.css, a0.ts, pointset.ts, README.md, tsconfig.json, package.json, gulpfile.js remaining (of the files in the sampel: you may have other files if you create them).

**Do Not Change the names** of a0.html and a0.ts.  The TAs need to be able to test your program as follows:

1. cd into the directory and run ```npm install```
2. compile with ```tsc```
3. open and view the web page ```a0.html```

Please test that your submission meets these requirements.  For example, once you create your zip file, extract it into a new folder and test these steps.
 
# Development Environment

The sample has already been set up with a complete project for Typescript development.

To work with this sample and prepare your submission, you should have Node (and in particular, npm) installed, which you can retrieve from [nodejs.org](http://nodejs.org).   

In addition to node, you should make sure Typescript is installed, as described at [www.typescriptlang.org](http://www.typescriptlang.org).

## Running 

You can compile the typescript to javascript and then open the html file in your web browser to run:
```
tsc
open a0.html   // on a mac
```

The project also includes a simple gulpfile.js to run a simple gulp-connect web server to serve up the files in this directory.  To use it, you must install all the required npm packages, and then run gulp to build the project and run the server:
```
npm install
gulp
```

You can run the sample by pointing your web browser at ```http://localhost:8080/a0.html```
