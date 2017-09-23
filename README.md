# Vehicle Detection


## Michael DeFilippo

#### Please see my [project code](https://github.com/mikedef/CarND-Vehicle-Detection/blob/master/Vehicle_Detection.ipynb) for any questions regarding implementation.
---

**Vehicle Detection Project**
---

The goals / steps of this project are the following:

   - Perform a Histogram of Oriented Gradients (HOG) feature extraction on a labeled training set of images and train a classifier Linear SVM classifier
   - Optionally, you can also apply a color transform and append binned color features, as well as histograms of color, to your HOG feature vector.
   - Note: for those first two steps don't forget to normalize your features and randomize a selection for training and testing.
   - Implement a sliding-window technique and use your trained classifier to search for vehicles in images.
   - Run your pipeline on a video stream (start with the test_video.mp4 and later implement on full project_video.mp4) and create a heat map of recurring detections frame by frame to reject outliers and follow detected vehicles.
   - Estimate a bounding box for vehicles detected.

---

[//]: # (Image References)

[image1]: ./output_images/vehicles.png "vehicles"
[image2]: ./output_images/non-vehicles.png "non-vehicles"
[image3]: ./output_images/sobel_road_img_harder_sample.png "Sobel Example"
[image4]: ./output_images/mag_road_img_sample.png "Mag Example"
[image5]: ./output_images/dir_road_img_sample_kernel3.png "Dir Example"
[image6]: ./output_images/combined_road_img_sample_.png "Combined Example"
[image7]: ./output_images/combined_color_road_img_sample_.png "Combined with color Example"
[image8]: ./output_images/perspective_transform_road_img_sample_.png "perspective transform Example"
[image9]: ./output_images/histogram_road_img_sample_.png "Hist of lane line pixles"
[image10]: ./output_images/slidingWinddow.png "sliding Hist of lane line pixles"
[image11]: ./output_images/FittedLaneLines.png "slidings Hist of lane line pixles"
[image12]: ./output_images/curve_fitting_road_img_sample_.png "curve fitting"
[video14]: ./project_video_output.mp4 "Video"

## [Rubric](https://review.udacity.com/#!/rubrics/513/view) Points

### Here I will consider the rubric points individually and describe how I addressed each point in my implementation.  

---

### Exploring The Data

First I would like to explore the data sets given by udacity to train the classifier. The classifier will be used to identify vehicles on a road Vs non-vehicles. Below are a sample of the images provided.

![alt text][image1]
