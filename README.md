# **Finding Lane Lines on the Road** 
[![Udacity - Self-Driving Car NanoDegree](https://s3.amazonaws.com/udacity-sdc/github/shield-carnd.svg)](http://www.udacity.com/drive)

<img src="examples/laneLines_thirdPass.jpg" width="480" alt="Combined Image" />

Reflection
---

The pipeline:
  This project mainly just uses the helper function provided and builds a pipeline for both extrapolatation and without by passing a boolean argument. The pipeline is quite staright forward:
  a. convert to grayscale
  b. Gaussian blurring
  c. Canny edge detection
  d. Set a mask based on the camera mountaing (would be cool if we can do online calibration based on the result of this project and automatically generates a mask)
  e. Hough transformation (curve fitting or without)
  f. Combine with original image
  
  Two functions:
  1. process_image: Process the image and draw the Hough Transmation lines on the image
  2. process_image_fitting: Same processing but add curve fitting to extrapolate the lane markings by calling draw_lines_fitting

Drawbacks:
1. Spent a lot of time tuning the parameters: thresholds of Canny detector and Hough transform parameters. Maybe there is a way more efficient way to do so.
2. For every condition (poor lighting or raining), this algorithm may need a set of parameters respectively
3. For curving fitting, it requires more data, which could be replaced by Gaussian Process Regression
4. For the optical challenge, the result is terrible

Potential Improvements:
1. Find a more efficient way to tune the parameters (Use some opencv filters)
2. Given the fact that the lane markings are only painted in yellow or white, maybe find the great filter for lane marking dectetion purpose
3. Integrate with Gassian Process Regression to generate more meanningful extrapolated points with variance info.
