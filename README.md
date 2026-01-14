# Ferroelectricity-Analysis

## Project Description
Ferroelectricity is a material property wherein a material possesses a spontaneous nonzero electric dipole moment. This is valuable in many applications such as long-term information storage. In order to exhibit ferroelectricity, the crystal structure of a material must be noncentrosymmetric by Neumman's principle. This repository features a suite of functions designed to analyze the centrosymmetry properties of two-dimensional assemblies from coarse-grained molecular dynamics trajectories.

## Overview
The tools contained in this repository are designed to analyze molecular dynamics trajectories of model chromophores which tend to self-assemble into 2D sheets. The file 'ferro_cluster_statistics.py' contains functions designed to analyze these sheets. The main function for this is 'calc_centrosymmetry_props_3d'. Sheets are first detected via a hierarchical subspace DBSCAN clustering algorithm via the function . Chromophores are first clustered using a DBSCAN algorithm according to their orientation. These orientation-based clusters are then clustered with another round of DBSCAN based on chromophore position. To analyze the centrosymmetry properties of each sheet, we reduce the dimensionality of the clusters from 3D to 2D via the gyration tensor $S$ which is defined as

$$S_{mn}=\frac{1}{N}\sum_{i=1}^Nr_m^{(i)}r_n^{(i)}$$

where $r_{n,m}^{(i)}$ are the $(m,n)$ components of vector $\vec{r}^{(i)}$ associated with chromophore $i$, $N$ is the number of chromophores in the sheet, and $m,n\in\{x,y,z\}$. Note that the set of positions $\vec{r}^{(i)}$ are equal to $\vec{r}^{(i,0)}-\vec{r}_{c}$ where we note that $\vec{r}_c$ is the center of mass of the sheet.

## Dependencies
A list of required packages can be found in 'requirements.txt'.
