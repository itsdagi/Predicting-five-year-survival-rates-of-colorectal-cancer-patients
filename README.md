# Colorectal Cancer Survival Predictor

This project predicts the five-year survival rates of colorectal cancer patients using a Random Forest machine learning model.

## Folder Structure

- `data/`: This directory contains the dataset used for training and evaluating the model.
  - `colorectal_cancer_dataset.csv`: The primary dataset file.
- `colorectal_cancer_predictor_model.ipynb`: The main Jupyter notebook containing all the Python code for data analysis, preprocessing, model training, and evaluation.
- `best_random_forest_model.joblib`: The saved, trained Random Forest model. This file is generated after running the Jupyter notebook.
- `README.md`: This file, providing an overview and instructions for the project.

## What the Code Does

The Jupyter notebook `colorectal_cancer_predictor_model.ipynb` implements a machine learning pipeline to predict the five-year survival rates of colorectal cancer patients. The key steps are:

1.  **Data Loading and Initial Exploration**:
    *   Loads the dataset from `data/colorectal_cancer_dataset.csv` using pandas.
    *   Performs initial checks like viewing the first few rows, column names, and checking for missing values.

2.  **Data Preprocessing**:
    *   Handles missing values by filling numeric columns with the median and categorical columns with the mode.
    *   Drops identifier columns and other non-predictive features (e.g., `Patient_ID`, `Survival_Prediction`, `Mortality`).
    *   Performs one-hot encoding for categorical features to convert them into a numerical format suitable for machine learning models. This includes features like `Country`, `Gender`, `Cancer_Stage`, etc.

3.  **Feature Selection and Target Variable Definition**:
    *   Defines the feature matrix `X` (independent variables) using the preprocessed data.
    *   Defines the target variable `y` (dependent variable), which is `Survival_5_years_Yes` (indicating whether the patient survived for 5 years).

4.  **Data Splitting**:
    *   Splits the dataset into training and testing sets (e.g., 80% training, 20% testing) using `train_test_split` from scikit-learn to evaluate model performance on unseen data.

5.  **Model Training**:
    *   Trains a Random Forest classifier using `RandomForestClassifier` from scikit-learn on the training data.

6.  **Model Evaluation**:
    *   Evaluates the trained model on the test set.
    *   Calculates and prints performance metrics such as accuracy and a detailed classification report (including precision, recall, and F1-score for each class).

7.  **Addressing Class Imbalance**:
    *   The notebook explores techniques to handle class imbalance in the target variable:
        *   **Class Weighting**: Retrains the Random Forest model with `class_weight='balanced'` to give more importance to the minority class.
        *   **Oversampling**: Uses `RandomOverSampler` from the `imbalanced-learn` library to oversample the minority class in the training set.

8.  **Hyperparameter Tuning**:
    *   Employs `GridSearchCV` from scikit-learn to perform an exhaustive search over a specified parameter grid for the Random Forest model.
    *   This helps in finding the optimal hyperparameters (e.g., `n_estimators`, `max_depth`, `min_samples_split`, `min_samples_leaf`, `class_weight`) based on F1-score and cross-validation.

9.  **Feature Importance Analysis**:
    *   Visualizes the feature importances derived from the best Random Forest model using `matplotlib`. This helps in understanding which features are most influential in predicting survival rates.

10. **Saving the Model**:
    *   Saves the best-trained model (obtained from GridSearchCV) to disk as `best_random_forest_model.joblib` using `joblib`. This allows for later use without retraining.

11. **Prediction on New Data (Example)**:
    *   Includes an example of how to load the saved model and make predictions on new (dummy) patient data, ensuring the new data is preprocessed in the same way as the training data.

## How to Implement the Code Locally

To run the colorectal cancer survival prediction model on your local machine, follow these steps:

### 1. Prerequisites/Dependencies

Ensure you have the following installed:

*   **Python 3.x**: The code is written in Python.
*   **pandas**: For data manipulation and analysis.
*   **scikit-learn**: For machine learning tasks (Random Forest, train-test split, evaluation metrics, GridSearchCV).
*   **matplotlib**: For plotting feature importances.
*   **imbalanced-learn**: For handling class imbalance (specifically `RandomOverSampler`).
*   **joblib**: For saving and loading the trained model.
*   **Jupyter Notebook or JupyterLab**: To open and run the `.ipynb` file.

### 2. Installation

You can install the necessary Python libraries using pip. It's recommended to use a virtual environment.

```bash
# Create and activate a virtual environment (optional but recommended)
python -m venv cancer_predictor_env
# On Windows:
# cancer_predictor_env\Scripts\activate
# On macOS/Linux:
# source cancer_predictor_env/bin/activate

# Install the required packages
pip install pandas scikit-learn matplotlib imbalanced-learn joblib jupyter
```

### 3. Running the Code

1.  **Clone the Repository (if applicable)**:
    If this project is in a Git repository, clone it to your local machine.
    ```bash
    # git clone <repository-url>
    # cd <repository-directory>
    ```

2.  **Ensure Dataset is Present**:
    *   Place the `colorectal_cancer_dataset.csv` file inside the `data/` directory in the project's root folder.

3.  **Launch Jupyter Notebook/Lab**:
    *   Navigate to the project's root directory in your terminal.
    *   Launch Jupyter Notebook or JupyterLab:
        ```bash
        jupyter notebook
        # or
        # jupyter lab
        ```
    *   This will open a new tab in your web browser.

4.  **Open and Run the Notebook**:
    *   In the Jupyter interface, navigate to and open the `colorectal_cancer_predictor_model.ipynb` file.
    *   You can run the cells sequentially by selecting a cell and pressing `Shift + Enter` or by using the "Run" menu.
    *   Running the notebook will perform all steps from data loading to model training, evaluation, and saving the best model as `best_random_forest_model.joblib`.

### 4. Using the Saved Model for Predictions

Once the notebook has been run and the `best_random_forest_model.joblib` file is generated, you can use it to make predictions on new data. The notebook itself contains an example of how to:
*   Load the saved model using `joblib.load()`.
*   Prepare new patient data in the same format (including one-hot encoding) as the training data.
*   Use the loaded model to predict survival.
