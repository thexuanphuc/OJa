The methods Oja's Rule, Sanger's Rule, and Independent Component Analysis (ICA) represent sequential stages in data analysis aimed at dimensionality reduction, decorrelation, and the extraction of independent components. All these methods are connected to Principal Component Analysis (PCA), but each has its unique features and applications. Below, we provide a detailed explanation of these methods, their theoretical connections, and the formulas describing their algorithms.

## Oja's Rule: Basics and Formulas

Oja's Rule extends the classical Hebbian learning rule by introducing weight normalization to converge towards the first eigenvector of the data covariance matrix. This allows the neuron to approximate the computation of the first principal component (PCA).

The formula for weight updates in Oja's Rule is:

$$
\Delta \mathbf{w} = \eta y (\mathbf{x} - y \mathbf{w})
$$

where:
- $`  \eta  `$ is the learning rate, 
- $` \mathbf{x} = [x_1, x_2, \dots, x_n] `$ is the input vector,
- $` \mathbf{w} = [w_1, w_2, \dots, w_n] `$ are the weights of the neuron,
- $` y = \mathbf{w}^T \mathbf{x} `$ is the neuron output.

We will prove that the weight $\mathbf{w}$ converge to the first eigenvector:

- If we multiply two sides of equation with $\mathbf{w}^T$:

$$\Delta \mathbf{w} = \eta y (\mathbf{x} - y \mathbf{w}) \text{  }\vert  \mathbf{w}^T$$

$$\Delta (\mathbf{w}^T \mathbf{w}) = \eta y \mathbf{w}^T (\mathbf{x} - y \mathbf{w}) = y^2 \cdot (1 - \Vert W \Vert ^ 2)$$

$$\Delta (\mathbf{w}^T \mathbf{w}) = y^2 \cdot (1 - \Vert \mathbf{w} \Vert ^ 2) = 0$$
$\Rightarrow$ We normaize $ \Vert \mathbf{w} \Vert = 1$ to make it converge

- The weight $\mathbf{w}$ is eigenvector of Input covariance matrix $\mathbf{x}\mathbf{x}^T$


$$\Delta \mathbf{w} = \eta(\mathbf{x}\mathbf{x}^T\mathbf{w} - \mathbf{w}^T\mathbf{x}\mathbf{x}^T\mathbf{w}\mathbf{w}) $$

$$\Delta \mathbf{w}= \mathbf{Q} \mathbf{w} - (\mathbf{w}^T\mathbf{Q} \mathbf{w})\mathbf{w}$$

$\rightarrow$ If input $\mathbf{x}$ is zero mean, we have the matrix $\mathbf{Q} = \mathbf{x}\mathbf{x}^T$ become covariance matrix. 



$\Rightarrow$ This method efficiently finds the first eigenvector but cannot extract additional components. This limitation is addressed in Sanger's Rule.

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

