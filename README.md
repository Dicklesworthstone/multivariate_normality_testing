# Multivariate Normality Testing via 3D Projections

![License: MIT](https://img.shields.io/badge/License-MIT-blue.svg)

**By Jeffrey Emanuel, created on 4/24/2025**

## Overview

This web application implements a novel approach to multivariate normality testing using random 3D projections. It provides an interactive, visual way to assess whether high-dimensional data follows a multivariate normal distribution by examining the distribution of ellipsoid fit errors from multiple random projections.

## Core Methodology

The application leverages a fundamental property of multivariate normal distributions: **any linear projection of a multivariate normal (MVN) distribution is itself normal**. Departures from normality in high-dimensional space often manifest as non-ellipsoidal shapes in lower-dimensional projections.

The testing process follows these steps:

1. **Generate/upload high-dimensional data**
   - A multivariate normal dataset serves as the reference
   - Test data (potentially non-normal) for comparison

2. **Projection Testing**
   - Randomly select 3 dimensions for projection
   - Project the N-dimensional data onto these 3 dimensions
   - Fit an ellipsoid to the projected points using eigendecomposition of the sample covariance matrix
   - Calculate Mean Squared Error (MSE) between points and the fitted ellipsoid surface

3. **Distribution Comparison**
   - Collect MSE values from thousands of random projections
   - Compare the MSE distributions between reference and test datasets
   - Apply statistical tests to determine significant differences

## Statistical Implementation

### Ellipsoid Fitting

The ellipsoid fitting algorithm uses principal component analysis (PCA) to determine shape and orientation:
- Calculate the covariance matrix of the projected points
- Perform eigendecomposition to find principal axes and their lengths
- The eigenvectors define the orientation of the ellipsoid
- The eigenvalues determine the radii along each principal axis
- Scale the ellipsoid to minimize the overall MSE

### Distribution Comparison

The Mann-Whitney U test is employed to determine if the MSE distributions differ significantly:
- Non-parametric test that doesn't assume normality of the MSE distributions
- Accounts for ties in the data
- Provides a p-value indicating statistical significance of differences

### Normality Score Calculation

A heuristic "normality score" combines multiple factors:
- Ratio of mean MSE between test and reference distributions
- Ratio of standard deviations of MSE distributions
- p-value from the Mann-Whitney U test
- Higher scores indicate greater similarity to multivariate normal data

## Mathematical Advantages

From a mathematical perspective, this approach offers several advantages:

1. **Dimensionality Reduction**: Avoids the "curse of dimensionality" inherent in many high-dimensional tests

2. **Sensitivity**: Can detect various forms of non-normality:
   - Skewness
   - Multimodality
   - Non-linear dependencies
   - Heteroscedasticity

3. **Robustness**: Using many random projections provides a more complete picture than a single test

4. **Visualization**: The 3D representation offers intuitive understanding of the data structure

## Technical Implementation

The application combines several modern web technologies:
- **Three.js** for 3D visualization of projections and fitted ellipsoids
- **Chart.js** for histogram display of MSE distributions
- **PapaParse** for CSV handling and processing
- **Numeric.js** for linear algebra operations (eigendecomposition, matrix operations)
- **Tailwind CSS** for responsive, modern UI design

## Comparison with Traditional Multivariate Normality Tests

Traditional approaches to multivariate normality testing typically fall into these categories:

### 1. Multivariate Extensions of Univariate Tests

- **Mardia's Test**: Examines multivariate skewness and kurtosis
  - Computationally efficient but may miss certain types of non-normality
  - Performance degrades in high dimensions

- **Henze-Zirkler Test**: Based on a non-negative functional of the empirical characteristic function
  - More powerful than Mardia's test
  - Still struggles with high-dimensional data

- **Shapiro-Wilk Multivariate**: Extension of the univariate Shapiro-Wilk test
  - Good power for detecting departures from normality
  - Computationally expensive for large datasets

### 2. Graphical Methods

- **Q-Q Plots**: Comparing ordered squared Mahalanobis distances against chi-square quantiles
  - Visual but subjective
  - Difficult to interpret for very high-dimensional data

- **Scatter Plots of Principal Components**: Examining pairwise scatter plots of principal components
  - Can miss complex non-linear structures
  - Requires manual inspection of many plots for high-dimensional data

### 3. Energy-Based Tests

- **E-statistic Tests**: Based on energy distances between distributions
  - Powerful against various alternatives
  - Computationally intensive for large datasets

### Advantages of the Projection-Based Approach

Compared to these traditional methods, the 3D projection approach offers:

1. **Scalability to Higher Dimensions**: Operates effectively on data with hundreds of dimensions
2. **Visual Interpretability**: Provides an intuitive 3D visualization of the data structure
3. **Sensitivity to Various Departures**: Can detect many types of non-normality through multiple random projections
4. **Interactive Exploration**: Allows users to generate new projections to explore the data from different angles
5. **Comparative Analysis**: Direct comparison against a known multivariate normal reference
6. **Empirical Distribution**: Builds an empirical distribution of MSE values for more robust assessment

## Usage Instructions

### Requirements

- Modern web browser with WebGL support
- No server-side requirements (fully client-side)

### Getting Started

1. Open the HTML file in a web browser
2. Configure dimensions and sample sizes
3. Generate reference and test datasets (or upload your own CSV)
4. Run tests and compare distributions
5. Explore different projections with the "New Projection" button

### Data Upload Format

- CSV file with numeric data
- No headers
- Each row represents one observation
- Each column represents one dimension/variable

## Potential Extensions

This approach could be extended in several ways:

1. **Multiple Reference Distributions**: Compare against different parametric distributions
2. **Dimension Contribution Analysis**: Identify which dimensions contribute most to non-normality
3. **Alternative Geometry Fitting**: Explore non-ellipsoidal fitting methods for more complex distributions
4. **Projection Dimensionality**: Experiment with projections of different dimensionalities (2D, 4D+)
5. **Supervised Learning Integration**: Use projection MSE features for anomaly detection or classification
6. **Adaptive Sampling**: Focus testing on regions of the distribution that show potential non-normality

## References

- Liang, J., & Li, R. (2019). "A projection-based test for multivariate normality." *Computational Statistics & Data Analysis*, 131, 1-13.
- Szekely, G. J., & Rizzo, M. L. (2005). "A new test for multivariate normality." *Journal of Multivariate Analysis*, 93(1), 58-80.
- Mecklin, C. J., & Mundfrom, D. J. (2004). "An appraisal and bibliography of tests for multivariate normality." *International Statistical Review*, 72(1), 123-138.
- Mardia, K. V. (1970). "Measures of multivariate skewness and kurtosis with applications." *Biometrika*, 57(3), 519-530.

## License

MIT License
