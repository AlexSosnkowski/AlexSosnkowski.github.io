---
layout: page
title: Principle Component Analysis
thumbnail: /pca/thumbnail.png
blurb: Do you have extremely high dimensional data that you want to plot on a nice 2d or 3d graph? Than PCA might just be the solution for you!
---
A while back I read an interesting paper ([this](https://arxiv.org/pdf/2310.06824) one), and its usage of Principle Component Analysis or PCA intrigued me. It was the first time I have ever heard of the technique, so I went about learning more the only way I know how - by searching the web! 

I found quite a few excellent blogs (linked at the bottom), however, I wasn't able to find any writeups that showed a coded implementation of PCA that wasn't reliant on a library implementation like Scikit-learn's version of PCA. After researching the mathematical foundation / theory behind PCA, I realized it is incredibly simple and straightforward to implement. Lets jump in!

## The Goal

Humans have gotten incredibly good at representing two, three, or even four dimensional datasets with traditional graphing techniques. The problem is that many real world datasets can have tens if not hundreds of features. This curse of dimensionality can be especially annoying when we are trying to understand and gain intuition about the data itself, as we have no straightforward way of visualizing it without simply dropping dimensions and loosing significant amounts of information. But what if there was a way we could squish down a high dimensionality dataset to a few key features (say two or three) that are easy to plot? This is exactly what PCA lets us do!

## Working with Real Data

One of the oldest metrics to observe the relationship between features in a dataset is correlation. The correlation between two features is effectively a normalized covariance.

Our goal is to generate two or three new features that are a linear combination of all other features such that our new features pack as much information as possible. Thus, we do not want our new features to be correlated with each other as this would be wasted "information" i.e more compression is potentially possible.

An initial idea may be to simply select the most correlated features with our target value. There are numerous problems with this idea, but for fun lets try it on a real dataset! 

I will begin by using the sklearn wine toy dataset that asks us to classify between 3 different wine cultivators in Italy using 13 chemical features. 

A quick look at the corelation between features in the dataset is shown below.

<img src="./pca/corr.png">

It looks like total_phenols and od280/od315_of_diluted_wines are the strongest correlated features with our target so lets plot those two features on their own to see if our data has a clear separation! 

<img src="./pca/naive.png">

It's certainly not terrible but it still leaves much too be desired as the classes mix in difficult to linearly separate ways. 

What we need is a more advanced, informed technique. In comes PCA.

## A Brief Review of Covariance Matrices and Eigenvalues / Eigenvectors

Let's recall that a m x n matrix $A$ can be considered a kind of linear transformation that takes vectors in $\mathbb R^n$ and returning some new vector in $\mathbb R^m$ where $\mathbb R^a$ is the $a$ dimensional real vector space. An Eigen vector $v$ is a vector for a square matrix $A$ such that $Av = \lambda v$ or, in essence, a vector that is transformed into a scaled version of itself (thus preserving its direction). $\lambda$ is the Eigen value associated with $v$ and it is how much $v$ gets scaled by with each transformation. 

## Back to PCA

Returning to our covariance matrix, there are two key features we can leverage. A covariance matrix is symmetric and positive semi-definite. Symmetry comes from the simple fact that the $cov(a, b) = cov(b, a)$. Showing covariance matrices are positive semi-definite is a much more involved process left out for brevity (for more info see [here](https://statproofbook.github.io/P/covmat-psd.html)). This ensures that our matrix is square and that we have non-negative Eigen values. 

Thus, we can find the Eigen values and Eigen vectors of our covariance matrix! We can do this super easily with Numpy using the code shown below (how Eigen values / vectors are numerically approximated merits its own blog, Numpy for example uses [this](https://netlib.org/lapack/explore-html-3.6.1/d9/d8e/group__double_g_eeigen_ga8ec1625302675b981eb34ed024b27a47.html)).

````
#rowvar is set to false here because each row 
#represents an observation, not a variable 
cov = np.cov(x, rowvar=False)
E, V = np.linalg.eig(cov) # eigen values and vectors
````

These Eigen vectors are called principle components. The Eigen values for each of these vectors represent how "far" we scale or stretch the vector when we apply the covariance as a transformation. This means a larger Eigen value (remember they are guaranteed to be non-negative), corresponds to a bigger increase in variance. Which is exactly what we want since this means data is spread the largest across the axis and thus the axis contains more "information" about the data than lower spread axes! 

So all we have to do is sort our list of Eigen vectors to prioritize the ones with the highest Eigen values. From there, it is a simple process of projecting our data onto the top (highest Eigen value) Eigen vectors for however many dimensions we want in our final transformed dataset to be (for us this is 2). The code to do this is also incredibly simple and is reproduced below. 

````
#V here is our Numpy array of Eigen Vectors 
proj = np.reshape(V[:,0:d], (p, d))
return x @ proj
````

For the wine dataset, once we plot our data projected onto the first two principle components we get the results below. 

<img src="./pca/ourpca.png">

Lets compare this to the results we get using Scikit-learn.

<img src="./pca/sklearnpca.png">

Uhhhhhh.... why is it flipped? That can't be good right? Actually, I believe this is a fairly simple issue stemming from having two different ways of calculating the Eigen vectors (Scikit-learn's way and Numpy's way)! An Eigen vector can be multiplied by any non-zero scalar and still be a valid Eigen vector for the given Eigen value. To show this, consider the following for some matrix $A$, non-zero scalar $\alpha$, Eigen vector $v$, and Eigen value $\lambda$. 

$A(\alpha v) = \alpha (A v) = \alpha \lambda v = \lambda(\alpha v)$

So $(\alpha v)$ still matches our definition of an Eigen vector for Eigen value $\lambda$. 

After flipping our Eigen vectors (multiplying them by -1) we get the following result which matches Scikit-learn's implementation.

<img src="./pca/apca.png">

One final trick we can use to quantify the effectiveness of our projections is to calculate the percentage of variance our results account for. To do this, we simply take the Eigen value for the particular principle component and divide it by the sum of all our Eigen values (the classical way to get percentages). For the wine dataset I got the following.  

````
Principle Component 0 accounts for 0.3619884809992634% of the variance!
Principle Component 1 accounts for 0.1920749025700893% of the variance!
````

So having more than 50% of the variance in a 13 dimensional dataset accounted for by just two axes is not terrible!

We can try other datasets as well, including the famous Iris dataset.

<img src="./pca/anotherpca.png">

We can also do 3d plots for when we use 3 dimensions in our projection!

<img src="./pca/anotherpca3d.png">


You can view and run my complete Jupyter Notebook on Google Colab [here](https://colab.research.google.com/drive/13g6LOxFrkEXbphEVFBCCMHi-HhrCz2aq?usp=sharing).


## Useful References

[https://builtin.com/data-science/step-step-explanation-principal-component-analysis](https://builtin.com/data-science/step-step-explanation-principal-component-analysis)

[https://www.realcode4you.com/post/principal-component-analysis-pca-using-wine-dataset-hire-data-science-expert](https://www.realcode4you.com/post/principal-component-analysis-pca-using-wine-dataset-hire-data-science-expert)