The methods Oja's Rule, Sanger's Rule, and Independent Component Analysis (ICA) represent sequential stages in data analysis aimed at dimensionality reduction, decorrelation, and the extraction of independent components. All these methods are connected to Principal Component Analysis (PCA), but each has its unique features and applications. Below, we provide a detailed explanation of these methods, their theoretical connections, and the formulas describing their algorithms.

## Oja's Rule: Basics and Formulas

Oja's Rule extends the classical Hebbian learning rule by introducing weight normalization to converge towards the first eigenvector of the data covariance matrix. This allows the neuron to approximate the computation of the first principal component (PCA).

The formula for weight updates in Oja's Rule is:

$$
\Delta w_i = \eta (x_i y - y^2 w_i),
$$

where:
- $`  \eta  `$ is the learning rate, 
- $` \mathbf{x} = [x_1, x_2, \dots, x_n] `$ is the input vector,
- $` \mathbf{w} = [w_1, w_2, \dots, w_n] `$ are the weights of the neuron,
- $` y = \mathbf{w}^T \mathbf{x} `$ is the neuron output.

This method efficiently finds the first eigenvector but cannot extract additional components. This limitation is addressed in Sanger's Rule.

## Sanger's Rule: Extending Oja's Rule for PCA

Sanger's Rule is a modification of Oja's Rule that enables the computation of multiple principal components. It introduces a correction term to remove the influence of previously computed components, preserving orthogonality among them.

The formula for Sanger's Rule is:

$$
\Delta w_{ij} = \eta \left( x_i y_j - \sum_{k=1}^j y_k w_{ik} \right),
$$

where:
- $` \mathbf{y} = [y_1, y_2, \dots, y_m] `$ are the neuron outputs (projections onto the principal components),

- $` \sum_{k=1}^j y_k w_{ik} `$ is the sum of corrections to eliminate the influence of previous components.

Unlike traditional PCA, which computes the components through eigen decomposition or via SVD, Sanger's Rule enables an online, iterative approach to compute multiple principal components. This is particularly useful when dealing with streaming data or datasets too large to fit into memory

## Independent Component Analysis (ICA): From PCA to Independence

After PCA, data becomes decorrelated but may still retain higher-order dependencies. ICA addresses the problem of finding independent components by minimizing mutual information between them.

The weight update formula for ICA can be written as:

$$
\Delta w_i = \eta \left[ x_i - g(\mathbf{w}^T \mathbf{x})w_i \right],
$$

where:
- $` g(\cdot) `$ is a non-linear function (e.g.,$` \tanh `$ or sigmoid),
- $` \mathbf{w}^T \mathbf{x} `$ is the linear combination of input signals.

ICA assumes that mixed signals are a superposition of independent sources. The goal of the method is to find a weight matrix $` \mathbf{W} `$ that extracts these sources using the statistical properties of the data (e.g., maximizing negentropy).

## Connection to PCA and Advantages

PCA, implemented through Oja's and Sanger's Rule, effectively reduces data dimensionality while preserving the primary variance structure. However, it does not account for non-linear dependencies among variables. ICA, on the other hand, is aimed at uncovering hidden independent sources, making it indispensable for tasks such as signal processing (e.g., separating sound or image sources).

## 2D grid of output neurons' weights as an image

![](https://github.com/Pqlet/OJa/blob/main/image-pres/training_ims.gif)

