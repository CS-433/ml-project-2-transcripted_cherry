-Learn to work with google collab to get more computation power   __Done, it indeed goes much faster, but we might have some issues with big files__  

-Create function that matchs a feature (as a matrix ?) and the mask matrix to obtain feature for a particular nuclei
-Try to see if storing only matrices instead of images is saving any space

-In the end creating a pipeline for one small folder containing one TF and solving the first part

Task 1: Find relationship between nuclear size and expression level for each individual transcription factor
- get rid of blurred parts in the image (Tamara tries variance of laplacian filter) -> maybe done, discuss next time.
- polynomial feature expansion and cross validation (Tamara)
- maybe try also ridge regression
- Compare across different transcription factors
- Compare which feature (sum/mean/etc) would be best for the regression (maybe combination)
- Try with not only one image, does regression change (Alexis)

Task 2: 
- Classify different types of nuclear signal localisation 
- Find position of nuclear signal based on Y-Pet signal
- Find features for classifying: E.g. mean value, contrast, degree of colocalisation with DNA (Cherry signal) -> create M x N matrix where M = TF, N: features
    - Apply PCA to those features to extract the ones that vary the most
. Classify with unsupervised classification 
    - Clustering

. If we have time left: Classify with supervised classification (e.g. k nearest neighbour, decision trees such as random forest, logistic regression) -> we first have to   generate training data by classifying some nucleaus manually according to signal localisation (such as smooth, granular, stratied, with puncti, close to nuclear         membrane) 

