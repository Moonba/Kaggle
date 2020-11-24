# Introduction
This notebook is inspired from [Abhinand05](https://www.kaggle.com/abhinand05/histopathologic-cancer-detection-using-cnns)'s submission providing a solution to [Histopathologic Cancer Detection](https://www.kaggle.com/c/histopathologic-cancer-detection/overview) challenge on Kaggle. 

### Background:
In this problem, we have to create an algorithm to identify metastatic cancer in small image patches taken from larger digital pathology scans. 
The data for this competition is a slightly modified version of the [PatchCamelyon (PCam) benchmark dataset](https://github.com/basveeling/pcam). 
In the author's words:
>PCam packs the clinically-relevant task of metastasis detection into a straight-forward binary image classification task, akin to CIFAR-10 and MNIST. Models can easily be trained on a single GPU in a couple hours, and achieve competitive scores in the Camelyon16 tasks of tumor detection and WSI diagnosis. Furthermore, the balance between task-difficulty and tractability makes it a prime suspect for fundamental machine learning research on topics as active learning, model uncertainty and explainability.
 ![cancer](https://jithinjk.github.io/blog/images/histo/pcam.png)
### Data:

**The train data we have here contains 220,025 images and the test set contains 57,468 images.** 

Images name format: image_id.tiff  
The train_labels.csv file provides the ground truth for the images in the train folder.
As it's a binary classification problem, the desired submission format is | image_id | 0 or 1 |.

To run this notebook, please download the [input data](https://www.kaggle.com/c/histopathologic-cancer-detection/data)

 > You are predicting the labels for the images in the test folder. A positive label indicates that the center 32x32px region of a patch contains at least one pixel of tumor tissue. Tumor tissue in the outer region of the patch does not influence the label. This outer region is provided to enable fully-convolutional models that do not use zero-padding, to ensure consistent behavior when applied to a whole-slide image.
 
This from the competition's description means that the centers of the images are the ones that really matter.

### Evaluation Metric
The evaluation metric is the **Area Under ROC Curve** which is also called **AU-ROC/AOC Curve**.

AUC - ROC curve is a performance measurement for classification problem at various thresholds settings. ROC is a probability curve and AUC represents degree or measure of separability. **It tells how much model is capable of distinguishing between classes.** Higher the AUC, better the model is at predicting 0s as 0s and 1s as 1s. By analogy, higher the AUC (close to 1), better the model is at distinguishing between patients with disease and no disease. The curve is plotted with True Positive Rates Vs the False Positive Rates along the x and y axes respectively.


ROC                        |  AUC 
:-------------------------:|:-------------------------:
 ![ROC Curve](http://gim.unmc.edu/dxtests/roccomp.jpg)  |   ![AUC Curve](https://i.ibb.co/mBKh6ZB/roc.pnghttps://i.ibb.co/mBKh6ZB/roc.png)
