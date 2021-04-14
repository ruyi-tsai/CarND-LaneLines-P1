# **Finding Lane Lines on the Road** 
[![Udacity - Self-Driving Car NanoDegree](https://s3.amazonaws.com/udacity-sdc/github/shield-carnd.svg)](http://www.udacity.com/drive)

<img src="examples/laneLines_thirdPass.jpg" width="480" alt="Combined Image" />

Overview
---

When we drive, we use our eyes to decide where to go.  The lines on the road that show us where the lanes are act as our constant reference for where to steer the vehicle.  Naturally, one of the first things we would like to do in developing a self-driving car is to automatically detect lane lines using an algorithm.

Pipeline
---
* Gray transform
* gussian smooth
* Canny edge detection
* Region of interest selection
* Line detection by Hough transformation


Gray transform
---
```python
cv2.cvtColor(img, cv2.COLOR_RGB2GRAY)
```
gussian smooth
---
The gussian smooth is help that image remove white noise to avoid detect error 
```python
cv2.GaussianBlur(img, (kernel_size, kernel_size), 0)
```
Canny edge detection
---
The Canny edge detector is an edge detection operator that uses a multi-stage algorithm to detect a wide range of edges in images. It was developed by John F. Canny in 1986.
From the OpenCV we call it with:
```python
cv2.Canny(img, low_threshold, high_threshold)
```
Region of interest selection
---
we are interested in what region is we want.
```python
imshape = image.shape
vertices = np.array([[(0,imshape[0]),(450, 330), (490, 300), (imshape[1],imshape[0])]], dtype=np.int32)
masked_edges = region_of_interest(edges,vertices)
```

Hough Transform Line Detection
---
The Hough transform takes a binary edge map (output of a Canny transform) as input and attempts to locate edges placed as straight lines.
```python
def hough_lines(img, rho, theta, threshold, min_line_len, max_line_gap):
    return cv2.HoughLinesP(img, rho, theta, threshold, np.array([]), minLineLength=min_line_len, maxLineGap=max_line_gap)
```


