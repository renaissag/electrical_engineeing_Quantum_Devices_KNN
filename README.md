# Quantum Device Machine Learning Performance Classification: An Integration of KNN and Random Forest Models

## Project Overview

In this project, 750 quantum electronic and spintronic devices are used as a specific dataset for machine learning. Using physical characteristics, material systems, and operational parameters, the objective is to categorize if a device "meets specifications".

## Data Preprocessing Workflow
  ### To prepare the data for the KNN and Random Forest models, the following program was executed:
  - **Outlier Cleanup:** Continuous variables (e.g., `temperature_K`, `bias_voltage_V`) were processed using an IQR-based function to cap values at lower and upper fences *(1.5 * IQR)*.
  - **Label Encoding:** Categorical columns like `device_type` and `material_system` were transformed into numerical format using `LabelEncoder`.
  - **Feature Scaling:** All numerical columns were normalized using `MinMaxScaler` to ensure consistent weighting across different units (e.g., Kelvin vs. eV).

## Results & Interpretations
  ### 1. K-Nearest Neighbors (KNN)
  - **Optimal Configuration:** An elbow method identified **k=23** as the ideal neighbor count for maximum accuracy.
  - **Key Drivers:** Features such as `quantum_efficiency` and `bias_voltage_V` were highly informative, as higher injection and efficiency naturally lead to enhanced device performance.
  - **Performance:** The model achieved an **accuracy of 90.22%** and a **F1 score of 88.85%**.

  <img width="965" height="658" alt="image" src="https://github.com/user-attachments/assets/7d89cf0a-701a-492f-b8d6-8fad6bcd73a3" />


  ### 2. Random Forest
  - **Performance:** Random Forest was the top-performing model with an **accuracy of 92.44%** and a **Macro F1 score of 0.915**.
  - **Advantage:** This ensemble method likely handled the non-linear relationships between variables like `bandgap_eV` and `spin_polarization` more effectively than the distance-based KNN.

  <img width="320" height="107" alt="image" src="https://github.com/user-attachments/assets/e2eff42d-9e9a-4a3c-a2a1-622a527b6cc0" />


  ### 3. PCA (Principal Component Analysis) Visualization
  - **Dimensionality Reduction:** PCA reduced the high-dimensional feature set of 18 columns into two principal components (PC1 and PC2) for visualization.
  - **Cluster Analysis:** The PCA scatter plot displays how various quantum devices divide into "classes" according to their fundamental physical characteristics. This determines the main causes of variations in device performance, including the difference between emitters of visible and infrared light. The clusters actually represent the variance anomg quantum device types. The spread along PC1 typically represents the feature with the highest variance (likely `temperature_K` or `bias_voltage_V`).

  <img width="684" height="547" alt="image" src="https://github.com/user-attachments/assets/c646e598-f00f-4961-af4d-65400a2ae73d" />

