# **Finding Lane Lines on the Road** 

## Writeup Template

### You can use this file as a template for your writeup if you want to submit it as a markdown file. But feel free to use some other method and submit a pdf if you prefer.

---

**Finding Lane Lines on the Road**

The goals / steps of this project are the following:
* Make a pipeline that finds lane lines on the road
* Reflect on your work in a written report


[//]: # (Image References)

[image1]: ./report_images/color.png "Starting color image"

[image2]: ./report_images/gray.png "Grayscale"

[image3]: ./report_images/edge.png "Edges"

[image4]: ./report_images/edge_mask.png "Edges with mask applied"

[image5]: ./report_images/overlaycolor.png "Hugh lines from the previously detected edges"

[image6]: ./report_images/hugh_lines_averageslopes.png "Hugh lines averaged lines re-drawn using average slope and average centers of left and right lane"


---

### Reflection

### 1. Describe your pipeline. As part of the description, explain how you modified the draw_lines() function.

My pipeline consisted of 5 steps. First, I converted the images to grayscale, then I applied a gaussian blur on the image. This helps with 
reducing some of the noise in the next step of edge detection using the Canny algorithm. Since we know the approximate location where the lanes are located in the 
image we apply a mask, this blocks the edges in the image that are not part of the lane edges and makes the lane detection easier. The next step is to use a hugh transform 
to detect line segments on the previously computer edges. The output of this draws many lines on the image

In order to draw a single line on the left and right lanes, I modified the draw_lines() function by first calculating the slope of each line. Based on the slop I grouped the lines in either left 
lane or right lane. For each group I then filtered out bad slopes that are too far off from the majority, computed the average slope, and calculated the average center of the line. Using this average slope and center for the left and right line I used the (y - y')=Slope*(x - x') to calculate what the correct lane lines in the videos should be. 

Bellow is an example of the lane detection pipeline. 

![alt text][image1]

![alt text][image2]

![alt text][image3]

![alt text][image4]

![alt text][image5]

![alt text][image6]

### 2. Identify potential shortcomings with your current pipeline


One shortcoming of the current implementation is that it only uses grayscale to detect the lane lines. This makes it much harder to distinguish between shadows, cracks in the road, and the true lane 
markers. 

Another shortcoming is in the way I filter out the slopes and calculate the center of the edges later.


### 3. Suggest possible improvements to your pipeline

A possible improvement would be to use the entire RGB data of the image and look for the white and yellow lanes in the image. Another potential improvement would be to also use other attitude sensors (IMU/Accelerometer) to better estimate where in the image the lane lines should be. 

Another potential improvement could be to ...
