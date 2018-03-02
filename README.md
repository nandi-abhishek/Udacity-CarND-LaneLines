# **Finding Lane Lines on the Road** 

## Writeup 

### Reflection

### 1. Describe your pipeline. As part of the description, explain how you modified the draw_lines() function.

My pipeline function called 'find_lanes' consisted of 6 steps. 
    1. First, I converted the images to grayscale. 
    2. Then I apply Gaussian smoothing.
    3. Then on the gray image I applied Canny's edge detection algorithm. 
    4. Then I create a four sided polygon to mask and apply on the selected edge image to get masked edge image
    5. After that I run Hough transformation on the edge detected image
    6. At last I draw the lines from Hough transformation to the original image

In order to draw a single line on the left and right lanes, I modified the draw_lines() function using the slope of the lines:
    a. Any negative slope means left lane and positive slope means right lane
    b. I also remove any line that is close of horizontal. I used threshold slope of 0.5
    c. Then in the set of left and right lines I apply numpy.linalg.lstsq to get least square solution and find a 'm' and 'c'
    d. Using this m and c I extend the line from bottom of the image to least 'y' value of my region_of_interest


### 2. Identify potential shortcomings with your current pipeline


1. One potential shortcoming would be what would happen when we come to a curve. Then this pipeline will not give proper result 
2. I have a feeling that may be runtime could be an issue

### 3. Suggest possible improvements to your pipeline

1. May be we need to update our region of intersect to make it proper for curves also.
Make the slope of the intersecting lines of the region of intersect as a function of previous image's 'm' calculated in draw_lines function
As we approach a curve the 'm' should change in draw_line then for next image we should update region of intersect based on it.

2. We may try applying ML tecniques to improve runtime.

