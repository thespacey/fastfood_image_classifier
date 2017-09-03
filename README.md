# fastfood_image_classifier
This is a TensorFlow Image Classifier to recognize if a given image is either a burger, a HotDog or a pizza

This is a detailed tutorial on how to build the TensorFlow Image Classifier that I created.

I used Google's Inception (2015) model. Inception is a deep convolutional neural network built for classifying real world images of a thousand categories.

# Repository structure
You can take a look at the training images in /dataset/fastfood/
You can use some images to test this model's prediction. 
# Requirements
* Docker
# Dropbox link to download the files for my fastfood image classifier
https://www.dropbox.com/sh/ktyikjplao38nbw/AADOJ_XxUZGFfkqDg3fLQ2jSa?dl=0
# Getting started / How-to build your own Image Classifier
1. Download and install Docker Toolbox
2. Open docker and install the TensorFlow Image by typing the following command: docker run -it gcr.io/tensorflow/tensorflow:latest-devel
3. Search and prepare different folders each containing a class of images you want to use (For example man/woman or car/boat/plane etc.)
4. Now back in you Docker create a destination file where you are going to move these files by typing: mkdir dataset
5. mkdir dataset/fastfood
6. cd dataset/fastfood/
7. Now you have to move the classes of images you have to this new directory you've created.
Example: mv D:/burger .
         mv D:/pizza .
         mv D:/hotdog .
   You can check if the files where moved by typing: ls dataset/fastfood/
8. Type: cd dataset and then: vi label_image.py to open a blank python file, type i to modify it and copy/paste the code from the corresponding file in my repository, click on 'esc' and type :wq and then click 'enter' to save the changes.(This script will be used to classify an image at the end)
9. Now cd to go back to the home directory
10. Type: docker run -it -v ~/dataset/:/dataset/ gcr.io/tensorflow/tensorflow:latest-devel (This step will link the Tensorflow image to your docker contained)
11. Download the training script by doing the following: cd /tensorflow and run: git pull (This will allow to retrain the inception classifier with the newely linked fastfood image dataset)
12. To retrain the model run the following:
    python tensorflow/examples/image_retraining/retrain.py \
    > --bottleneck_dir=/dataset/bottleneck \
    > --how_many_training_steps 500 \
    > --model_dir=/dataset/inception \
    > --output_graph=/dataset/retrained_graph.pb \
    > --output_labels=/dataset/retrained_labels.txt \
    > --image_dir /dataset/fastfood
13. To classify an image run: python /dataset/label_image.py /path/to/image    

# Example of result I got for classifying a new image
  > burger (score = 0.97235)
  
  > hotdog (score = 0.02228)
  
  > pizza (score = 0.00537)
  
  I provided the classifier with a new image of a burger that wasn't present in its training dataset and it correctly classified it as a burger with a score of 0.97235.
