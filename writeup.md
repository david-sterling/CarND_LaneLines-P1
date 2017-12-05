# **Finding Lane Lines on the Road** 

    ## David Lopez Rubio

### Udacity Car-ND project 1 writeup.

---

**Finding Lane Lines on the Road**

The goals / steps of this project are the following:
* Make a pipeline that finds lane lines on the road
* Reflect on your work in a written report


[//]: # (Image References)



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

[image1]: ./demo_images/demo0.jpg "White filter"
[image2]: ./demo_images/demo1.jpg "Yellow filter"
[image3]: ./demo_images/demo2.jpg "White and yellow bitwise and"
[image4]: ./demo_images/demo3.jpg "Gaussian processing"
[image5]: ./demo_images/demo4.jpg "Canny edges filter"
[image6]: ./demo_images/demo5.jpg "Lines computed with linear regression"
[image7]: ./demo_images/demo6.jpg "Lane lines over original image"



![alt text][image1]
![alt text][image2]
![alt text][image3]
![alt text][image4]
![alt text][image5]
![alt text][image6]
![alt text][image7]

I have detected positive and negative slopes on the segments the hough lines straight lines detection function. After getting a group of positive and negative sloped segments, I adjust a straight line with fitline function from opencv using DIST_FAIR technique. I used a fixed height for the lines, but you could calculate a interception point and adjust height to that value. Lines are being drawn with "point slope" equations the fitline function gives.


### 2. Identify potential shortcomings with your current pipeline


One potential shortcoming would be what would happen when lanes are curved 

Another shortcoming could be the lines are adjusted without "memory", so the change on slope sometimes is so abrupt and sometimes a line is almost horizontal when white/yellow cars and signals pass throught the filter and are mistakenly detected as lines. 


### 3. Suggest possible improvements to your pipeline

A possible improvement would be to have memory and stablish a maximum slope change from last photogram to improve smoothiness.

Another potential improvement could be to better adjust the filters to improve behaviour when contrast conditions or light are worse.
