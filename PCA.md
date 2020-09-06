## Principal Component Analysis

1. Libraries Used :
    
    [sklearn.decomposition.PCA](https://scikit-learn.org/stable/modules/generated/sklearn.decomposition.PCA.html) 

    [sklearn.preprocessing.StandardScalar](https://scikit-learn.org/stable/modules/generated/sklearn.preprocessing.StandardScaler.html)


2. Method:

    a. Split the data into train and test:

        ```python
        X_train, X_test, y_train, y_test = train_test_split(creditData[features], creditData[target], test_size =0.01, shuffle= True)
        ```
    b. Apply standardization before PCA :

        ```python
        scaler = StandardScaler()
        scaler.fit(X_train)
        X_train = scaler.transform(X_train)
        print(X_train)
        ```

    c. fit the PCA :
    
        ```python
        pca = PCA(n_components = 23)
        pca.fit(X_train)
        ```

    d. Plot the diagrams:

        ```python
        plt.bar(list(range(1,7)),pca.explained_variance_ratio_,alpha=0.5, align='center')
        plt.ylabel('Variation explained')
        plt.xlabel('eigen Value')
        plt.show()

        plt.step(list(range(1,7)),np.cumsum(pca.explained_variance_ratio_), where='mid')
        plt.ylabel('Cum of variation explained')
        plt.xlabel('eigen Value')
        plt.show()

        plt.figure()
        plt.plot(np.cumsum(pca.explained_variance_ratio_))
        plt.xlabel('Number of Components')
        plt.ylabel('Variance (%)') 
        plt.title('Explained Variance')
        plt.show()      
        ```

    e. Choose the components and repeate the PCA fit:

        ```python
            pca3 = PCA(n_components=3, random_state = 42)
            pca3.fit(XScaled)
            print(pca3.components_)
            print(pca3.explained_variance_ratio_)
            Xpca3 = pca3.transform(XScaled)
        ```
    f. Apply the same pca3 to test data:

        ```python
           X_test_pca = pca.transform(X_test) 
        ``` 

3. Measure of accuracy: None
4. Observations:
    a. sns.pairplot(pd.DataFrame(Xpca3)) could show the independence of chosen variables.