Quantum Device Performance Classification: ML Analysis

Project Overview
  This project applies machine learning to a specialized dataset of 750 quantum electronic and spintronic devices. The goal is to classify whether a device "meets specifications" based on physical properties, material systems, and operational parameters.
Preprocessing Workflow
  To prepare the data for the KNN and Random Forest models, the following program was executed:
    Outlier Cleanup: Continuous variables (e.g., temperature_K, bias_voltage_V) were processed using an IQR-based function to cap values at lower and upper fences (1.5 * IQR).
    Label Encoding: Categorical columns like device_type and material_system were transformed into numerical format using LabelEncoder.
    Feature Scaling: All numerical columns were normalized using MinMaxScaler to ensure consistent weighting across different units (e.g., Kelvin vs. eV).
Results & Interpretations
  1. K-Nearest Neighbors (KNN)
    Optimal Configuration: An elbow method identified k=23 as the ideal neighbor count for maximum accuracy.
    Key Drivers: Features such as quantum_efficiency and bias_voltage_V were highly informative, as higher injection and efficiency naturally lead to improved device performance.
    Performance: The model achieved an accuracy of 90.22%.
  2. Random Forest
    Performance: Random Forest was the top-performing model with an accuracy of 92.44% and a Macro F1 score of 0.915.
    Advantage: This ensemble method likely handled the non-linear relationships between variables like bandgap_eV and spin_polarization more effectively than the distance-based KNN.
  3. PCA Visualization
    Dimensionality Reduction: PCA reduced the 18-feature dataset into two principal components (PC1 and PC2) for visualization.
    Cluster Analysis: The scatter plot shows how devices separate in a 2D space. The clusters actually represent the variance anomg Quantum Device Types. The spread along PC1 typically represents the feature with the highest variance (likely temperature_K or bias_voltage_V).
