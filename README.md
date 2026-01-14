# Ferroelectricity-Analysis

## Project Description
Ferroelectricity is a material property wherein a material possesses a spontaneous nonzero electric dipole moment. This is valuable in many applications such as long-term information storage. In order to exhibit ferroelectricity, the crystal structure of a material must be noncentrosymmetric by Neumman's principle. This repository features a suite of functions designed to analyze the centrosymmetry properties of two-dimensional assemblies from coarse-grained molecular dynamics trajectories.

## Overview
The tools contained in this repository are designed to analyze molecular dynamics trajectories of model chromophores which tend to self-assemble into 2D sheets with a nearly rectangular lattice structure. The file 'ferro_cluster_statistics.py' contains functions designed to analyze these sheets. The main function for this is 'calc_centrosymmetry_props_3d'. Sheets are first detected via a hierarchical subspace DBSCAN clustering algorithm via the function . Chromophores are first clustered using a DBSCAN algorithm according to their orientation. These orientation-based clusters are then clustered with another round of DBSCAN based on chromophore position. To analyze the centrosymmetry properties of each sheet, we reduce the dimensionality of the clusters from 3D to 2D via the gyration tensor $\mathbf{S}$ which is defined as

$$S_{mn}=\frac{1}{N}\sum_{i=1}^Nr_m^{(i)}r_n^{(i)}$$

where $r_{n,m}^{(i)}$ are the $(m,n)$ components of vector $\vec{r}^{(i)}$ associated with chromophore $i$, $N$ is the number of chromophores in the sheet, and $m,n\in\{x,y,z\}$. Note that the set of positions $\vec{r}^{(i)}$ are equal to $\vec{r}^{(i,0)}-\vec{r}_c$ where $\vec{r}^{(i,0)}$ is the original vector and $\vec{r}_c$ is the center of mass of the sheet. We then compute the eigenvalues ($\lambda_1$, $\lambda_2$, $\lambda_3$) and eigenvectors ($\vec{u}_1$, $\vec{u}_2$, $\vec{u}_3$) of $\mathbf{S}$ where $\lambda_1\ge\lambda_2\ge\lambda_3$. For approximately planar data, our point cloud is spanned by $\vec{u}_1$ and $\vec{u}_2$. We can then map each point $\vec{r}_i$ to a new point $\vec{x}_i$ with two components (a_i=\vec{r}_i\cdot \vec{u}_1,b_i=\vec{r}_i\cdot \vec{u}_2). We note that this procedure is identical to principal component analysis with coordinate covariance matrix $\mathbf{S}$.

Centrosymmetries are calculated from the set of 2D coordinates $\{\vec{x}_i\}$ which are additionally normalized by interparticle distances in both principal directions. The local centrosymmetry parameter $P$ of each point is calculated as

$$P=\sum_{i=1,2}\left\lVert\vec{r}_i+\vec{r}\_{i+2}\right\rVert_2^2$$

where $\vec{r}_i$ $\vec{r}\_{i+2}$ are vectors between that point and pairs of opposing nearest neighbors. Greater values of $P$ correspond to greater amounts of local symmetry breaking and greater potential for ferroelectric behavior. 

Clearly, $P$ cannot be calculated for points on the boundaries of any clusters. These are detected and filtered out by measuring the sum of distances from each point to the 8 closest neighbors. Points with a sum greater than a cutoff are classified as edges and not considered in centrosymmetry analysis.

## Dependencies
A list of required packages can be found in 'requirements.txt'.
