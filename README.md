# ml-project-2-transcripted_cherry

ML4sciences project with the SUTER LAB about transcription factors!

# Code organization:

## Feature processing
The feature processign is done using the google colab jupyter notebook, since we need the GPU to compute faster the nucleus segmentation. Inside it all the feature that are mentionned in the .pdf report we wrote. If used on colab it should be quite straight forward to adapt to anyone. The only part that one should take care of if the data importation from a google drive, that should be in the right folder, and adapt also the output folder name and end of file name to be coherent with what has been computed.
This file takes quite a long to run and has been the main issue that prevented us to run it for the 750+ TF's. Using standard GPU from google colab, it takes for one TF arround $1.5$ hours to run, using most of the time for the feature computation that are occuring over big images and so pixels.

## Task 1

## Task 2




## Discussion point: 
We're not sure how the measurement was made. In order for our result to be true the measurement distance to the measurement plate has to stay constant-> size scale is constant over different images
## Discussion (shouldn't be here at the end)
- Nucleus might be overlayed
- We did normalize each image by the mean. 
- We could have normalized within each image, if this makes more sens for biologists. With this we assume that the mean across different pictures of same TF is the same. This is plausible since we have many nucleis in one image.
- We assume that expression level is fully measured by Ypet that is within the 'mask' of nucleus. Maybe it could also diffuce outwards
- Some cells might not be fully round -> the size we see is not equal to the actual size

## Further improvement
Check if model imrpoves by using other segmentation methods such as watershed 

