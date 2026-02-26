# Quantum Device Machine Learning Performance Classification: An Integration of KNN and Random Forest Models

## Project Overview

In this project, 750 quantum electronic and spintronic devices are used as a specific dataset for machine learning model performance. Using physical characteristics, material systems, and operational parameters, the objective is to classify whether a device **meets specifications (Class 1)** or is **non-compliant (Class 0)**.

## Data Preprocessing Workflow
  ### To prepare the data for the KNN and Random Forest models, the following program was executed:
  - **Outlier Cleanup:** Continuous variables (e.g., `temperature_K`, `bias_voltage_V`) were processed using an IQR-based function to limit values at lower and upper fences *(1.5 * IQR)*.
  - **Label Encoding:** Categorical columns like `device_type` and `material_system` were transformed into numerical format using `LabelEncoder`.
  - **Feature Scaling:** All numerical columns were normalized using `MinMaxScaler` to ensure consistent weighting across different units (e.g., Kelvin vs. eV).

## Results & Interpretations
  ### 1. K-Nearest Neighbors (KNN)
  - **Optimal Configuration:** The optimal neighbor count of **k=23** was determined using both the automatic `GridSearchCV` and the visual Elbow Method. The maximum prediction accuracy while maintaining strong generalization is confirmed by this combination at **k=23**.
  - **Tuning Parameters:** To ensure that closer physical parameters in the feature space had a relatively greater impact on the classification, the model was further optimized using Manhattan distance and distance-based weighting.
  - **Key Drivers:** Features such as `quantum_efficiency` and `bias_voltage_V` were highly informative, as higher injection and efficiency naturally lead to enhanced device performance.
  - **Performance:** Following the `StandardScaler` application and hyperparameter tuning, the model achieved an **accuracy of 90.67%** and a **F1 score of 0.8939**.
    
  <img width="863" height="555" alt="download" src="https://github.com/user-attachments/assets/c344034e-a2a2-475e-be2c-9f6fba821f54" />


  ### 2. Random Forest
  - **Performance:** Random Forest was the top-performing model with an **accuracy of 92.44%** and a **Macro F1 score of 0.9153**.
  - **Advantage:** This ensemble method likely handled the non-linear relationships between variables like `bandgap_eV` and `spin_polarization` more effectively than the distance-based KNN.

  <img width="320" height="100" alt="image" src="https://github.com/user-attachments/assets/9fe385a9-0b9d-42e0-abb9-60fbf8b0be08" />


  ### 3. PCA (Principal Component Analysis) Visualization
  - **Dimensionality Reduction:** To visualize complex device relationships, 18 high-dimensional physical properties have been divided into two Principal Components (PC1 and PC2).
  - **Cluster Analysis:** Based on fundamental physical characteristics, the figure shows natural clusters. The difference between visible and infrared light emitters is one example of how different quantum device types and material systems are represented in this separation. The experimental variables such as `temperature_K` and `bias_voltage_V` significantly influence the primary variance (PC1).
  - **Impact of Standardization:** The use of `StandardScaler` was essential to reduce unit-scale bias, which made it possible to differentiate clusters more clearly and determine the main physical causes of device variance.
    
  <img width="671" height="547" alt="download" src="https://github.com/user-attachments/assets/cbebae55-f4d5-4cdd-b559-4c57eb8937c7" />


  ### Key Decision: 
  - Both models are highly reliable for identifying **Class 0** (non-compliant) devices, with exactly **141 True Negatives** each.
