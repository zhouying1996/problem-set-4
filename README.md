# Problem Set 4: Clustering

## Fork the repository

Fork the repository for the problem set 4, `problem-set-4` (https://github.com/macss-ml20/problem-set-4). _Remember, all final submissions should be a single rendered PDF with code produced in-line._ Also, don't forget to **open the pull request** once you've committed your final submission to your forked repository. It needs to be merged back into the course master branch to be considered "submitted". See the syllabus for details.

### The Data: State Legislative Professionalism

For the *second* "applied" part of the problem set, you will perform the three main clustering techniques we addressed in class (hierarchical, k-means, and Gaussian mixture models) on the Bowen and Greene state legislative professionalism data. In these data, there are four key features of interest, which record raw values for every state legislature in the U.S. from 1974-2010: 

  * Total session length 
  * Regular session length
  * Legislators' salaries
  * Expenditures per legislator

See the codebook for more details on these feature and the full set. 

### Performing k-Means By Hand

In this first part of the problem set, your goal is to gain a deeper conceptual understanding of the iterative process of k-means, which operates by initializing random cluster assignments, then updates cluster centroids, then cluster assignments, and so on, until convergence, which is defined by no furtehr changes to cluster configurations (i.e., optimal clusters definined by minimum sums of squares *within* clusters, and maximum sums of squares *between* clusters. 

In short, then, by answering each of the following questions, you will be performing k-means clustering "by hand" to see and demonstrate this iterative process. Your simulated data includes `n = 6` observations and `p = 2` features, and you should set the number of clusters, `k`, equal to two (i.e., you are hunting for 2 clusters within these data). I will get you started with the observations in the set. Run the following line to create your simulated data:

  > `x <- cbind(c(1, 1, 0, 5, 6, 4), c(4, 3, 4, 1, 2, 0))`

1. (5 points) Plot the observations.

2. (5 points) Randomly assign a cluster label to each observation. Report the cluster labels for each observation *and* plot the results with a different color for each cluster (*remember to set your seed first*).

3. (10 points) Compute the centroid for each cluster.

4. (10 points) Assign each observation to the centroid to which it is closest, in terms of Euclidean distance. Report the cluster labels for each observation.

5. (5 points) Repeat (3) and (4) until the answers/clusters stop changing.

6. (10 points) Reproduce the original plot from (1), but this time color the observations *according to the clusters labels you obtained* by iterating the cluster centroid calculation and assignments. 

### Clustering State Legislative Professionalism

1. Load the state legislative professionalism data. See the codebook (or above) for further reference.

2. (5 points) Munge the data: 

    a. select only the continuous features that should capture a state legislature’s level of “professionalism” (session length (total and regular), salary, and expenditures); 
    b. restrict the data to only include the 2009/10 legislative session for consistency; 
    c. omit all missing values; 
    d. standardize the input features;
    e. and anything else you think necessary to get this subset of data into workable form (hint: consider storing the state names as a separate object to be used in plotting later) 

3. (5 points) Diagnose clusterability in any way you’d prefer (e.g., sparse sampling, ODI, etc.); display the results and discuss the likelihood that natural, non-random structure exist in these data. _Hint:_ We didn't cover how to do this R in class, but consider `dissplot()` from the `seriation` package, the `factoextra` package, and others for calculating, presenting, and exploring the clusterability of some feature space.
 
4. (5 points) Fit an **agglomerative hierarchical** clustering algorithm using any linkage method you prefer, to these data and present the results. Give a quick, high level summary of the output and general patterns. 

5. (5 points) Fit a **k-means** algorithm to these data and present the results. Give a quick, high level summary of the output and general patterns. Initialize the algorithm at `k = 2`, and then check this assumption in the validation questions below.

6. (5 points) Fit a **Gaussian mixture model via the EM algorithm** to these data and present the results. Give a quick, high level summary of the output and general patterns. Initialize the algorithm at `k = 2`, and then check this assumption in the validation questions below.

7. (15 points) Compare output of all in visually useful, simple ways (e.g., present the dendrogram, plot by state cluster assignment across two features like salary and expenditures, etc.). There should be several plots of comparison and output.

8. (5 points) Select a *single* validation strategy (e.g., compactness via min(WSS), average silhouette width, etc.), and calculate for all three algorithms. Display and compare your results for all three algorithms you fit (hierarchical, k-means, GMM). _Hint:_ Here again, we didn't cover this in R in class, but think about using the `clValid` package, though there are many other packages and ways to validate cluster patterns across iterations.

9. (10 points) Discuss the validation output, e.g.,

 a. What can you take away from the fit? 
 b. Which approach is optimal? And optimal at what value of k? 
 c. What are reasons you could imagine selecting a technically “sub-optimal” clustering method, regardless of the validation statistics? 

