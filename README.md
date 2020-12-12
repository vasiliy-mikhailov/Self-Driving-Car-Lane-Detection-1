# **Finding Lane Lines on the Road** 

---

**Finding Lane Lines on the Road**

The goal of this project is to build pipeline that detects lane markings on the road.

Example input images

[image1]: ./test_images/solidWhiteCurve.jpg "Example 1"
[image2]: ./test_images/solidYellowCurve.jpg "Example 2"

Example output images

[image3]: ./test_images_output/solidWhiteCurve.jpg "Example 1"
[image4]: ./test_images_output/solidYellowCurve.jpg "Example 2"

---

## Pipline for images (LaneDetector class)

1. Convert image from RGB to Hue-Saturation-Value and use Value component gray channel.
2. Blur image
3. Clip region of interest
4. Select colors
5. Make Canny detection
6. Make Hough transform
7. Find out which line is left and which line is right by checking "m" sign in line equation y = mx + b
8. Find longest left line and longest right line
9. Find intersection point of left and right line

## Pipeline for videos (AveragerLaneDetector class)
Averager lane detector averages N last left and N last right lanes to produce smooth lines output.


## Pipeline for finding out best parameters for LaneDetector
I took all test images and every 25'th frame of every test video and marked left and right line by hands in "Supervise.ly" service and turned that data into train dataset.

I calculated good enough region of interest by putting all dots from train dataset on a plane and making quadrangle with 5% extent to all dots.

I calculated good enough parameters for blur, select colors, Canny and Hough by running Monte Carlo simulation for 1 million times which took 20 hours on my 4-core i5 running in parallel.

### Shortcomings of current pipeline

1. Different lighting conditions ruin the algorithm
2. Stabilization is still not very good on videos
3. Lane will not be detected if car turns because of two reasons:
3.1 Region of interest will clip out most image required to identify lane
3.2 When left lane or right lane will become vertical algorithm will not be able to see it as true left and true right line
4. Snow / dirt will ruin the algorithm
5. Orange and blue lines will ruin the algorithm 

### Possible improvements to pipeline

1. Identify left and right lane by inspecting "peaks" in Hough output and rotate image accordingly. It will help to overcome clipping problems and problems with distinquising left and right line.
2. Provide more training data
3. Use convolution neural networks to identify left and right lines



