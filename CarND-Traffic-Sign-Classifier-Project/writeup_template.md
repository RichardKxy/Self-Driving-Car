# **Traffic Sign Recognition** 

## Writeup

### You can use this file as a template for your writeup if you want to submit it as a markdown file, but feel free to use some other method and submit a pdf if you prefer.

---

**Build a Traffic Sign Recognition Project**

The goals / steps of this project are the following:
* Load the data set (see below for links to the project data set)
* Explore, summarize and visualize the data set
* Design, train and test a model architecture
* Use the model to make predictions on new images
* Analyze the softmax probabilities of the new images
* Summarize the results with a written report


[//]: # (Image References)

[image1]: ./my-output/Data_visualization.jpg "Visualization"
[image2]: ./my-output/Model.png "Model"
[image3]: ./my-test/00092.png "Traffic Sign 1"
[image4]: ./my-test/00108.png "Traffic Sign 2"
[image5]: ./my-test/00297.png "Traffic Sign 3"
[image6]: ./my-test/00154.png "Traffic Sign 4"
[image7]: ./my-test/00298.png "Traffic Sign 5"

## Rubric Points
### Here I will consider the [rubric points](https://review.udacity.com/#!/rubrics/481/view) individually and describe how I addressed each point in my implementation.  

---
### Writeup / README

#### 1. Provide a Writeup / README that includes all the rubric points and how you addressed each one. You can submit your writeup as markdown or pdf. You can use this template as a guide for writing the report. The submission includes the project code.

You're reading it! and here is a link to my [project code](https://github.com/udacity/CarND-Traffic-Sign-Classifier-Project/blob/master/Traffic_Sign_Classifier.ipynb)

### Data Set Summary & Exploration

#### 1. Provide a basic summary of the data set. In the code, the analysis should be done using python, numpy and/or pandas methods rather than hardcoding results manually.

I used the pandas library to calculate summary statistics of the traffic
signs data set:

* The size of training set is 34799
* The size of the validation set is 4410
* The size of test set is 12630
* The shape of a traffic sign image is [32, 32, 3]
* The number of unique classes/labels in the data set is 43

#### 2. Include an exploratory visualization of the dataset.

Here is an exploratory visualization of the data set. It is a bar chart showing how the data ...

![alt text][image1]

### Design and Test a Model Architecture

#### 1. Describe how you preprocessed the image data. What techniques were chosen and why did you choose these techniques? Consider including images showing the output of each preprocessing technique. Pre-processing refers to techniques such as converting to grayscale, normalization, etc. (OPTIONAL: As described in the "Stand Out Suggestions" part of the rubric, if you generated additional data for training, describe why you decided to generate additional data, how you generated the data, and provide example images of the additional data. Then describe the characteristics of the augmented training set like number of images in the set, number of images for each class, etc.)

As a first step, I decided to convert the images to grayscale with a simple method. Each pixel value is divided by 3 and then add the value at each point in R,G and B layers together.

As a last step, I normalized the image data with (pixel - 128)/ 128.

#### 2. Describe what your final model architecture looks like including model type, layers, layer sizes, connectivity, etc.) Consider including a diagram and/or table describing the final model.

![alt text][image2]

#### 3. Describe how you trained your model. The discussion can include the type of optimizer, the batch size, number of epochs and any hyperparameters such as learning rate.

To train the model, I used several below parameters：

mu = 0

sigma = 0.1

EPOCHS = 40

BATCH_SIZE = 120

rate = 0.001

#### 4. Describe the approach taken for finding a solution and getting the validation set accuracy to be at least 0.93. Include in the discussion the results on the training, validation and test sets and where in the code these were calculated. Your approach may have been an iterative process, in which case, outline the steps you took to get to the final solution and why you chose those steps. Perhaps your solution involved an already well known implementation or architecture. In this case, discuss why you think the architecture is suitable for the current problem.

My final model results were:
* training set accuracy of 1.000
* validation set accuracy of 0.967
* test set accuracy of 0.940

* I first chose to use Lenet5 to test. The accuracy is about 88%. It didn't satisfy the requirement of this project. Then based on what I have learnt, for example, max pooling, relu, dropout, etc., I began to modify the model.

* I added one more layer of convolution and used only one max pooling after three layers of convolution

* I used more EPOCHs. 10 EPOCHs only used not many training sets. I needed more training sets to train the model. Therefore, I changed it to 40 EPOCHs.

### Test a Model on New Images

#### 1. Choose five German traffic signs found on the web and provide them in the report. For each image, discuss what quality or qualities might be difficult to classify.

Here are five German traffic signs that I found on the web:

![alt text][image3] ![alt text][image4] ![alt text][image5] 
![alt text][image6] ![alt text][image7]

The reason that I chose them is that they have different shape, background and image.

#### 2. Discuss the model's predictions on these new traffic signs and compare the results to predicting on the test set. At a minimum, discuss what the predictions were, the accuracy on these new predictions, and compare the accuracy to the accuracy on the test set (OPTIONAL: Discuss the results in more detail as described in the "Stand Out Suggestions" part of the rubric).

Here are the results of the prediction:

| Image			        |     Prediction	        					| 
|:---------------------:|:---------------------------------------------:| 
| 50 km/h	      		| 50 km/h					 					| 
| Turn rigth ahead     	| Turn rigth ahead 								|
| Children crossing		| Children crossing								|
| No entry	      		| No entry						 				|
| Ahead only			| Ahead only	      							|


The model was able to correctly guess 5 of the 5 traffic signs, which gives an accuracy of 100%. 

#### 3. Describe how certain the model is when predicting on each of the five new images by looking at the softmax probabilities for each prediction. Provide the top 5 softmax probabilities for each image along with the sign type of each probability. (OPTIONAL: as described in the "Stand Out Suggestions" part of the rubric, visualizations can also be provided such as bar charts)

The code for making predictions on my final model is located in the 11th cell of the Ipython notebook.

For the first image, the model is relatively sure that this is a stop sign (probability of 0.6), and the image does contain a stop sign. The top five soft max probabilities were

| Image			        | Probability      					  |     Prediction	        								| 
|:---------------------:|:-----------------------------------:|:-------------------------------------------------------:| 
| 50 km/h	      		| 1.	6.2483925e-24	9.4525689e-26 | 50 km/h   			| 60 km/h			| Double curve	| 
| Turn rigth ahead     	| 9.99	6.1852875e-04	3.3425578e-05 | Turn rigth ahead	| 30 km/h			| Stop			|
| Children crossing		| 1.	9.5509330e-20	1.3031067e-23 | Children crossing	| Bicycles crossing	| Ahead only	|
| No entry	      		| 1.	8.1153774e-24	2.8276170e-34 | No entry			| Traffic signals	| Stop          |
| Ahead only			| 1.	2.0389628e-21	1.4550150e-28 | Ahead only     		| Turn left ahead	| No passing	|

### (Optional) Visualizing the Neural Network (See Step 4 of the Ipython notebook for more details)
#### 1. Discuss the visual output of your trained network's feature maps. What characteristics did the neural network use to make classifications?


