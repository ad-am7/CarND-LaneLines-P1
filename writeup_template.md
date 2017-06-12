# **Finding Lane Lines on the Road** 

## Writeup Template

### You can use this file as a template for your writeup if you want to submit it as a markdown file. But feel free to use some other method and submit a pdf if you prefer.

---

**Finding Lane Lines on the Road**

The goals / steps of this project are the following:
* Make a pipeline that finds lane lines on the road
* Reflect on your work in a written report


[//]: # (Image References)

[image1]: ./examples/grayscale.jpg "Grayscale"

---

### Reflection

### 1. Describe your pipeline. As part of the description, explain how you modified the draw_lines() function.

My pipeline consisted of 5 steps. First, I converted the images to grayscale, then I applied gaussian smoothing and canny edge detection to get the edges of the image. The image is then masked for the Region of Interest. A hough transformation is then undertaken to get the parameters of the lines. The lines are then group by left lines or right lines and a single line is approximated for each side 

In order to draw a single line on the left and right lanes, I modified the draw_lines() function by appending the lines to a list as either Left Lines or Right Lines (based on the slope of the line). A polyfit function is then used to average out all of the accepted lines. One approximation of the left or right lines is done by drawing a straight line between the uppermost point and the intercept of the line at the images height (img_height[0]) 



### 2. Identify potential shortcomings with your current pipeline


One potential shortcoming would be what would happen when the car changes lanes, or the car drives on a more aggressive bend in the road. This may not be identified by the pipeline in its current form.  

Further, The ROI masking accepts the region directly in front of the car. So any line marking, such as directional arrows in car parks, toll stations etc, may throw up odd results. 

Another shortcoming could be that the pipeline was not tested for differing light conditions.

A general shortcoming of the pipeline is that it is a process of filitering out unwanted results, but does not have a path to take if all the results are filtered out (it just doesnt display anything on the image). Depending on whether the hardware this code is controlling requires constants feedback or not, this may be an issue.


### 3. Suggest possible improvements to your pipeline

A possible improvement would be to have the region of interest change dynamically and also not include the region directly infront of the vehicle (ie where car parking directional arrows would be).

Another potential improvement could be to have the pipeline scan the image to estimate the overall light quality, and adjust the edge detection values to better match the overall picture.

The pipeline does not currently give any consideration to the result of the previous frame. In reality, the amount at which the left line and right line are limited. This would improve the consistancy of the results and also provide dummy lane lines if not lane lines are found in frame.
