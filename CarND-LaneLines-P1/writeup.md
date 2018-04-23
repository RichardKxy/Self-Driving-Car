# **Finding Lane Lines on the Road** 

## Writeup Template

### You can use this file as a template for your writeup if you want to submit it as a markdown file. But feel free to use some other method and submit a pdf if you prefer.

---

**Finding Lane Lines on the Road**

The goals / steps of this project are the following:
* Make a pipeline that finds lane lines on the road
* Reflect on your work in a written report


[//]: # (Image References)

[image1]: ./performance/original.jpg "Original"
[image2]: ./performance/lanelines.jpg "Gray"
[image3]: ./performance/region.jpg "Region"
[image4]: ./performance/output.jpg "Output"

---

### Reflection

### 1. Describe your pipeline. As part of the description, explain how you modified the draw_lines() function.

My pipeline consisted of 5 steps.

![alt text][image1]

First, I converted the images from RGB to HSV. I didn't use grayscale, because it didn't work well in optional challenge. The shadow of trees caused many contours that have a strong influence on grayscale.

![alt text][image2]

Second, I separately found yellow and white color with cv2.inRange(hsv,lower,upper). Then I merge them together with cv2.addWeighted(mask_w, 1., mask_y, 1., 0.) named "img".

Third, I use GaussianBlur to filter noise in "img".

Forth, I use Canny to find gradient change in "img". And set ROI to this contour image.

![alt text][image3]

Fifth, I use Hough Transform to find lines and drawed them in original image.

![alt text][image4]

In order to draw a single line on the left and right lanes, I modified the draw_lines() function by setting rational ranges of slope and position. 

1. left lanes have negative slopes and at the left part of the image. Symmetrically, right lanes have positive slopes and at the right part of the image.

2. Calculate the total length of left lanes and right lanes. Then according to their precentage of length, calculate the final slope of each lane.

3. Sort the list of left lanes and right lanes. Take left lanes as an example. Find the longest line as a reference. Then sort left lanes again to find upmost point, which could connect itself with reference line in left final slope.

If you'd like to include images to show how the pipeline works, here is how to include an image: 


### 2. Identify potential shortcomings with your current pipeline

One shortcoming should be this algorithm will only work when car moves along the road. If it tries to change lanes, the range of slope and position will make the pipeline work badly. If I didn't apply my pipeline on challenge, I didn't add limitation of position. For increasing the performance in challenge video, I believe left and right lane lines are divided from verical center line.

One potential shortcoming would be that the red lane line mark would be very short even absent if there exists the shadow of trees or strong sunlight.

Another shortcoming could be if one part of road doesn't have lane line  about one second or the lane lines is too short, it won't draw the line.

Another shortcoming could be uneven road will cause much distrubance, which sometimes makes the lane lines deviate from the real lane line.

### 3. Suggest possible improvements to your pipeline

A possible improvement would be to weaken the influence of specific factor, such as the shadow and sunlight, to increase the strength of features that we are interested in.

Another potential improvement could be to record previous lane lines and draw it in next frame instead of real lane lines if the absence or shortness is limited in a small range.

Another potential improvement could be smooth the image based on the relative position of camera and road.
