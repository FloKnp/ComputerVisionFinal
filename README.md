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
* Select a good pretrained network (pretrained networks considered: EfficientNetB0 and Resnet50)
* Enhance and tune the network that works on the extracted features of the pretrained network
* Add some data augmentation

## Architecture of final submission
### Code structure
Our final submission is the result of the steps explained in the prargraph before. The struture of our notebook comes from the first step and can be summarized as follows: 
* Create datasets for both training and testing data
* Method definitions for training and testing
* Class definition of the model
* Train model, call it on the test data, and write the predictions to a csv which can be submitted

### Network structure
Be aware that in earlier steps we used test/validation splits on the train data in the end we then trained our model on the whole dataset.
INSERT IMAGE OF NETWORK
\
As outlined before we started with a very simple network of multiple linear layers with some dropout and activation functions. However, we quickly recognized that even a lot of fine tuning wouldn't really bring some awesome resutls.
\
Hence we decided to use a more advanced approach: We used transfer learning. That is we use a pretrained network and pretrained weights on that nework to extract features from the inoput images. This means that this network is freezed during training as we do not have the capacity to train a network that large. But that's the beauty of transfer learning: Often features extracted in a general setting are still useful for a more specialized usecase with some extra work.
\
In our final network we use EfficientNetBO as such a pretrained network to extract features. The pretrained weights we use result from a training on general images in the IMAGENET1K_V1 dataset. Even though these are general images and not specifically birds, the features we get from a forward pass of an image through this network capture features extracted from the inputs which are images - but just of birds. On these features we now train our own network to perform the specific task we want to solve: Classify birds.
\
This network is composed of some linear layers, tanh activation functions, batch normalization layers, and some dropout.
\
To actually perform the classification or rather the training for it we selected the adam optimizer, a decaying learning rate scheduler, and the negative log likely loss for multiclass classification.

## Resulsts & The bigger context & Ideas for further improvement
INSERT THE ACTUAL RESULTS

What are our resutls worth in the bigger context? Well we need to recognize that our performance is not the best even if you compare it with our classmates we are off by quite a margin. We believe that the overall structure of the code is not that bad. Maybe some more complex pretrained netowrk would have offered some better features. We could only find networks that were pretrained on general image datasets. Of course, if we would've found one pretrained on birds or even just animals maybe the features would have very likely been even more useful than those obtained from general images. Also as our time schedule was disturbed by the issue that we didn't get our rough code struture to work for so long way more parameter fine tuning would have probably helped to increase performance. 


## Main issues
The main issue is that both of us were pretty new to programming with neural networks. We had one very big issue that took us several days to resolve and it is just a formal one, that is one you would expect beginners to encounter: 
\
When training the network it is trained on some indexes the datasets.ImageFolder() creates when loading the data. When trying to actually predict from this network you need to transform the indexes back to the labels. We were not aware that this is necessary as the indexes just looked like they were prober labels. As you can see from our submission history we spend days desperately trying to figure out what was wrong with our network which even produced good results on a test/val split of the training data. This took so much time of our schedule that we didn't have a lot of time to actually fine tune the model to an extend we wished and planned to do in the beginning.
\
Overall getting familiar and seeting up a skeleton to perform the task was maybe the biggest challenge for us.

## Other work used
As said both of us are rather new to neural network programming especially using pytorch. Hence the rough structure, which to our knowledge is roughly the same for most classification tasks, is inspired by other networks we found online that perform classification tasks on data sets that have similar struture (in terms of folder structure for classes) as the one we had to deal with. However, once we had a rough sketch on the how to structure the code we wrote the code on our one. To conclude there is no single notebook that one could really say about that we started with that particular one and just made some of the adjustments.
