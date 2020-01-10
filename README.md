# Classification-MachineLearning
Step by Step Classification in Machine Learning

In this work we are going to develop a machine learning classification application. This Project consist of four steps. 
<pre>1.	First step is loading, Analyzing and data manipulating the data (one-hot-encoding, assigning value for null field) 
2.	The second step is calculating importance of each feature and select the feature
3.	The third step is selecting and tuning the algorithms and evaluating performance of each algorithms
4.	The last step is finalizing the model (validation)</pre>
In this project we are going to use Sonar Mines vs Rocks dataset. We try to predict metal or rock objects from sonar return data.

**1. Loading, Analyzing and Manipulating Data**  
This dataset dates to the Cold War and consists of sonar data. The name and setup suggest that the aim of this data is do distinguish between rocks and metal structures such as sea mines on the seafloor. The experimental setup was as follows:
<pre>•	A metal cylinder and a cylindrical rock, both of length 5 ft, placed on sandy ocean floor 
•	Sonar impulse: wide-band linear FM 
•	Return sampling in 10 meters 
•	Return sample aspect angle: spanning 90° (metal cylinder) and 180° (rock) 
•	Input data is a normalized spectral envelope covering 60 samples 
•	208 samples selected from 1200 (by which criteria?); 111 metal samples, 97 rock samples</pre>

| x |   1    |    2   | .... |   59   |  60 |
| - | ------ | ------ | ---- | ------ | --- |
| 0 | 0.0200 | 0.0371 | ---  | 0.0090 |  R  |
| 1 | 0.0453 | 0.0523 | ---  | 0.0052 |  R  |


The detail information about the data set provided [here](https://archive.ics.uci.edu/ml/datasets/Connectionist+Bench+(Sonar,+Mines+vs.+Rocks)
The label associated with each record contains the letter "R" if the object is a rock and "M" if it is a mine (metal cylinder). For running algorithms on dataset efficiently we have to make some preprocessing operation on dataset. We are going to answer the questions listed below to prepare data.
<pre>
•	Is the separation between rocks and mines obvious? 
•	How correlated are the variables? 
•	Do we need to standardize? 
•	Are there outliers?
</pre>
from pandas.tools.plotting import andrews_curves, parallel_coordinates
![Alt text](https://i.hizliresim.com/va1Jvm.jpg "Optional title")

<b>df.plot.box(figsize = (12,4), xticks=[]) pass </b>
![Alt text](https://i.hizliresim.com/LvVOWa.jpg "Optional title")

From figure 2 it is obvious we have to standardize data. For standardizing data, we will use StandardScaler and RobustScaler 
from sklearn.preprocessing import StandardScaler, RobustScaler
</br>
<b>data_scaled = DataFrame(StandardScaler().fit_transform(data), columns=data.columns)</b>

If there are outliers, we will use a robust routine
ata_robust = DataFrame(RobustScaler().fit_transform(data), columns=data.columns)
after this preprocessing operation we will use PCA (Principle Component Analysis) for dimension reduction.
</br></br>
<b>from sklearn.decomposition import PCA </br>
pca = PCA() </br>
data_scaled_pca = DataFrame(pca.fit_transform(data_scaled), columns=data.columns) </br>
imp = clf.best_estimator_.feature_importances_ </br>
idx = np.argsort(imp)</b> </br></br>

![Alt text](https://i.hizliresim.com/r0lJoV.jpg "Figure 3. Importance of Each Feature")
</br>
In figure above we showed each feature importance via graph. So, we can eliminate some of these features according to their importance on dataset.

**2. selecting and tuning the algorithms and evaluating performance of each algorithms**

We don't know what algorithms will do well on this dataset. Gut feel suggests distance-based algorithms like k-Nearest Neighbors and Support Vector Machines may do well. We will use 10-fold cross validation for test. The dataset is not too small, and this is a good standard test harness configuration. We will evaluate algorithms using the accuracy metric.  As first step I will import all required libraries to my project.
</br>
![Alt text](https://i.hizliresim.com/7B0yrP.jpg "Optional title")
</br>
we adjust Test options and define evaluation metric. We set number of folds, seed and scoring parameters.</br>
![Alt text](https://i.hizliresim.com/P7LOZ6.jpg "Optional title")
</br>
We will select a suite of different algorithms capable of working on this classification problem. We used six different classification problem.
</br>
![Alt text](https://i.hizliresim.com/gP39JZ.jpg "Optional title")
</br>
The algorithms all use default tuning parameters. Let's compare the algorithms. We will display the mean and standard deviation of accuracy for each algorithm as we calculate it and collect the results for use later.</br>

![Alt text](https://i.hizliresim.com/Z5bOPk.jpg "Optional title")
</br>
This simple a classification sample. In this study we try to tell a classification problem step. As first step preprocessing operation was applied on dataset. After that classification algorithms were selected. The selected algorithms were performed on dataset. The last step is comparing success of each algorithm.
