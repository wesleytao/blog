# Palm Tree detection and Counting for High Resolution Satellite Images
## About
In agriculture, palm tree cultivation is one of the big sectors with a huge market value. Palm trees are used to produce a variety of products like vegetable oil, bio-fuel, papers, furniture, decorations,
fodder for cattle etc. It also has to be mentioned that palm oil is the most widely used vegetable oil in the world.  
It is necessary to plan well during cultivation and to monitor different aspects of trees like proper inventory, health, size, heights etc., at different stages of their life.  
As palm tree cultivation zones are huge and difficult to be monitored visually on ground, images analysis can play a vital role in delivering those data and analysis, cost and labor efficiently from the satellite or aerial images.

![myimg](figs/sat.png)



## Project Objective
This project investigates on one aspect, more specifically **localizing and counting palm trees** for creating their inventory, as an initial step towards the multifaceted monitoring.

![myimg](figs/intro.jpg)


## Dataset and Processing
High-resolution satellite images are usually very large and have more than three channels. A typical one has 20000 * 20000 pixels and four channel. In most cases, it has an irregular shape, and edges are padded with white background.
Sometimes, we need to do basic image processing like resizing, rotation, smoothing, readjusting label values and so on.

Our training dataset has pixel-level labeled mask. It will provide more information than the bounding box convention. Masks are hand labeled by the full-time analysts with professional image labeling tools.

Then our deep-learning model has achieved best human-eye accuracy.
All of these data are **the property of the company of Adatos and they are not included in this repository.**

We first use a small subset of images for experiment and then later we apply the model for big image.

* Stage 1
  * Train data set:  4 channel, resolution 1341*2048 , 4 mask has difference size.
    * orthogonal.tif
    * orthogonal_mask0.tif
    * orthogonal_mask1.tif
    * orthogonal_mask2.tif
    * orthogonal_mask3.tif

  * Test data set: we cut images into pieces and sample some images as test data.
  {# Test} / {# Train}  = 10-20%

* Stage 2
  * Train data set: 3 channel
    * KILE_sample.tif  (2560*2560)
    * KILE_sample_mask.tif (2560*2560)

  * Test data set:
    * gab_SIR_bawah.jpg (24051*15908)
    * KILE.tif (18500*16976)

## Methods
### **Blob Detection**

The objective of blob detection is quite straightforward, to detect groups of connected pixels in a binary image. This method is naturally suitable for tree localization because palm trees share a similar shape.

There are three types of blob detection:
 * Simple Blob Detection
    This algorithm is simply to find the connected pixels with a threshold filter.

 * Laplacian of Gaussian Blob Detection
   This method is the most accurate and slowest approach for detecting local maxima.  It uses laplacian gaussian filter as an interesting point detector.

 * Difference of Gaussian Approach
 This is a faster approximation for laplacian gaussian filter. In practice, this method is more frequently used in many mature applications.

One of the advantages of blob Detection is that it doesn't require label data which in a sense is suitable for a small project with budget and time constraint.  This method is quite handy with a small data set.

However, the major problem for blob detection its scalability.  For a much larger picture,  the shape of palm trees varies by tree maturity, illumination conditions, surrounding plantation. It might work pretty well for a small well-separated regular grid plantation region but not good for closely-clustered mature trees in a much darker background.
The parameters have to be fine-tuned for versatile conditions. The calibration process is a pain in the neck, and we need manually check result picture by picture.  To make matters worse, blob detection is inherent computationally expensive and require a lot of time for running.

>images have to be divided into small pieces and parameter has to be fine tuned depend on different situation.
![myimg](figs/blob.png)




### **Convolution Neural Network**

There are some researchers try to implement deep learning models to do this job. The highlight of their works is to hand label the center of the palm tree and then use a sliding window to get many batches of paired training data. After preprocessing and training, the convolutional neural network will produce a confidence map for the locations of the center of a palm tree given a new image. In the end, they use local maxima suppression to narrow down the targets.

This is a nice approach, but this is way too much computationally expensive. There is a lot of waste because many overlap images share some information and during the training process, weights are not shared. The sliding window approach is now deprecated by the deep-learning community.  

![myimg](figs/CNN.png)



### **Fully-Connected Neural Network**
The Fully-Connected Neural Network differs from CNN only by the connectivity at the last few layers. A nodes that are fully connected with every node in the next layer. This algorithm is the deep-learning benchmark for image segmentation task.
![myimg](figs/FCN-Lnet.png)

We have tried this method, and it turns out not to be the best solution. There some problems with this method. First, the number of parameters to be trained increase in the order of magnitude. Second, because of increasing parameters, this is also prone to imbalanced data pitfall. In other words, the model will predict all the pixel with the dominant class in the training dataset.


### **U-Net Image Segmentation**

<a herf ="https://arxiv.org/pdf/1505.04597.pdf">U-net </a>is a new architecture proposed in 2017.  The winning solution for 2018 kaggle data science bowl. It is widely used in medical image segmentation.  We implemented this method and get satisfactory results.
![myimg](figs/u-net-architecture.png)

* some advantages of Unet:
Satisfactory accuracy with proper training, enough dataset(hundreds of pics) and training time;
This architecture  does not contain fully connected layers which makes it very scalable to train;
Less parameter also leads to smaller model weight size (we use 256*256 ,and model size is less than 30mb);
we can also use it to train multiple class.

## Evaluation and Results
out-of-sample prediction
* stage 1

![origin](figs/stage1/stage1.png)
![label](figs/stage1/stage1_label.png)
![pred](figs/stage1/stage1_pred.png)

* stage 2
![pred](figs/large.png)
![pred](figs/zoom in.png)

![pred](figs/unet_post_process.png)

* loss Function
  For a classification problem, binary cross entropy prefer neat and cleaner solution than mean squared error. We have tried both at stage one and found binary cross entropy is slightly better than mse.

* metrics
  * accuracy:
  This is straightforward and easy to understand. However, accuracy is not a right metrics, especially for classification problem. Two type of error, False positive and false negative are ignored and imbalanced data problem is also hidden in misleading high accuracy.

  * Roc curve:
   We plot the ROC curve for stage one. We could compare different models based on the pixel-level correctness. The larger area under the curve, the better the model.
  ![label](figs/ROC.png)

  * IoU(Intercept over Union):   
  Intersection over Union is an evaluation metric used to measure the accuracy of an object detector on a particular dataset. We often see this evaluation metric used in object detection challenges such as the popular.
  There are usually good metrics with bounding boxs. In object detection task, mean IoU is a good metrics for localization and object detection.
 ![label](figs/iou_equation.png)

## Improvement and limitations
Deep learning model or in a broad sense, machine learning model heavily depends on the quality and quantity of the training data. Larger amounts of data with high quality label will no doubt increase the overall perfromance.


## Data pipeline and Automation

```
deepunet
 ├── basics.py
 │   ├── reshape
 │   └── resize
 ├── engine.py
 │   └── train
 ├── model.py
 |   └── UnetModel
 |
 └── imagetool.py
         ├── Image
         ├── ImageGrid
         ├── YImage
         └── XImage
 ```

## Reference and Resources
<a href = "https://arxiv.org/pdf/1505.04597.pdf" > 1. Barkau, Robert L. UNET: One-dimensional unsteady flow through a full network of open channels. User's manual. No. HEC-CPD-66. Hydrologic Engineering Center Davis CA, 1996.</a>

<a href ="https://www.cv-foundation.org/openaccess/content_cvpr_2015/papers/Long_Fully_Convolutional_Networks_2015_CVPR_paper.pdf">2.
 Long, Jonathan, Evan Shelhamer, and Trevor Darrell. "Fully convolutional networks for semantic segmentation." Proceedings of the IEEE conference on computer vision and pattern recognition. 2015.</a>

 <a href ="https://arxiv.org/ftp/arxiv/papers/1701/1701.06462.pdf">3.Cheang, Eu Koon, Teik Koon Cheang, and Yong Haur Tay. "Using Convolutional Neural Networks to Count Palm Trees in Satellite Images." arXiv preprint arXiv:1701.06462 (2017).
 </a>

This project is led by Chief Data Scientist Cui Han at Atados.ai https://www.adatos.com/product
