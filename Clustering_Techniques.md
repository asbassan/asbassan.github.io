# Clustering Techniques

## Table Of Contents
1. [Agglomerative Clustering](#AgglomerativeClustering)





### AgglomerativeClustering
1. Libraries Used :
    
    [scipy.cluster.AgglomerativeClustering](https://scikit-learn.org/stable/modules/generated/sklearn.cluster.AgglomerativeClustering.html) 

    [scipy.cluster.hierarchy](https://docs.scipy.org/doc/scipy/reference/cluster.hierarchy.html#module-scipy.cluster.hierarchy)

    [scipy.spatial.distance](https://docs.scipy.org/doc/scipy/reference/generated/scipy.spatial.distance.pdist.html)

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

    d. Calculate Cophenetic Coefficient(measure of accuracy):

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