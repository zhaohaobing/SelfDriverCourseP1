# **Finding Lane Lines on the Road** 

## Writeup Template
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

My pipeline consisted of 6 steps. 

1), I converted the images to grayscale.

2), I used gaussian smothing method to suppressing noise and spurious gradients by averaging. (kernel_size = 5)

3), I used canny to detect the edges. (low_threshold = 50, high_threshold = 150)

4), I setted vertices = np.array([[(0,imshape[0]),(460, 320), (490, 320), (imshape[1],imshape[0])]], dtype=np.int32), 

to mask the valid lane region.

5), I used hough transfer to get all the lines in the vertices region.

6), I used weighted_img to combine the line image and the source image.

In order to draw a single line on the left and right lanes, I modified the draw_lines() function by 3 steps.

1), check each line's slope, only keep the valid slope's line by these conditions:

    slope larger than -0.8 and smaller than -0.5, belong to left lane, also need x1 and x2 smaller than 
    
    the image's width/2.
    
    slope larger than 0.5 and smaller than 0.8, belong to right lane, also need x1 and x2 larger than
    
    the image's width/2.
    
2), calculate the left lane and right lane's avarage point and slope.

3), calculate the left and right lane's start and end point, then draw left and right lane


### 2. Identify potential shortcomings with your current pipeline


One potential shortcoming would be what would happen when canny method get some noise lines 

and these noise lines' slope and location is valid, It will cause the lane move to left or right.


### 3. Suggest possible improvements to your pipeline

A possible improvement would be to the avarage slope calculate is not so well, maybe 

I can use a line fitting algorithm (cv2.fitLine or numpy.polyfit) to get the left and right slope,

it should be more quickly and more accurity.

Another potential improvement could be to auto adjust some parameters and redo it

when I missed the left lane or the right lane.
