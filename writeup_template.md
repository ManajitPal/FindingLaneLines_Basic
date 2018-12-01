# **Finding Lane Lines on the Road** 

## Writeup

---

**Finding Lane Lines on the Road**

The goals / steps of this project are the following:
* Make a pipeline that finds lane lines on the road
* Reflect on the work in a written report

---

### Reflection

### 1. Describe your pipeline. As part of the description, explain how you modified the draw_lines() function.

My pipeline consisted of the following 7 steps, using the helper functions:

1. Selected colors through channel selection by giving priority to the red channel so that it can create a contrast between the yellow color and the rest of the image.

2. Converted the resultant image to grayscale

3. Added Gaussian blur to the image to smoothen the whites.

4. Applied Canny Edge detection to find all the edges in the image.

5. Masked the deried region of interest for our purpose, in this case, the lane.

6. Applied Hough Transform to the edges by tuning the parameters.

7. Interpolated the final result to the initial image to get the ouput of the test images and the videos.


In order to draw a single line on the left and right lanes, I modified the draw_lines() function by:

1. Creating an array for all the coordinates of the lines that were formed in the hough transform. 

2. Calculate the slope for each line and store the coordinates to the left lines, if the slope is less than 0, and to the right lines, otherwise.

3. Get the average coordinates of x1, y1, x2 and y2 by taking the sum and number of elements of the respective coordinate array.

4. Calculate the final x1, y1, x2 and y2 using appropriate parameters.

5. Finally draw a line using the above coordinates, for both left and right sides.


### 2. Identify potential shortcomings with your current pipeline


One potential shortcoming would be what would happen when a shadow or maybe too might light is casted on the road. Using the current RGB space, it was difficult to find the optimum values which would be able to detect the lane markings in both the conditions. Increasing the threshold value for the red channel and crushing other channels gave some clarity on light roads but worked poorly in case of dark roads, which required low value of the threshold for the red channel. The outcome can be seen in the challenge video.

I tried possible workarounds by drawing long lane lines to which would be able to detect white markings far off the road but that did not seem to work either.

Another shortcoming could be detecting curves. The current pipeline mainly focuses on drawing a straight line using average of points and extrapolation. However, in a real-world scenario, this pipeline would quickly mess up especially when the car encounters a curve.


### 3. Suggest possible improvements to your pipeline

As a person from a design background, I took a screenshot of the challenge video in Adobe Photoshop and fiddled around with some values. The only trick that would make the detection of lanes easier would be to play with the values of contrast in HSL space which would provide more control over the array for detecting yellow.
