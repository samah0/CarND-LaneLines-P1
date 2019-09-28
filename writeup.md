# **Finding Lane Lines on the Road** 

---

**Finding Lane Lines on the Road**

The goals / steps of this project are the following:
* Make a pipeline that finds lane lines on the road
* Reflect on your work in a written report


[//]: # (Image References)

[image1]: ./test_images/solidWhiteRight.jpg "Input image"
[image2]: ./examples/processed_image.jpg "Processed image"


---

### Reflection

### 1. Describe your pipeline. As part of the description, explain how you modified the draw_lines() function.

My pipeline consisted of 6 steps. First, I perform color detection for white and yellow colors in the RGB color space and create a binary mask contains pixels that fall into the defined boundaries for white and yellow colors. After that, I apply "cv2.bitwise_and()" to keep only pixels in the image that have a corresponding value in the mask. Next, I convert the masked image to grayscale then I apply Canny edge detection to detect edges in the masked image. After detecting edges, a trapezoidal mask applied to the output image of previous step using "region_of_interest()" method to filter our all pixels outside region of interest. The output of this step is passed to "hough_lines()" method to detect lines in the masked image. 

In order to draw a single line on the left and right lanes, I modified the draw_lines() function by computing the slope of each line and using the slope's sign to determine if it belongs to the left  lane vs. right lane. My algorithm ignores vertical and horizontal lines. After separating line segments into two groups for left and right lanes then I fit a line for each group using numpy.polyfit() to find the best line that fits each group of points, then draw those lines on a mask and finally use  "weighted_img()" method to overlay the mask on the input image.


### Example input image
![alt text][image1]

### processed image
![alt text][image2]

### 2. Identify potential shortcomings with your current pipeline


One potential shortcoming would be what would happen when the weather is rainy. The proposed pipeline detects white and yellow colors in RGB space but it will be hard to detect colors in bad weather or under different illumination.

Another shortcoming could be, the current pipeline is fitting best line for each lane, but it would fail to detect lane lines if the road is curvy.


### 3. Suggest possible improvements to your pipeline

A possible improvement would be to use another color space like HSV or HSL to detect colors.

Another potential improvement could be to fit a polynomial of degree 2 or fit a line between each consecutive line segments to make the pipeline more robust and automatically adjust for straight or curvy road. 

### Resources

- Udacity/Introduction to Computer Vision Class.
- https://www.amazon.com/Programming-Computer-Vision-Python-algorithms/dp/1449316549/ref=sr_1_3?keywords=Programming+Computer+Vision+with+python+O%27reilly&qid=1569688868&sr=8-3
- https://www.pyimagesearch.com/2014/08/04/opencv-python-color-detection/

