### ml-project-2-transcripted_cherry

ML4sciences project with the SUTER LAB about transcription factors!

[Overleaf report link](https://www.overleaf.com/project/6396e543351e79205bde5cb8)

# Setup for the code.
The code will need several packages to run each tasks and the colab notebook. The colab notebook already contains the lines required to install the packages not present un the basic colab environment, and also one specific package version required (scikit-image not updated to last version on the basic environment when we did the project).
The packages needed for tasks 1 and 2 are:
- [numpy](https://numpy.org/)
- [pandas](https://pandas.pydata.org/)
- [matplotlib](https://matplotlib.org/)
- [scipy](https://scipy.org/)
- [seaborn](https://seaborn.pydata.org/)
- [re](https://docs.python.org/3/library/re.html)
- [sklearn](https://scikit-learn.org/stable/)
- [skimage](https://scikit-image.org/)
- [warnings](https://docs.python.org/3/library/warnings.html)
- [math](https://docs.python.org/3/library/math.html)
- [cv2 from openCV](https://pypi.org/project/opencv-python/)

# Code organization:

## Feature processing
The feature processign is done using the google colab jupyter notebook, since we need the GPU to compute faster the nucleus segmentation. Inside it all the feature that are mentionned in the .pdf report we wrote. If used on colab it should be quite straight forward to adapt to anyone. The only part that one should take care of if the data importation from a google drive, that should be in the right folder, and adapt also the output folder name and end of file name to be coherent with what has been computed.
This file takes quite a long to run and has been the main issue that prevented us to run it for the 750+ TF's. Using standard GPU from google colab, it takes for one TF arround $1.5$ hours to run, using most of the time for the feature computation that are occuring over big images and so pixels.

## Data preprocessing (post feature calculation)
In order to give the most flexibility to anyone that would need to re use our codes and stuff, we did as little as possible preprocessing before the feature saving. Then when one will import these features in the Task_1.ipynb and Task_2.ipynb files, data preprocessing (pre-analysis) will need to be done. Since this one might be different between the two tasks, especially since a restrained number of features are used in the task 1, and globally the features are not used in the same way. The data preprocessing is then detailed below. Both globally contains possibility for __Outliers removal__, __Normalization__ and __log transformation__.

## Task 1

### Data preprocessing of task 1
This part is extensively described in the report that can be found on this github.

### Code
The code is mainly planned to run for a specific TF, which name (and file path) has to be defined at the top of the file. If it is used with a global feature file that contains the data for different TF at once, the expected behavior can be retrieved quite easily thanks to the column _TF_name_. Some parameters such as the $alpha$ grid (for ridge regression) and the $degrees$ grid that are tested can be also be found in a top cell that contains parameters. \
Then the code runs both linear regression and ridge regression with the grids defined above, and then select the best model according to the lowest error coming from the crossvalidation. The error used is the mean squarred error that the crossvalidation is trying to minimize in the test set.

## Task 2

Since the task 2 consisted mainly in unsupervised learning, it's first using PCA to reduce the dimensionality of the data (2 if one wants to visualize the results), and then KMEANS, aiming that multiple datapoints of a same TF will cluster together and show that 2 TF are indeed different. This is especially planned to be usefull to make some clusters of multiple TF, tring to pack some of them in one class. \
The normalization if also becoming more important since it will help to keep the PCA number reasonnable and not going to high or too low. This normalization is done according to each TF since most of the features (such as intensies) are not comparable between TF and might mainly come from technical issues/differences. \
One should then choose a good number of clusters according to the number of TF he is using, and what visualization looks like. 



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

