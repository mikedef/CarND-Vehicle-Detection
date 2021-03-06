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
[image2]: ./output_images/non_vehicles.png "non-vehicles"
[image3]: ./output_images/hog_examples.png "HOG Example"
[image4]: ./output_images/color_hist.png "color hist"
[image5]: ./output_images/spatial_bin.png "spatial binning"
[image6]: ./output_images/search_windows_separate.png "sliding window search"
[image7]: ./output_images/located_cars.png "located cars"
[image8]: ./output_images/vehicle_final_efficient.png "finding vehicles"
[image9]: ./output_images/heatmap.png "heat map"

[video14]: ./project_video_output.mp4 "Video"
[video15]: ./project_video_gif.mp4 "Video"

## [Rubric](https://review.udacity.com/#!/rubrics/513/view) Points

### Here I will consider the rubric points individually and describe how I addressed each point in my implementation.  

---

### Exploring The Data

First I would like to explore the data sets given by udacity to train the classifier. The classifier will be used to identify vehicles on a road Vs non-vehicles. Below are a sample of the images provided.

![alt text][image1]
![alt text][image2]

The images extracted show that in the vehicles folder there are images of vehicles of various angles, crops, and zooms. In the non-vehicle folder we have images of typical scenes that you might see driving without any other vehicles around. I will use these images to train the classifier.

### Extracting Image Features 
### Histogram of Gradients (HOG)

To extract the HOG features I defined a function  `get_hog_features()` which implements `scikit-image` and the function to extract HOG features as shown below. The HOG function has selectable parameters such as orientation, pixels per cell, and cells per block. Through experimentations I found that the LUV color space was the best color space parameter to extract features. Based on the lesson I selected 8 pixels per cell and 8 orientations.

![alt text][image3]

It is easy to see the difference between the Vehicle HOG images and the Non-Vehicle HOG images

### Color Features

Next I will extract features based on different color cars looking at each color spaces. The sample below looks at RGB color space, but I decided on using the LUV color space based on the performance of the classifier.

![alt text][image4]

### Spatial Binning

Next I will look at how reducing the resolution will affect how well I can detect features. 


![alt text][image5]

This reduces the images resolution but we can still make out the vehicle enough to capture valid information

## Classifying Images

Next I will build a classifier to tell if a image is a vehicle or not. I ended up using a Random Forest model using a grid search that returned 99.35% accuracy on the test set. 

### Sliding Window Search

A sliding window approach has been implemented, where overlapping tiles in each test image are classified as vehicle or non-vehicle. The sliding window search shows different scale windows used to identify vehicles at various distances away from the camera. 

![alt text][image6]

The searching the windows above the classifier is able to identify the windows where a potential vehicle is located. 

![alt text][image7]

Implementing the HOG extraction over all new windows is very inefficient and takes a long time to do. Using the HOG extraction function over the sliding window improves the efficiency and helps separate detections.

![alt text][image8]

### Heat Maps

Next I use a heatmap to reduce false positives and control for noise in the images and use a bounding box to identify each vehicle.

![alt text][image9]

### Video Pipeline
I have added more images from the udacity dataset to help with training a better classifier for this pipeline.

Here's a [link to my updated video result](https://youtu.be/cv8-oMW0zdY)


or see the project_video_output.mp4 or project_video_gif.mp4 in this repository. 
or see the project_video_output3.mp4 for an updated vehicle detection video. 

![Alt Text](project_video_gif.mp4)

### Discussion

Using this pipeline on a live video is extremely inefficient. It takes well over 30 minutes to extract and identify vehicles. Also my pipeline seems to have a problem pickin the white vehicle back up after the road changes color. This would simply not work in real life. Maybe training a neural network would help reduce how the time that this pipeline takes to identify vehicles to something that is real-time. 


