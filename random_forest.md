# Random Forest

* Ensemble method for classification and regression
* Forest = collection of multiple decision trees
* Random = decision trees are generated using random subset of data
..* bootstrapping: tree has unique set of data = random subset of the original data with replacement
* Resul is the mode (in classification) or mean (in regression) of the individual trees
* 

## Python and scikit-learn

* A random forest classifier: [sklearn.ensemble.RandomForestClassifier](http://scikit-learn.org/stable/modules/generated/sklearn.ensemble.RandomForestClassifier.html#sklearn.ensemble.RandomForestClassifier)
* A random forest regressor: [sklearn.ensemble.RandomForestRegressor](http://scikit-learn.org/stable/modules/generated/sklearn.ensemble.RandomForestRegressor.html#sklearn.ensemble.RandomForestRegressor)

## References

[Breiman, L. (2001). Random Forests.](https://www.stat.berkeley.edu/~breiman/randomforest2001.pdf)

[Leo Breiman and Adele Cutler: Random Forests](https://www.stat.berkeley.edu/~breiman/RandomForests/)
