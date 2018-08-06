# Tree Detection Project
## Memory Error
The satellite images are too big to copy to GPU or to perform convolutions on. A typical type of an image is 100K * 100K * 4 pixel. One natural solution for this is to divide the image in a predefined number of tiles and train on small batches.
<img src="https://github.com/wesleytao/blog/blob/master/figs/figs/large.png" alt="img">

Our Solution:
1. divide into 512 * 512 * 3 tiles
2. set small batch size


## Unbalanced data
A typical problem in machine learning is unbalanced data. One class is much larger and our positive class is very small. In our case,we labeled the center area of the palm tree as 1, labeled other areas as 0.that means the majority of the mask images are 0, and only a few sample pixels are 1.
Our first attemp using FCN model achieve good error rate by classifying all data as negative.
<img src="https://github.com/wesleytao/blog/blob/master/figs/figs/imbalanced.png" alt="img">

Things to Try:

1.  Oversampling | Weight adjusting
2.  Cascade  | Thresholding
<img src="https://github.com/wesleytao/blog/blob/master/figs/figs/cascade.png" alt="img">
3. Use binary cross-entropy instead of global accuracy

Our Solution:
1. Switch models from FCN model to Unet Model.
2. Use Convolution to enlarge the area
>
img = cv2.GaussianBlur(img,(5,5),0)

>
np.where(img[:,:,:]>0,1,0)


## Boundary Issue
Because of zero-paddings procedure on the boundary, the performance on the edge of those tiles is not very good.


Things to try:
1. Conditional random field (CRF) A post-processing to generate better boundaries

Our Solution:
We used some overlap between tiles to counteract for loss in the convolutional layer and stitch them together.
