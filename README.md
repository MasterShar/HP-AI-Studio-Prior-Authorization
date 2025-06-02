
# Prior Authorization Approval Prediction

This project builds and trains machine learning models to predict the approval rate of health plan prior authorization requests. It uses real-world structured data, applies preprocessing, trains a PyTorch-based neural network, and logs results using MLflow.

---

## Dataset

The dataset is named:

```
Health_Plan_Prior_Authorization_Data_20250505 for Hackathon.csv
```

It includes features such as:

- Carrier
- Service category
- Request
- Code type
- Number of requests per code
- Approval rate (target)

---

## Environment Requirements

This code is designed to run inside the HP AI Studio Deep Learning image and does not require external libraries or internet access.

- Python 3.12+
- `pandas`, `numpy`, `scikit-learn`
- `matplotlib`, `seaborn`
- `torch`
- `mlflow`

---

## Workflow Overview

1. Load & Clean Data
2. Encode categorical business variables
3. Standardize features
4. Train/test split
5. Train a PyTorch regression model
6. Log results with MLflow
7. Evaluate model performance (MSE, R²)

---

## Model Architecture

The PyTorch model is a simple feedforward network:

```python
TabularNN(
  Linear(input_dim, 64) → ReLU
  Linear(64, 32) → ReLU
  Linear(32, 1)
)
```

- Loss Function: Mean Squared Error (MSE)
- Optimizer: Adam (lr=0.001)
- Epochs: 100

---

## Evaluation Metrics

The model reports:
- `Mean Squared Error (MSE)`
- `R² Score`

These are logged via MLflow along with the model artifact.

---

## MLflow Integration

MLflow is used for:

- Logging hyperparameters and metrics
- Saving the trained model (`mlflow.pytorch.log_model`)
- Tracking experiments under the name:
  ```
  prior_auth_approval_pytorch
  ```

---

## Next Steps

- Export model for external API deployment (e.g. FastAPI)
- Integrate Swagger UI for REST prediction endpoint (outside AI Studio)
- Add early stopping or learning rate scheduling
- Expand the model to classification for categorical outcomes
