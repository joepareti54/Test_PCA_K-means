This is a simpler case than https://github.com/joepareti54/CustomerSegments and yet it uses a similar pipeline of ML tools to illustrate the concept.

The k-means model predicts which cluster a given customer belongs to. We have 6 customers, therefore the prediction is a [1,6] array.
Next we calculate the proportion of customers that belong to a given cluster, by summing up the number of customers belonging to a given cluster, divided by the total number of customers (=len(purchases.index)).
The k-mean model was obtained on the ORIGINAL data (from PCA with 3 principal components), and using 4 centers: when using the method model.cluster_centers, the output is a 4x3 array, where the rows are cluster centers, and the columns are principal components.
To be abel to draw a comparison between original and new datasets, I need to transform the principal components back to the original features space (apples, oranges, ...)

Even though the k-means label is NOT invariant across runs, the transformed features should be consistent.
Let's inspect 2 independent simulations:
RUN 1 
k-means predictions --- original data
[3 1 0 2 1 0]
k-means predictions --- new data
[1 2 0 1 1 0]
k-means centers coordinates in original features space
      apples    oranges       figs      pears    berries   tomatoes     onions
0   3.815409  11.140532  10.647411  13.750075  12.931495   1.829856   8.183790
1   6.856632  12.917453  21.462751   2.476402   4.464275  21.608906   3.263839
2  20.845435   1.405542   5.974547   4.056566  -0.426516   0.890788   2.932460
3  11.810483  -0.521511  -8.194870   9.490480   4.634975   5.231688  12.172282
RUN 2
k-means predictions --- original data
[1 2 0 3 2 0]
k-means predictions --- new data
[2 3 0 2 2 0]
k-means centers coordinates in original features space
      apples    oranges       figs      pears    berries   tomatoes     onions
0   3.815409  11.140532  10.647411  13.750075  12.931495   1.829856   8.183790
1  11.810483  -0.521511  -8.194870   9.490480   4.634975   5.231688  12.172282
2   6.856632  12.917453  21.462751   2.476402   4.464275  21.608906   3.263839
3  20.845435   1.405542   5.974547   4.056566  -0.426516   0.890788   2.932460

The explanation is:
 the clusters are the same, just called differently once you retrained the model ("0" remained "0", "1" became "2", "2" became "3", "3" became "1").
https://stackoverflow.com/questions/65749167/different-k-means-results-for-repeated-runs-of-this-program
