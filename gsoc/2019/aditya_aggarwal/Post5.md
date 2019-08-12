# Experimenting with the Model and Error Handling

12th August, 2019

So after completing the first draft of the basic working component, I worked on the parameter tuning and  Error Checking. Parameter tuning plays a very important role as it helps not to overfit the model and perform equally well on the unseen data which is the crux of the Face Recognition.

## Parameter Tuning 

Since the model returns a 512 dimensional vector for each image, thus a distance metric (given by L2 distance) is used for the multi class classification. This requires a threshold parameter which helps to identify if given images in database are potential class labels for the given test image (By comparing the distance metric). So in order to find this threshold I performed a Random Search on the threshold on the LFW dataset and verified the accuracy for a smaller set of real images. The same process is also repeated for another distance metric given by the dot product.

## Removing Reduntant Data

Imbalanced data can create a bias in the dataset, thus not able to effectively predict the known people. Hence it is very important to ensure that each person has similar number of images. This also helps to store a lesser number of neural embeddings, saving space and computation time. Thus neural embeddings which belong to the same class and are very similar(measured in terms of L2 distance) are ignored and only the prior one is stored. Thus a threshold on the distance metric is required to find such cases. This threshold was found empirically for a small dataset of real images.

### Error Handling for the new images
While adding new images, in order to ensure that the person's image does not belong to multi classes, an error checking is performed. In this case whenever a new image is added, its neural embedding is compared with the complete dataset. If there is a match and the facelabels are not same then, the embedding is not stored. Threshold for this case is also calculated empirically for the small dataset of real images.


Now the first 100% functioning **People Identification Component** is complete which serves the required two purposes of identifying known people and able to dynamically add labels whenever required without training the model. 
* * *
Aditya Aggarwal
