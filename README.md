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
  - **Performance:** The model achieved an **accuracy of 90.67%** and a **F1 score of 89.39%**.
    
  <img width="863" height="555" alt="download" src="https://github.com/user-attachments/assets/c344034e-a2a2-475e-be2c-9f6fba821f54" />


  ### 2. Random Forest
  - **Performance:** Random Forest was the top-performing model with an **accuracy of 92.44%** and a **Macro F1 score of 91.53%**.
  - **Advantage:** This ensemble method likely handled the non-linear relationships between variables like `bandgap_eV` and `spin_polarization` more effectively than the distance-based KNN.

    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }


  
    
      
      Model
      Accuracy
      Macro F1
    
  
  
    
      0
      KNN
      0.906667
      0.893918
    
    
      1
      Random Forest
      0.924444
      0.915281
    
  


    

  
    

  
    
  
    

  
    .colab-df-container {
      display:flex;
      gap: 12px;
    }

    .colab-df-convert {
      background-color: #E8F0FE;
      border: none;
      border-radius: 50%;
      cursor: pointer;
      display: none;
      fill: #1967D2;
      height: 32px;
      padding: 0 0 0 0;
      width: 32px;
    }

    .colab-df-convert:hover {
      background-color: #E2EBFA;
      box-shadow: 0px 1px 2px rgba(60, 64, 67, 0.3), 0px 1px 3px 1px rgba(60, 64, 67, 0.15);
      fill: #174EA6;
    }

    .colab-df-buttons div {
      margin-bottom: 4px;
    }

    [theme=dark] .colab-df-convert {
      background-color: #3B4455;
      fill: #D2E3FC;
    }

    [theme=dark] .colab-df-convert:hover {
      background-color: #434B5C;
      box-shadow: 0px 1px 3px 1px rgba(0, 0, 0, 0.15);
      filter: drop-shadow(0px 1px 2px rgba(0, 0, 0, 0.3));
      fill: #FFFFFF;
    }
  

    
      const buttonEl =
        document.querySelector('#df-4478d2cb-891b-415a-91b8-527d180a9193 button.colab-df-convert');
      buttonEl.style.display =
        google.colab.kernel.accessAllowed ? 'block' : 'none';

      async function convertToInteractive(key) {
        const element = document.querySelector('#df-4478d2cb-891b-415a-91b8-527d180a9193');
        const dataTable =
          await google.colab.kernel.invokeFunction('convertToInteractive',
                                                    [key], {});
        if (!dataTable) return;

        const docLinkHtml = 'Like what you see? Visit the ' +
          '<a target="_blank" href=https://colab.research.google.com/notebooks/data_table.ipynb>data table notebook</a>'
          + ' to learn more about interactive tables.';
        element.innerHTML = '';
        dataTable['output_type'] = 'display_data';
        await google.colab.output.renderOutput(dataTable, element);
        const docLink = document.createElement('div');
        docLink.innerHTML = docLinkHtml;
        element.appendChild(docLink);
      }
    
  
  ### 3. PCA (Principal Component Analysis) Visualization
  - **Dimensionality Reduction:** To visualize complex device relationships, 18 high-dimensional physical properties have been divided into two Principal Components (PC1 and PC2).
  - **Cluster Analysis:** Based on fundamental physical characteristics, the figure shows natural clusters. The difference between visible and infrared light emitters is one example of how different quantum device types and material systems are represented in this separation. The experimental variables such as `temperature_K` and `bias_voltage_V` significantly influence the primary variance (PC1).
  - **Impact of Standardization:** The use of `StandardScaler` was essential because it reduced unit-scale bias, which made it possible to differentiate clusters more clearly and determine the main physical causes of device variance.
    
  <img width="671" height="547" alt="download" src="https://github.com/user-attachments/assets/cbebae55-f4d5-4cdd-b559-4c57eb8937c7" />

