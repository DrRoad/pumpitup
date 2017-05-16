# Pump it Up: Data Mining the Water Table
## My analysis for the Driven Data competition

By [Ville Heilala](https://heila.la), 2017

## Research question

The [Driven Data competition](https://www.drivendata.org/competitions/7/pump-it-up-data-mining-the-water-table/) describes the question as follows:

>Can you predict which water pumps are faulty?

>Using data from Taarifa and the Tanzanian Ministry of Water, can you predict which pumps are functional, which need some repairs, and which don't work at all? ... Predict one of these three classes based on a number of variables about what kind of pump is operating, when it was installed, and how it is managed. A smart understanding of which waterpoints will fail can improve maintenance operations and ensure that clean, potable water is available to communities across Tanzania.

<p align="center">
  <img src="https://upload.wikimedia.org/wikipedia/commons/0/04/Flickr_-_usaid.africa_-_Water_pump_provided_by_USAID.jpg" width="500"/><br>
  Picture: <a href="https://commons.wikimedia.org/wiki/File:Flickr_-_usaid.africa_-_Water_pump_provided_by_USAID.jpg">Wikimedia Commons</a>
</p>

## The data

Data can be obtained from the competition site by registering and downloading the data sets. Data set contains training variables, labels and test set for participating the competition. Total data size is 74250 observations, 40 independent variables and 1 dependent variable. Predicted status group can be either "functional", "non functional" or "functional needs repair".

## Tools

* [Anaconda](https://www.continuum.io/) + [Jupyter](http://jupyter.org/)
* [Numpy](http://www.numpy.org/) Stack, [pandas](http://pandas.pydata.org/), [scikit-learn](http://scikit-learn.org/stable/)

## Methods

* basic exploration methods
* [Random Forest](random_forest.md)
* [Density-based spatial clustering of applications with noise (DBSCAN)](https://en.wikipedia.org/wiki/DBSCAN)
  * Ester, M., Kriegel, H., Sander, J. & Xu, X. (1996). [A Density-Based Algorithm for Discovering Clusters in Large Spatial Databases with Noise](https://www.aaai.org/Papers/KDD/1996/KDD96-037.pdf)
  * scikit-learn: [sklearn.cluster.DBSCAN](http://scikit-learn.org/stable/modules/generated/sklearn.cluster.DBSCAN.html)

## Workflow

I'm using analysis workflow prensented in [this](https://www.quora.com/What-is-the-workflow-or-process-of-a-data-scientist) Quora answer.

### 1. Ask A Question

This question is provided by the competition.

>Can you predict which water pumps are faulty?

### 2. Get the Data

* [Jupyter notebook: Get the data](pumpitup_getdata.ipynb)

### 3. Explore the Data

* [Jupyter notebook: Explore the data](pumpitup_explore.ipynb)
  * A basic starting point using R is presented in a tutorial by [DataCamp](https://www.datacamp.com/community/open-courses/drivendata-water-pumps-challenge#gs.UjARtQI)
  * The main problem with the data is missing values: 12 of the 40 variables have missing data, which needs to be dealt with. Exploration revealed some potential ways to do imputation.
  * Categorical values need to be converted numerical. Numerical values might need to be normalized.
  
<p align="center">
  <img src="status_group_map.png"/><br>
  Plotting 2000 pumps each by status_group
</p>

### 4. Model the data

* [Jupyter notebook: Preprocess the data I: Get missing gps_height values](pumpitup_missing_gps_height.ipynb)
  * Using [geocoder](http://geocoder.readthedocs.io/) library to obtain missing gps_height values
* [Jupyter notebook: Preprocess the data II: Process variables](pumpitup_preprocess.ipynb)
  * Combine train and test sets to do processing for the whole data, combine train set and train labels
  * Drop, round, combine to larger bins, normalize, [one-hot encode](https://www.quora.com/What-is-one-hot-encoding-and-when-is-it-used-in-data-science)
  * Make a new variable by clustering latitude and longitude with DBSCAN
* [Jupyter notebook: Model the data I: Optimize metaparameters](pumpitup_model_metaparameters.ipynb)
  * Excluding few redundant variables
  * Estimating optimal max_features parameter

<p align="center">
  <img src="max_features.png"/><br>
  Optimizing max_features parameter, which is the number of features to consider when looking for the best split
</p>

* [Jupyter notebook: Model the data II: Making prediction](pumpitup_model.ipynb)

## Results

Best version of this model scored 0.8239 in the competition.
