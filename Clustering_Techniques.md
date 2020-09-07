# Clustering Techniques
- Play balancing act between compression and accuracy

## Table Of Contents
1. [KMeans Clustering](#KMeansClustering)
2. [Agglomerative Clustering](#AgglomerativeClustering)
<br>
<br>
<br>



### KMeansClustering
1. Libraries Used :
    
    [scipy.cluster.Kmeans](https://scikit-learn.org/stable/modules/generated/sklearn.cluster.KMeans.html#sklearn.cluster.KMeans) 

    [scipy.spatial.distance.cdist](https://docs.scipy.org/doc/scipy/reference/generated/scipy.spatial.distance.cdist.html)



2. Method:

    a. scale the attributes(standard scalar can be applied):

        ```python
        custDataScaled = custDataAttr.apply(zscore)
        ```
    b. Check the distortions for various clusters  :

        ```python
        clusters=range(1,10)
        meanDistortions=[]

        for k in clusters:
            model=KMeans(n_clusters=k)
            model.fit(techSuppScaled)
            prediction=model.predict(techSuppScaled)
            meanDistortions.append(sum(np.min(cdist(techSuppScaled, model.cluster_centers_, 'euclidean'), axis=1)) / techSuppScaled.shape[0])


            plt.plot(clusters, meanDistortions, 'bx-')
            plt.xlabel('k')
            plt.ylabel('Average distortion')
            plt.title('Selecting k with the Elbow Method')
        ```

    c. use the optimial value of k obtained above :
    
        ```python
            # Let us first start with K = 3
            final_model=KMeans(3)
            final_model.fit(techSuppScaled)
            prediction=final_model.predict(techSuppScaled)

            #Append the prediction 
            tech_supp_df["GROUP"] = prediction
            techSuppScaled["GROUP"] = prediction
            print("Groups Assigned : \n")
            tech_supp_df.head()
        ```

    d. Check the various features:

        ```python
            techSuppClust = tech_supp_df.groupby(['GROUP'])
            techSuppClust.mean()
        ```

    e. Check the variations within group:

        ```python
            techSuppScaled.boxplot(by='GROUP', layout = (2,4),figsize=(15,10))
        ```  

    f. take decision based on observations from point d and e above.

<br>
<br>


### AgglomerativeClustering
1. Libraries Used :
    
    [scipy.cluster.AgglomerativeClustering](https://scikit-learn.org/stable/modules/generated/sklearn.cluster.AgglomerativeClustering.html) 

    [scipy.cluster.hierarchy](https://docs.scipy.org/doc/scipy/reference/cluster.hierarchy.html#module-scipy.cluster.hierarchy)

    [scipy.spatial.distance.pdist](https://docs.scipy.org/doc/scipy/reference/generated/scipy.spatial.distance.pdist.html)

    [scipy.stats](https://docs.scipy.org/doc/scipy/reference/generated/scipy.stats.zscore.html)

2. Method:

    a. scale the attributes:

        ```python
        custDataScaled = custDataAttr.apply(zscore)
        ```
    b. Create a cluter model :

        ```python
        model = AgglomerativeClustering(n_clusters=3, affinity='euclidean',  linkage='average')
        ```

    c. fit the  model :
    
        ```python
        model.fit(custDataScaled)
        ```

    d. Calculate Cophenetic Coefficient(measure of accuracy - Bigger the better : range (0 - 1)):

        ```python
            z = linkage(custDataScaled, metric = 'euclidean' , method  = 'average')
            c, coph_dists = cophenet(z, pdist(custDataScaled))
            c
        ```

    e. Draw dendrogram:

        ```python
            plt.figure(figsize=(10, 5))
            plt.title('Agglomerative Hierarchical Clustering Dendogram')
            plt.xlabel('sample index')
            plt.ylabel('Distance')
            dendrogram(z, leaf_rotation=90.,color_threshold = 40, leaf_font_size=8. )
            plt.tight_layout()
        ```