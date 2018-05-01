# **Finding Lane Lines on the Road** 
[![Udacity - Self-Driving Car NanoDegree](https://s3.amazonaws.com/udacity-sdc/github/shield-carnd.svg)](http://www.udacity.com/drive)

<img src="examples/laneLines_thirdPass.jpg" width="480" alt="Combined Image" />

Objective
---
To identify lane lines using canny edge detection and hough transform.

The Project
---
Step 1: Convert RGB image to grayscale.
Step 2: Apply Gaussian blur to reduce noise.
Step 3: Apply Edge detection using canny method in opencv.
Step 4: Select the region of interest making it easier to detect lines. 
Step 5: Detect lines using Hough transform.
Step 6 : Draw the lines by modifying the draw_lines method.
Step 7: Interlay the drawn lines over the original image.


Modification of draw_lines method:

The default version plots the lines detected using Hough transform. The method is modified so as to extrapolate to a single line representing the boundary of a lane.
By identifying that the left boundary lines have positive slope, and right boundary lines have negative slope, we can separate the lines identified after the Hough transform.
I used a threshold of slope values for left and right boundaries. (Between 0.2 and 0.8) for left and (-0.2 and -0.8) for right. This works for all of the test images.
I calculate the centre of x values and y values along with the slope and separate them into left and right lane boundaries based on slope values.
I calculate the average of the centers in x and y directions, and the average slope. This is used to extrapolate the lane lines.
Finally, I choose the y limits for the lane lines and then calculate the x intercepts based on the slope equation.
After obtaining the intercepts, we have the vertices required to draw the lane lines.

Shortcomings:
---
The current set of parameters for Hough Transform and extrapolation method fails in the challenge video. The problem is ?draw_lines? method encounters divide by zero errors when calculating the average slope values since it does not recognize any right lanes based on the thresholds. This means either the Hough transform does not recognize the right lane boundaries or the thresholds do not accept any right lanes. Further inspection is needed.

There might be fundamental problems due to the average values of slope taken to draw a single line. A solution can be to apply linear regression to the points separated by the slope thresholds.

Improvements Suggested
---
1) Increase value of min_line length and max_line_gap (Hough Transform parameters)
2) Perform weighted average of lane lines detected in previous 10 frames to reduce jitteriness of lines drawn.


