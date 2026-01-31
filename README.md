# Customer Churn Prediction with CI/CD Pipeline

Automated Machine Learning pipeline for customer churn prediction using GitHub Actions and CML (Continuous Machine Learning).

## Project Overview

This project demonstrates a complete CI/CD workflow for a Machine Learning model that predicts customer churn using a Random Forest classifier. The pipeline automatically trains the model, evaluates performance, and publishes results on every code change.

## Dataset

The project uses a banking customer dataset (`dataset.csv`) with features including:
- Customer demographics (Age, Gender, Geography)
- Account information (Credit Score, Balance, Estimated Salary)
- Banking behavior (Number of Products, Has Credit Card, Is Active Member)
- Target variable: Customer churn (Exited)

## Model Approaches

The pipeline trains and compares three Random Forest models with different strategies for handling imbalanced data:

1. **Without Imbalance Handling**: Baseline model without any balancing technique
2. **With Class Weights**: Uses weighted classes to give more importance to minority class
3. **With SMOTE**: Applies Synthetic Minority Over-sampling Technique for data augmentation

## Project Structure
```
churn-cml-dvc/
├── .github/
│   └── workflows/
│       └── cml-churn.yaml      # CI/CD pipeline configuration
├── dataset.csv                 # Training data
├── script.py                   # ML training script
├── requirements.txt            # Python dependencies
└── README.md                   # This file
```

## Files Description

### script.py
Main training script that:
- Loads and preprocesses the dataset
- Handles missing values and categorical encoding
- Implements three balancing strategies
- Trains Random Forest models
- Generates evaluation metrics and confusion matrices
- Outputs results to `metrics.txt` and `conf_matrix.png`

### requirements.txt
Python dependencies including:
- scikit-learn: Machine learning algorithms
- imbalanced-learn: SMOTE implementation
- pandas: Data manipulation
- matplotlib & seaborn: Visualization
- sklearn-features: Custom transformers

### .github/workflows/cml-churn.yaml
GitHub Actions workflow that:
- Triggers on every push to the repository
- Sets up Python 3.11 environment
- Installs dependencies
- Executes training script
- Publishes results automatically using CML

## CI/CD Pipeline

The automated pipeline performs the following steps:

1. **Environment Setup**: Install Python 3.11, Node.js, and CML
2. **Dependency Installation**: Install required Python packages
3. **Model Training**: Execute script.py to train all three models
4. **Results Generation**: Create metrics.txt and conf_matrix.png
5. **Automated Reporting**: Post results as GitHub comment via CML

## How It Works

Every time code is pushed to the repository:
- GitHub Actions automatically starts the workflow
- The ML model is trained with latest code/data
- Performance metrics are calculated
- A comment is posted on the commit with:
  - F1-scores for training and validation
  - Confusion matrices for all three approaches
  - Visual comparison of model performance

## Results

The pipeline automatically reports:
- F1-score for training and validation sets
- Confusion matrices showing prediction accuracy
- Comparison between the three balancing strategies

Example output:
```
RandomForestClassifier without-imbalance
F1-score of Training: 68.60%
F1-score of Validation: 56.56%

RandomForestClassifier with-class-weights
F1-score of Training: 78.97%
F1-score of Validation: 63.08%

RandomForestClassifier with-SMOTE
F1-score of Training: 88.15%
F1-score of Validation: 60.53%
```

## Local Setup

To run the project locally:

1. Clone the repository:
```bash
git clone https://github.com/hannhm1109/churn-cml-dvc.git
cd churn-cml-dvc
```

2. Create virtual environment:
```bash
python -m venv venv
source venv/bin/activate  # On Windows: venv\Scripts\activate
```

3. Install dependencies:
```bash
pip install -r requirements.txt
```

4. Run training:
```bash
python script.py
```

5. View results:
- Metrics: `cat metrics.txt`
- Confusion matrix: Open `conf_matrix.png`

## Technologies Used

- **Python 3.11**: Programming language
- **scikit-learn**: Machine learning library
- **imbalanced-learn**: Handling imbalanced datasets
- **GitHub Actions**: CI/CD automation
- **CML**: Continuous Machine Learning reporting
- **pandas**: Data manipulation
- **matplotlib & seaborn**: Data visualization

## Key Features

- Fully automated ML pipeline
- Automatic model training on code changes
- Instant performance feedback via GitHub comments
- Comparison of multiple balancing strategies
- Reproducible experiments with fixed random seeds
- Visual performance reporting with confusion matrices

## Performance Metrics

Models are evaluated using:
- F1-score (harmonic mean of precision and recall)
- Confusion matrices (visual representation of predictions)
- Training vs validation performance comparison

## Future Improvements

Potential enhancements:
- Model versioning with DVC
- Hyperparameter tuning automation
- Model deployment pipeline
- A/B testing framework
- Feature importance analysis
- Cross-validation integration

## Author

Hanane Nahim


## Acknowledgments

- Professor: Pr. Soufiane HAMIDA
- Course: DevOps & MLOps
- Institution: ENSET Mohammedia
