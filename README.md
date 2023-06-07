# ComputerVisionFinal

Report final project for CSE 455 Computer Vision at University of Washington.
\
Team members:
* Florian Kneip
* Yanick Schimpf

## Problem Statement and Data Set
We decided to train a classifier that takes pictures of birds as inputs and outputs their class. The class, which inititally is only a number can then be tranlsated into the actual name of the respective bird's species. 
\
The dataset is given in the following structure:
* train set: There are 555 folders that represent the birds' classes. Each of these folders contains sample images of birds of that class.
* test set: In one folder there are all the images predictions are to be made on.

## Development outline
Both of us were pretty new to neural networks especially using pytorch - we had basically just seen the network in the assignement before which is fairly simple compared to what we put together in this task. In the later you will see why this fact is important to our projects outcome. 
\
In this parapragraph we provide a rough outline on our progress in the next paragraph we will dive deeper into the architecture of our final network.
\
The rough steps of the development of our network were the following:
* Create a working structure of the code that reads the data trains a trivial network and then predicts on the test set
* Write a more complex network in terms of layers and tune the parameters to achieve a good score
* Use transfer learning to extraxt features and then use a simple network on these features
* Select a good pretrained network
* Enhance and tune the network that works on the extracted features of the pretrained network

## Architecture of final submission


## Resulsts & Results in the bigger context


## Main issues
The main issue is that both of us were pretty new to progrmming 

## Other work used
As said both of us are rather new to neural network programming especially using pytorch. Hence the rough structure, which to our knowledge is roughly the same for most classification tasks, is inspired by other networks we found online that perform classification tasks on data sets that have similar struture (in terms of folder structure for classes) as the one we had to deal with. However, once we had a rough sketch on the how to structure the code we wrote the code on our one. To conclude there is no single notebook that one could really say about that we started with that particular one and just made some of the adjustments.
