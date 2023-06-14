# Bird classification using transfer learning 
Report final project for CSE 455 Computer Vision at University of Washington.
### Team members:
* Florian Kneip
* Yanick Schimpf

### Code and video:
* Code: See jupyter notebook in this repo: https://github.com/FloKnp/ComputerVisionFinal/blob/main/birdclassification.ipynb
* Video: https://youtu.be/iAuS4XP-v04
* Slide deck: https://docs.google.com/presentation/d/10-iDpTpoQIhPs98G61RVRzHN92VQ5iAcY9_zAM8vrVk/edit?usp=sharing
* Code explanation: https://youtu.be/aJz1cyLaCq8



## Problem Statement and Data Set
We decided to train a classifier that takes pictures of birds as inputs and outputs their class. The class, which initially is only a number can then be translated into the actual name of the respective bird's species. 
\
The dataset is given in the following structure:
* train set: There are 555 folders that represent the birds' classes. Each of these folders contains sample images of birds of that class.
* test set: In one folder there are all the images predictions are to be made on.

## Development outline
Note: Both of us were pretty new to neural networks especially using pytorch. In the later you will see why this fact is important to our projects outcome. 
\
In this paragraph we provide a rough outline on our progress. In the next paragraph we will dive deeper into the architecture of our final network.
\
The rough steps of the development of our network were the following:
* Create a working structure of the code that reads the data, trains a trivial network, and then predicts on the test set
* Write a more complex network in terms of layers and tune the parameters to achieve a good score
* Use transfer learning to extract features and then use a simple network on these features
* Select a good pretrained network
* Enhance the network that works on the extracted features of the pretrained network
* Add some data augmentation (only tried clashed with transforms of pretrained weights and hence resulted in poor results)

## Architecture of final submission
### Code structure
Our final submission is the result of the steps explained in the paragraph before. The structure of our notebook comes from the first step and can be summarized as follows: 
* Create datasets for both training and testing data
* Method definitions for training and testing
* Class definition of the model
* Train model, call it on the test data, and write the predictions to a csv which can be submitted

Be aware that in earlier steps we used test/validation splits on the train data in the end we then trained our model on the whole dataset.
### Network structure

![network](https://github.com/FloKnp/ComputerVisionFinal/assets/115632782/a08d5911-7a61-4b65-8e10-e33b0621da57)
\
As outlined before we started with a very simple network of multiple linear layers with some dropout and activation functions. However, we quickly recognized that even a lot of fine tuning wouldn't really bring some awesome results.
\
Hence we decided to use a more advanced approach: We used transfer learning. That is we use a pretrained network and pretrained weights on that network to extract features from the input images. This means that this network is freezed during training as we do not have the capacity to train a network that large. But that's the beauty of transfer learning: Often features extracted in a general setting are still useful for a more specialized use case with some extra work.
\
In our final network we use EfficientNetBO as such a pre trained network to extract features. The pretrained weights we use result from a training on general images in the IMAGENET1K_V1 dataset. Even though these are general images and not specifically birds, the features we get from a forward pass of an image through this network capture features extracted from the inputs which are images - but just of birds. On these features we now train our own network to perform the specific task we want to solve: Classify birds.
\
This network is composed of some linear layers, tanh activation functions, batch normalization layers, and some dropout.
\
To actually perform the classification or rather the training for it we selected the adam optimizer, a decaying learning rate scheduler, and the negative log likely loss for multiclass classification.

## Results & The bigger context & Ideas for further improvement
We achieved an accuracy between 55% - 60% on the test set.
\
What are our results worth in the bigger context? Well, we need to recognize that our performance is not the best. Even if you compare it with our classmates we are off by quite a margin. Still, we believe that the overall structure/idea of the code is not that bad. Maybe some more complex pre-trained network would have offered some better features. We could only find networks that were pretrained on general image datasets. Of course, if we would've found one pre-trained on birds or even just animals, the features would have very likely been even more useful than those obtained from general images. Also as our time schedule was disturbed by the issue that we didn't get our rough code structure to work (see next paragraph) for so long, more parameter fine tuning would have probably helped to increase performance. 


## Main issues
The main issue is that both of us were pretty new to programming with neural networks. We had one very big issue that took us several days to resolve and it is just a formal one, that is one you would expect beginners to encounter: 
\
When training the network it is trained on some indexes the datasets.ImageFolder() creates when loading the data. When trying to actually predict from this network you need to transform the indexes back to the labels. We were not aware that this is necessary as the indexes just looked like they were proper labels - they were in the range [0,554] as well. As you can see from our submission history we spend days desperately trying to figure out what was wrong with our network which even produced good results on a test/val split of the training data. This took so much time off our schedule that we didn't have a lot of time to actually fine tune the model to an extent we wished and planned to do in the beginning.
\
Overall getting familiar and setting up a skeleton to perform the task was maybe the biggest challenge for us.

## Other work used
As said both of us are rather new to neural network programming especially using pytorch. Hence the rough structure, which to our knowledge is roughly the same for most classification tasks, is inspired by other networks we found online that perform classification tasks on datasets that have similar form (in terms of folder structure for classes) as the one we had to deal with. However, once we had a rough sketch on how to structure the code, we wrote the code on our own. To conclude there is no single notebook that one could really say about that we started with it particularly - as just the structure is inspired by others we would say that our notebook is entirely our work as no significant findings of others were used.
