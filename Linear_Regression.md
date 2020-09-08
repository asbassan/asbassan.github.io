# Linear Regression Techniques
- Very Simple Yet Very Powerful 

## Table Of Contents
1. [Pros](#pros)
2. [Cons](#cons)
3. [Libraries Used](#libraries-used)
4. [Method](#method)
<br>
<br>
<br>



### Pros
1. Simple Model
2. Easily interpretable.

### Cons
1. Sometimes too simple.
2. Assumes that the features are independent.
3. Highly sensitive to outliers.


### Libraries Used:
    
[sklearn.linear_model.LinearRegression](https://scikit-learn.org/stable/modules/generated/sklearn.linear_model.LinearRegression.html) 

[sklearn.preprocessing.PolynomialFeatures](https://scikit-learn.org/stable/modules/generated/sklearn.preprocessing.PolynomialFeatures.html)

[sklearn.metrics](https://scikit-learn.org/stable/modules/classes.html#module-sklearn.metrics)
    
    import the following :
    a. r2_score
    b. mean_squared_error

[sklearn.model_selection](https://scikit-learn.org/stable/modules/classes.html#module-sklearn.model_selection)

    import the following :
    a. train_test_split
    b. GridSearchCV

[sklearn.pipeline](https://scikit-learn.org/stable/modules/classes.html#module-sklearn.pipeline)

    import the following :
    a. Pipeline
    


### Method:

    a. Split the data:
        
        ```python
        x_train, x_test, y_train, y_test = train_test_split(x, y, test_size = 0.3, random_state = 42)
        #we will now work on the train data
        x_train_model = x_train.copy()
        x_test_model = x_test.copy()
        ```
    
    b. Below is the code for Linear Regression using PolynomialFeatures and GridSearchCV:

        ```python
        #we define the function for Polynomial regression

        def polyreg(x_train, x_test , y_train, y_test):
            #we define the hyperparameters
            degree = [1, 2, 3 , 4, 5]
            interaction_only = [True , False]
            include_bias = [True, False]
            normalize = [True, False]
            fit_intercept = [True, False]
            order = ['C', 'F']
            
            #instantiate polynomial features :

            polyfeat = PolynomialFeatures()

            linreg = LinearRegression()

            pipe = Pipeline(steps=[('polyfeat', polyfeat), ('linreg', linreg)])

            #we define the param grid for the gridsearchcv:

            param_grid = {
            'polyfeat__degree': degree,
            'polyfeat__interaction_only': interaction_only,
            'polyfeat__include_bias': include_bias,
            'linreg__normalize':normalize,
            'linreg__fit_intercept': fit_intercept
            }


            polyregmodel = GridSearchCV(pipe, param_grid, n_jobs=6, cv = 10, iid = False)

            polyregmodel.fit(x_train, y_train)

            y_predict = polyregmodel.predict(x_test)
            
            

            return ("PolynomialRegression", polyregmodel, polyregmodel.best_params_, r2_score(y_test, y_predict), mean_squared_error(y_test, y_predict) )

        ```

    c. Call using an example method below:
        ```python
        #calling the regression function 
    
        regresultup = polyreg(x_train_model, x_test_model , y_train, y_test)
        print("regression r2: ", regresultup[3])
        print("regression mean_squared_error: ", regresultup[4])
        print("regression model: ", regresultup[1])
        print("regression model parameters:", regresultup[2])
        ```