# Titanic-ML-project
This repository contains my ML project on the Titanic dataset that uses two approaches (With and without pipeline) to predict the passengers' chances of survival. 

# Titanic Survival Prediction

This repository contains two approaches to predicting Titanic passengers' survival probabilities using a Decision Tree Classifier. The primary focus is to demonstrate the difference between using pipelines and manually handling preprocessing, fitting, and prediction steps. Both approaches yield the same outcome but differ significantly in terms of code organization, maintainability, and production readiness.

---

## **Project Structure**

### Files:
1. **Test_with_pipeline.ipynb**
    - This notebook demonstrates the prediction process using a pipeline.
    - The pipeline encapsulates all preprocessing and model-fitting steps into a single object that can be saved as a pickle file.

2. **Test_without_pipeline.ipynb**
    - This notebook demonstrates the prediction process without using a pipeline.
    - Three separate pickle files are used: two files for encoding, and one for the trained Decision Tree model. There was also an imputer object (Simple Imputer) but that wasn't exported as a pickle file since we were inputting a custom array ourselves and were not missing any values.

3. **Model_with_pipeline and Model_without_pipeline.ipynb**
   - Two notebooks containing the code for the ML model using the pipeline and without pipeline approach.

4. **Pipeline.pickle**
    - A pickle file containing the entire pipeline (preprocessing, model training, and prediction steps).

5. **oe_embakred and oe_gender.pickle**
    - Pickle files for feature one hot encoding.

6. **clf.pickle**
    - A pickle file for the trained Decision Tree Classifier.

---

## **Pipeline vs. Non-Pipeline Approach**

### **Pipeline Approach**
In the pipeline approach, all steps—including data preprocessing, scaling, and model training—are encapsulated in a single object. The pipeline can be saved as a pickle file and reused for predictions without repeating intermediate steps.

#### **Advantages:**
- **Code Simplicity:** Reduces boilerplate code by encapsulating multiple steps into one.
- **Reusability:** A single object can be used for training, validation, and prediction.
- **Production Readiness:** Ideal for deploying models to production, as the same pipeline ensures consistent preprocessing and predictions.
- **Maintainability:** Easier to modify and debug due to centralized control.

#### **Disadvantages:**
- **Black Box:** The encapsulated steps might be harder to interpret individually.
- **Limited Flexibility:** Custom intermediate outputs (e.g., transformed data) are less accessible unless explicitly exposed.

### **Non-Pipeline Approach**
In this approach, preprocessing, scaling, and model fitting are handled separately. Each component is saved as an independent pickle file and must be loaded individually for predictions.

#### **Advantages:**
- **Transparency:** Each step is explicitly handled, making the process easier to understand.
- **Flexibility:** Intermediate results can be accessed and modified independently.

#### **Disadvantages:**
- **Code Complexity:** Requires more code to manage each step individually.
- **Error-Prone:** Inconsistent preprocessing steps between training and prediction stages can lead to errors.
- **Harder to Deploy:** Requires careful orchestration of multiple components, making production deployment more challenging.

---

## **How to Use**

### Pipeline Approach
1. Load the pipeline using pickle:
   ```python
   import pickle

   with open('Pipeline.pickle', 'rb') as f:
       pipeline = pickle.load(f)
   ```
2. Make predictions using .predict on your dataset or custom array:
   ```python
   predictions = pipeline.predict(new_data)
   ```

### Non-Pipeline Approach
1. Load each component using pickle:
   ```python
   with open('Preprocessing.pickle', 'rb') as f:
       preprocessing = pickle.load(f)

   with open('Scaler.pickle', 'rb') as f:
       scaler = pickle.load(f)

   with open('Model.pickle', 'rb') as f:
       model = pickle.load(f)
   ```
2. Apply preprocessing,scaling and encoding again on the provided test data/custom array:
   ```python
   preprocessed_data = preprocessing.transform(new_data)
   scaled_data = scaler.transform(preprocessed_data)
   ```
3. Make predictions:
   ```python
   predictions = model.predict(scaled_data)
   ```

---

## **Key Insights**
- Pipelines significantly simplify the machine learning workflow, especially in production environments.
- However, for learning purposes or exploratory analysis, separating steps can provide greater clarity.

---

## **Conclusion**
This project demonstrates the importance of pipelines in reducing code complexity and ensuring reproducibility. Both approaches are valid and can be chosen based on the use case. Pipelines are generally recommended for production, while manual steps may be more suitable for educational or experimental contexts.

The accuracy achieved by our model using the accuracy_score metric from scikit learn was around 70%.


