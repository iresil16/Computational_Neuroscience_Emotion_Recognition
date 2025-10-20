# Computational Neuroscience: Emotion Recognition

**Author:** Irene Silvestro  
**Date:** July 2025  

This repository contains the code and analyses for the project *“Exploring fMRI Data for Emotion Recognition using Dynamic Functional Connectivity and Machine Learning”*.

The project focuses on leveraging fMRI data from the **NeuroEmo dataset** (OpenNeuro ds005700, v1.2.0) to explore brain dynamics underlying emotional responses to culturally relevant stimuli, specifically Indian Bollywood movie clips.



##  Project Overview

The primary objective of this work is to analyze **temporal and functional brain connectivity patterns** associated with different emotional states and to apply **machine learning models** for emotion recognition.

The workflow involves:

1. **Dataset Exploration**  
   - The NeuroEmo dataset contains fMRI recordings from **40 healthy participants** exposed to emotional movie clips.
   - Data acquisition: voxel size 1.8×1.8×4 mm, 36 slices, TR = 3 s, TE = 0.035 s, flip angle = 90°.
   - Task sequence includes 5 emotions (Calm, Afraid, Delighted, Excited, Depressed) interleaved with white noise.

2. **Preprocessing**  
   - Steps include motion correction, slice time correction, coregistration, spatial normalization, and smoothing.
   - Data reshaped from (128,128,36,200) to atlas space (52,62,52,200) using **Nilearn**.
   - Temporal splitting of fMRI data by emotion, concatenation of identical tasks, resulting in shapes (52,62,52,20) per emotion and (52,62,52,100) for all emotions or white noise.

3. **Functional Connectivity Analyses**  
   - **Seed-Based FC:** Regions of interest include *Amygdala*, *Insula*, and *Primary Visual Cortex*.  
   - Pearson correlation was used to compute voxel-wise FC, followed by group averaging.  
   - Independent t-tests compare Calm versus other emotions, with multiple comparison correction via FDR.  
   - FC maps visualized with color gradients: yellow-red for positive correlations, orange/purple for t-test significance.

4. **Dynamic Functional Connectivity (DFC)**  
   - Sliding-window approach with parameters: window size (`win_size`) and stride.  
   - Clustering performed on either full FC matrices or on leading eigenvectors.  
   - Optimal number of clusters (`k`) determined using **Silhouette** and **Davies-Bouldin** indices.  
   - Metrics calculated per state: Percentage of Occupancy (PO) and Lifetime (LF).  
   - Average transition matrices computed across subjects.

5. **Machine Learning for Emotion Classification**  
   - Eigenvectors from DFC used as features for training:  
     - Random Forest Classifier (RFC)  
     - Multilayer Perceptron (MLP)  
   - Dataset split: 70% training, 30% testing; features standardized to zero mean and unit variance.  
   - Model performance evaluated across different DFC parameters (`win_size` and `stride`).



##  Repository Structure

- `code/` – Python scripts and notebooks implementing preprocessing, FC/DFC analyses, and machine learning pipelines.  
   [Code repository](https://github.com/iresil16/Computational_Neuroscience_Emotion_Recognition/tree/main/code)  
- `data/` – Instructions to download the **NeuroEmo dataset** (OpenNeuro ds005700, v1.2.0).  
   [Dataset link](https://openneuro.org/datasets/ds005700/versions/1.2.0) 
- `figures/` – Example plots from FC and DFC analyses.


