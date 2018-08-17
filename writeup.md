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

My pipeline consisted of 5 steps: 
1. dismiss everything that is not close to yellow and white as these are the colors of the lane markers
2. apply region masking to a suitable window (and encode suitable polygon vertices with respect to the image size.)
3. Now we should have reduced the image to the lane markers. Switch to grayscale.
4. Apply smoothing and canny
5. Apply hough transform

Suppose now we have a bunch of line parts for both lanes. In order to draw a single line on the left lane, we call function compute_lanes_from_lines which does the following:
1. split to left and right depending on the slope: if the slope is close to the median of the slopes of one side, then it belongs to said side (use median because of outliers)
2. Interpolate overall lane from the line pieces by applying np.polyfit on all pieces belonging to a side. Plot the resulting line from bottom to close to the middle of the image.

If you'd like to include images to show how the pipeline works, here is how to include an image: 

![alt text][1.png]
![alt text][2.png]
![alt text][3.png]
![alt text][4.png]
![alt text][5.png]
![alt text][6.png]


### 2. Identify potential shortcomings with your current pipeline


One potential shortcoming would be what would happen when the street color is not well distinguishable from the lane markers, like in the challenge task.

Another shortcoming could be when the lane marker color varies too much: Since I filtered out the colors yellow and white it might be the case that some sorts of those colors will also be filtered out.


### 3. Suggest possible improvements to your pipeline

A possible improvement would be to take into account the surrounding landscape, or vehicles driving next to me. Especially the safety fence on the side can be helpful, as it is always parallel to my lane.

Another potential improvement could be to use machine learning techniques to automatically learn which lane marker colors have to be filtered out depending on the color of the street or the illumination.
