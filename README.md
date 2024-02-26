# kmeans-rfm-analysis-python
Welcome to my repository for doing kmeans clustering analysis with rfm variables using python and Jupyter notebooks.

1. Install the following libraries
- pandas
- numpy
- datetime
- matplotlib.pyplot
- KMeans
- seaborn

2. Create a dataset as CSV with the following columns.
- cust_id
- date
- OrdNum
- rev

Every row of the dataset should be 1 order. Your dataset should be between 0.5 to 2 years of data. You can add other user-, order-, and or product-related data if you want to do explorative analysis after based on your kmeans segments.

3. Edit in your Location and file name in CSV file in the 1. ### Import, Filter, Format Dataset ### section of the kmeans_clustering_script.ipynb.

4. Run 1. ### Import, Filter, Format Dataset ### and make sure everything works accordingly.

5. Run 2. ### Creating RFM dataset ### and make sure everything works accordingly.

6. Run 3. ### Determining amount of Clusters ### and make sure everything works accordingly
The elbow plot is your first measure of determining the amount of clusters for your kmeans analysis.

7. Insert the amount of clusters in n_clusters in 4. ### Performing RFM Analysis ###.

8. Run 4. ### Performing RFM Analysis ### and check if your happy with the distribution in kmeans_basic_centers.

9. Adjust the amount of clusters if neccessary and re-run 4. ### Performing RFM Analysis ###.

10. Perform an outlier analysis on your clusters by running 5. ### Outlier Cluster Analysis ### and determine if you need to exclude clients or purchases from your analysis.

11. Name your clusters (and add clusters if neccessary) in 6. ### Rename the Clusterlabels ### and run this code.

12. Edit the desired location for exporting your datasets in 7. ### Export Datasets ### and run this code.
