### ml-project-2-transcripted_cherry

ML4sciences project with the UPSUTER LAB about transcription factors!

# Setup for the code.
The code will need several packages to run each tasks and the colab notebook. The colab notebook already contains the lines required to install the packages not present un the basic colab environment, and also one specific package version required (scikit-image not updated to last version on the basic environment when we did the project).
The packages needed for tasks 1 and 2 are:
- [numpy](https://numpy.org/) (1.23.4)
- [pandas](https://pandas.pydata.org/) (1.5.2)
- [matplotlib](https://matplotlib.org/) (3.6.2)
- [scipy](https://scipy.org/) (1.9.3)
- [seaborn](https://seaborn.pydata.org/) (0.12.1)
- [re](https://docs.python.org/3/library/re.html)
- [sklearn](https://scikit-learn.org/stable/) (1.1.3)
- [skimage](https://scikit-image.org/) (0.19.3)
- [math](https://docs.python.org/3/library/math.html)
- [cv2 from openCV](https://pypi.org/project/opencv-python/) (4.6.0)

# Github organization

Based on an image with cell expressing H2B-mCherry (mCherry = red fluorescent protein) and an image in which a given transcription factor fused to Ypet (= yellow fluorescent protein) is expressed a pipeline is provided to generate features for each nucleus detected in the images as well as for two different tasks. One task giving a pipeline for a regression between nuclear size and an expression level and the second task for classifying the different nuclei according to their subnuclear localization as well as their associating with the DNA (computed by the co-localization with H2B-mCherry).
The github page is organized in four folders:
-	Jupyter notebooks: contains two files: Task_1.ipynb, Task_2.ipynb. The notebooks are further explained in the next chapter.
-	Collab_Notebooks: contains one file that can be run in google collab as well as locally. 
-	Images: Contains plots produced in different Jupyter_notebook files. If `Save = True`, images are saved in this folder when running the program. Images are either at the format .png or .pdf.
-	Features: Contains all the features generated for this project in .csv files.  

# Jupyter Notebooks organization:
## Feature generation
Feature generation is the first step and ran on TexasRed-channel images representing cell line and the corresponding Ypet-channel images. The code is provided as a Jupiter notebook file that should be run on google colab, but can be run locally as well.

There are two possibilities on how and which files should be imported. The two possibilities are:
-	Deciding manually which transcription factor should be analysed.
-	Analysing the content of a whole folder
Choosing the mode can be done by following the instructions of the program. 

The generated features as well as their meaning can be taken from the report. For further use there can also be taken other or more features into account.
The calculation of one transcription factor of 12 pictures(usually $1$ whole TF) takes around 1.5 hours to run using standard GPU from google Collab. 

## Preprocessing:
There is an individual preprocessing step in both files Task_1.ipynb and Task_2.ipynb. This allows an optimization of the preprocessing parameters for each task. 
Note: If there are many columns for which outlier removal should be applied to, a lot of datapoints are filtered out because not all outliers occur in the same feature.

During the preprocessing step outlier removal,  log transformation, z-score normalization as well as a step to get rid of bad detected or blurred values can be used. For each possible step the feature-columns that undergo this transformation have to be specified.
### Outlier removal
The `outlier_removal` function removes outliers from a dataframe based on the specified parameters. It can either remove outliers depending on the interquartile range or based on a specific quantile.
### Z-score normalization
The `normalization` function uses Z-score normalization in specified columns of a dataframe. 
### Log-Transformation
The `log-Transformation` takes the logarithm in the specified columns of a dataframe, which can reduce the skewness. 
### Filtering bad detected nuclei
The filtering contains a removal step for rows based on blurness as well as on similarity. 



### Parameters to adapt:
#### Outlier removal:
-	`outlier`: a boolean value indicating whether outliers should be removed (True) or not (False).
-	`interquantile`: a boolean value indicating whether outliers should be removed based on the interquantile range (True) or based on a specific quantile (False).
-	`quantile_keep`: a value between 0 and 1. Is only applied if `interquantile` is False. Specifies the quantile up to which values should be kept, e.g. 0.85: 85% of smallest points are kept.
-	`outlier_range`: only considered if `interquantile` is True. This value is used to define the range for outlier removal. It is multiplied with the interquantile range.
- `outlier_columns`: a list of column names in which outliers should be removed.
#### Normalization:
-	`normalization`: a boolean value indicating whether the data should be normalized (True) or not (False).
-	`columns_to_be_normalized`: a list of column names that should be normalized.
#### Log-Transformation:
-	`take_log`: a boolean value indicating whether the log of certain columns should be taken (True) or not (False).
-	`columns_log`: a list of column names for which the log should be taken if `take_log` is True. Needs a preanalyzation of the columns, recommended for columns that show a skewed distribution.
#### Filtering bad detected nuclei:
-	`remove_blur_lapl`: a boolean value indicating whether the blurred nuclei detected by the Laplacian should be removed (True) or not (False)
-	`remove_blur_lapl_treshold`: Integer value that defines the threshold. Rows that contain a blur value for the Laplacian below this threshold are removed.
-	`remove_blur_ski`: a boolean value indicating whether the blurred nuclei detected based on the discrimination level of blur should be removed (True) or not (False)
-	`remove_blur_lapl_treshold`: Value between 0 and 1. Values below this threshold are removed. 
-	`remove_similarity`: a boolean value indicating whether the nuclei with a certain similarity level should be removed or not. 
-	`similarity_threshold`: a Value between 0 and 1. Values below this threshold are removed.

## Task_1:

Task_1.ipynb contains in addition to the preprocessing step mentioned above, a pipeline for data analyzation and the application of regression models. 

During the analyzation part, features are explored with scatterplots.

A ridge regression and linear regression is built using cross validation where the best suited degree for a polynomial feature expansion is determined automatically. The test error (MAE or MSE) of the best ridge regression model and best linear regression model are compared and the better performing model is chosen. 
A 2D or ND-Regression is applied which gives back the best parameters. It also visualizes the results in case the a 2D-Regression was applied.
The `X_features` and `decide_y_feature` can be defined in both chapters individually. The `decide_x_feature` can just be adapted.

#### Parameters to adapt in the Beginning of the chapter:
- `maxdegree`: An integer value indicating up to which level the polynomial feature expansion should be tested.
- `alphas`: A list containing five possible alpha values for ridge regression, which controls the strength of the regularization. For all five alpha values a cross validation is applied, giving back the alpha resulting in the smallest error. 
- `K`: An integer value for the cross-validation, indicating how many sets of train/ test data should be computed.
- `X_features`: A list containing all the features that are interesting for the regression
- `Decide_y_feature`: A string with the y-value for the regression
- `Decide_x_feature`: An array containing the indices of the `X_feature` vector to be chosen. Can have multiple or just one index. 
- `mode_error`: ???mean_squared_error??? or ???mean_absolute_value??? depending on which loss function should be applied.

Remark: If a csv-file containing multiple transcription factors is read, an extraction of a subdata containing only one transcription factor has to be done. Otherwise, the model will compute the relationship of an aggregated set of transcription factors. The method to extract the subdata is listed in the notebook.

## Task_2:
Task_2.ipynb contains the preprocessing step described above and a pipeline for an unsupervised classification of different transcription factors. After applying a principal component analysis (PCA) the summarized features are clustered using a Kmean-classification algorithm.

#### Parameters to be defined: 
- `n_components`: An integer value that defines into how many features the original dataset should be summarized to during PCA.
- `Pca_excluded`: A list of columns that should be excluded in the PCA. It contains all the feature that should not be used for the classification task.
- `Random_state`: an integer value that is used as an input for the Kmeans algorithm to determine the random number generation for the centroid initialization.
- `N_clusters`: An integer number that the number of clusters

If `n_components` is set to two, a plot is provided to visualize the results of the classification.

#### Specific processing steps:
In order to select the best number of PCA components, a so called Elbow plot is made, which consists in computing which of the PCA components can explain which proportion of the variance of the data. If one can see an 'Elbow' on it, a sudden fast decrease, then it should be considered to take the `n_components` equal to the number of components each explaining a reasonable amount of the variance. 

Then to assess the quality of the clustering, we use the `sklearn silhouette_score` function, which is a metric using the distance between and intra clusters. The best value is $1$ and the worst is $-1$. It is always decreasing(from our experiment) with the number of clusters but remains helpful to help choosing `N_clusters`. 

To represent the quality of the model, we show a double entry dataframe with how many points from each TF in each cluster, as well as a coefficient representing how well the most representative cluster of a TF indeed represent it well. 









