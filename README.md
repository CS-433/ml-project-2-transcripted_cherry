# ml-project-2-transcripted_cherry

ML4sciences project with the SUTER LAB about transcription factors!







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

