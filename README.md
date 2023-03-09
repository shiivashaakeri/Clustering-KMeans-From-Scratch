# Clustering using k-means from Scratch
This is a Python implementation of k-means clustering algorithm from scratch. It allows you to cluster data points into `K` clusters using Euclidean distance as a similarity metric.

## Getting Started
1. Install the required packages:
``` bash
pip install numpy pandas matplotlib sklearn
```

2. Import the KMeans class:
``` python
from kmeans import KMeans
```

3. Load a dataset:
``` python
from sklearn import datasets

iris = datasets.load_iris()
X = iris.data
Y = iris.target
```

## Usage
Instantiate the `KMeans` class with the number of clusters `K` and maximum number of iterations `maxIter`:
``` python
model = KMeans(K=5, maxIter=150)
```

Fit the model to the data:
``` python
hist = model.fit(X)
```
Plot the convergence of the algorithm:
``` python
plotX = list(range(len(hist)))
plt.plot(plotX, hist)
xTicks = [plotX[int((len(plotX) - 1) / 10 * i)] for i in range(10)]
plt.xticks(xTicks)
plt.show()
```

Get the mean point and variance for each cluster:
``` python
meanDists, variances = model.getMetrics()
for i in range(len(meanDists)):
    print('\nFor cluster %d:' % i)
    print('Mean Point:', meanDists[i])
    print('Variance:', variances[i])
```

Get the intra-to-inter ratio for each cluster:
``` python
interClusterDistances = model.getInterClusterDistances()
intraClusterDistances = model.getIntraClusterDistances()
for i in range(len(meanDists)):
    print('\nFor cluster %d:' % i)
    if type(meanDists[i]) == str:
        print('Intra-to-Inter Ratio: Empty Cluster')
    else:
        print('Intra-to-Inter Ratio:', intraClusterDistances[i] / interClusterDistances[i])
```
