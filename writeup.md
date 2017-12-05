# **Finding Lane Lines on the Road** 

    ## David Lopez Rubio

### Udacity Car-ND project 1 writeup.

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

My pipeline follows this steps:

1) White filter of original image, helps identifying white paint marks on road
2) Yellow filter of original image after HSV conversion is applied, is usual to have yellow marks too, in Spain is usual to use when road is being subject to construction works
3) Both filters are fused, result image have only yellow and white elements
4) Image is converted to grayscale for easier manipulation
5) Then is softened with a blur gaussian filter to help with straight segments identification
6) Canny process is applied to detect all edges on the image
7) Region of interest mask removes the image outside the zone outside where the lanes are expected with the current car camera setup 
8) Hough transform is applied then line segments of a minimum of 50pix are detected and the points are used
9) Segments are classified by positive and negative slopes (left and right lane lines)
10) Lines are computed from segments using linear regression
11) Lanes lines are drawn on original images





![alt text][image1]




### 2. Identify potential shortcomings with your current pipeline


One potential shortcoming would be what would happen when lanes are curved 

Another shortcoming could be ...


### 3. Suggest possible improvements to your pipeline

A possible improvement would be to ...

Another potential improvement could be to ...
