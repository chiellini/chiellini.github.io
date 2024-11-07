---
title: "Robust integrated intracellular organization of the human iPS cell: where, how much, and how variable?"
subtitle: "Paper reading"
layout: post
author: "zelin"
header-style: text
catalog: true
tags:
  - Paper reading
---

REFERENCE:


https://doi.org/10.1101/2020.12.08.415562

https://1drv.ms/b/s!Ath3f5ykGji3mi8xidQEgV1zLX-W?e=FSwVfm

# Abstract

* benchmark 基準
* cell-to-cell variation
  * locations, amounts, and variation of the 25 cellular structures.
* stereotypy: a structure's individual location varied
* concordance: the structure localized relative to all the other cellular structures

# Introduction

* sub cellular components and processes in space
* four orders of magnitude.
* global cell behaviors:
  * protrusion 突出物 of a cell front
  * retraction of a rear during cell migration
* daunting 令人退縮的 immensely complex 及其複雜的
* enormously 巨大的
* quest 尋求
* This baseline should represent the typical, or mean, cell within the population(種群), as well as the full range of normal variation of the population itself.
* unprecedented 前所未有的
* a fundamental benchmark for comparision with future analyses of cell shape and cell organization for cells in different states.

# Result

* quality control workflows to create the Allen Cell Collection
* organelles 細胞器(包括綫粒體葉綠體什麽的)
* cellular structures
* compartments 間隔
* consistently 始終如一的

* nucleoli DFC 致密纤维组分, the dense fibrillar component
* nucleoli GC   the granular component
* nuclear speckles

* cohesin 粘连蛋白
* histones 
* nuclear envelope 细胞膜
* nuclear pores
* ...

# Methodology P33

## registration
* centroids 形心
* preserving
  * the biologically relevant, apical-basal（以顶点为基准的） axis (顶点的那个z轴危中心)
  * the longest axis of the cell perpendicular(垂直的 ) to that axis

## SHE -> SHAPE SPACE MAP P11 (RED PLACE） 

* A method to "morph" all of the locations of all of the points within a cell into the idealized reconstructed cell shape the best represents the cell shape.


## QUANTIFICATION AND STATISTICAL ANALYSIS P48

## Building the cell and nuclear shape space P54
**identifying the primary modes of shape variation**


**I didn't understand the PCA usages, I can not get the real PCA for every cell. 24-2-2021 The following fucking mapping methods are derived by my self, but I cannot get the real inverse, the result SHcPCA are so weired.**
* SHE + PCA 
  * you know what is PCA right?
  * PCA +- delta depend on the shape space map distribution
  * Probability density distribution of principal component values
  * see picture1 in experiment section

# Explanation
* MAXIMUM POINT IN PCA ( SHAPE SPACE) TO DO CLUSTERING

# Experiment
* correlation between original image and reconstruction image
  * reconstruction use nearest neighbor interpolation
  * step by step, voxel by voxel ( not regular filling)
* correlation
  * voxelwise pearson correlation between original image and recontruction image
* choose max point, shape model and shape space build:
![picture1](https://github.com/chiellini/pictures_sources/raw/master/67a8ca204afdfda315f6d2053792e31.png)
  * **shape model 6**
  * As an example, the bin corresponding to the map point (0,0,0,0,0,-1.5σ,0,0) is highlighted in blue.

## see suplementary materials(picture resources):
https://www.biorxiv.org/content/10.1101/2020.12.08.415562v1.supplementary-material


# ANALYSIS
## PCA shape
1. in this dataset, the total height of the cell is largely independent of its overall volume. (supported or to support 'Statistical Analysis of ')

# conclusion
* 

# NEED TO KNOW
* 