# **Finding Lane Lines on the Road** 
---

**Project Finding Lane Lines on the Road**

The goals / steps of this project are the following:
* Make a pipeline that finds lane lines on the road
* Reflect on your work in a written report


[//]: # (Image References)

[imageGray]: ./examples/imageGray.jpg "Grayscale"
[imageBlur]: ./examples/imageBlur.jpg "Blurred image"
[imageCanny]: ./examples/imageCanny.jpg "Canny edges"
[imageClipped]: ./examples/imageClipped.jpg "Clipped image"
[imageHough]: ./examples/imageHough.jpg "Hough lines"
[imageFinal]: ./examples/imageFinal.jpg "Lane lines"


---

### Reflection

### 1. Pipeline

My pipeline consisted of 5 steps. First, I converted the images to grayscale, then I ....

* Converted image to grayscale 
    * Color information is not adding any value in edge detection for identifying line so gray scale would simplify 
    the computation.

![Grayscale][imageGray]
* Blurred the image with gaussian blur filter to remove small patches in image.
        

![Blurred image][imageBlur]
* Canny edge detection step to Identify the lines in the image
    * aperture of size 5 worked better.

![Canny edge][imageCanny]
* Cliped the image to only region of interest 
    * Triangle formed by bottom left, bottom right and middle of image with small y offset is chosen
    * Running clipping before canny edge detection would have been faster but that need to ignore the edge 
    formed by clipping triangle.

![Clipped][imageClipped]
* Hough-line transformation step to identify
    * tweaked the line length to large enough to capture only long running lines.
    * as lane lines are placed distant enough, 100 px is distance between lines.
    * votes for selecting line 30 turns out to be good with given images.

![Hough line][imageHough]    
* Selecting only two lines

![Final line][imageFinal]

### In order to draw a single line on the left and right lanes:
* First all lines were getting drawn which was segments for small lines.
* First calculated slope of all lines and based on the angle, i.e., + or - added ¬them into 2 pools and averaged x and ys
* also applied a filter to remove all lines out of expected angle range.




### 2. Potential shortcomings:

One potential shortcoming would be what would happen when large intersection or lane merge opens the lane line
 for longer distance.

Another shortcoming could be concrete road where color is gray compared to dark color in sample images.


### 3. Improvements:

A possible improvement would be to normalize the image to have brighter picture, in one of image where 
there was shadow color levels dropped significantly leaving edge detection failing.  

Another potential improvement could be to selecting color channel as lane lines would be either yellow or white, 
blue channel can be completely ignored. 
