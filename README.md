# :pushpin: Computer Vision tasks using Deep Learning

Exploring computer vision tasks like **foreground extraction, classification with circlization and semantic segmentation** using deep learning models. Tensorflow is used to form the CNN models and MNIST dataset is used and modified for each of these tasks. Jaccard similarity is used as test performance metric.

The following is performed on MNIST dataset to build the new datasets for the three tasks:
1. Obtain foreground segmentation masks for images in MNIST dataset using TSS-based
threshold. In this way, you have rough groundtruth masks required to
build a new foreground segmentation dataset.
Note: The pre-existing labels are of no use here. The goal of the dataset is just to extract
the foreground.
2. Obtain tight groundtruth circles around the foreground segmentation masks obtained in
(a). In this way, you can build a new dataset of 10 classes for performing classification
with circlization (circular localization). You can use existing libraries for generating the
tight circles.
3. Randomly concatenate 4 images and their corresponding groundtruths obtained in (a),
along with the pre-existing labels, in a 2x2 manner to develop new images and semantic
segmentation groundtruths, respectively. In this way, you have a new dataset of 10
classes for performing semantic segmentation.

## :technologist: Requirements

:package: Tensorflow

Dataset<br>
:package: keras (MNIST dataset)

Visualizations <br>
:package: matplotlib <br>
:package: cv2 <br>
:package: skimage

## :card_file_box: Files
* 'Report.pdf': Contains the complete report for the exercise.<br>
* 'datapreparation.ipynb' : Contains the code for data preparation/first question of the exercise.<br>
* 'ques2.ipynb' : Contains the code for foreground extraction/second question of the exercise.<br>
* 'ques3.ipynb' : Contains the code for classification using circlization/third question of the exercise.<br>
* 'ques4.ipynb' : Contains the code for semantic segmentation/fourth question of the exercise.<br>
* models created : Contains the trained saved models of this exercise
* images created : Contains the images of the visualizations and model architectures

## :monocle_face: Learnings

These findings are based on the experiments performed and may vary in different tasks.

* Foreground Extraction
	* Implemented a modified U-net model architecture and used binary cross entropy for the loss as it compares each of the predicted probabilities to actual class output which can be either 0 or 1.
	* After training the model, the model was tested on a test set of size 10000. The outputs were thresholded with value 0.5 to get a binary matrix and Jaccard similarity score of 0.9935.

* Classification using Circlizations
	* Implemented a deep learning model with convolution layers, few max pooling layers, average pooling layer (before branching out for results) and dense layers. The output is branched out in two ways. 
		* One predicts the label of the image (0-9).
		* Other branch works for regression and predicts a continuous value between 0 to 1 (as data regarding center and radius is normalised). The last layer of this branch uses ‘sigmoid’ for activation and is of size 3.
	* After training the model, the model was tested on a test set of size 10000. The masks were created in case of right predictions and the jaccard similarity score was 0.71.

* Semantic Segmentation
	* Implemented a modified U-net model architecture. I used binary cross entropy for the loss as it compares each of the predicted probabilities to actual class output which can be either 0 or 1.
	* After training the model, the model was tested on a test set of size 1000. The model gave  a 56 * 56 * 11 matrix for each image with values between 0 to 1. For a single cell, let’s say i,j in 56 * 56, the label was taken as 1 for which the value was maximum in the 11 channels/layers for the cell i,j. Using this binary masks of size 56 * 56 * 11 was created which were used for Jaccard similarity (0.97).


More detailed analysis can be found in the Report.pdf

## Acknowledgments
This exercise was a part of Computer Vision course.

:star: Have you found this repository helpful? Give it a star to show your support! :star:

