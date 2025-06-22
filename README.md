# Phishing Email Classification App with Redis

This project demonstrates a phishing email classification application using machine learning. It includes four main components:

- **Model Training (`train.py`)**: Processes the dataset, trains a model using TF-IDF vectorization and logistic regression, and saves the trained model.
- **Model Validation (`validate.py`)**: Evaluates the saved model on a test dataset and outputs performance metrics such as accuracy, precision, and recall.
- **Model Serving (`serve.py`)**: Implements a FastAPI-based service to provide real-time phishing email predictions. Redis caching is used to optimize performance by speeding up repeated requests.

---


## Prerequisites

- Python 3.7+
- Pip


## Dataset

The dataset is sourced from [Kaggle](https://www.kaggle.com/datasets/subhajournal/phishingemails).

---

## Usage

### 1. Training the Model
Run the training script to process the dataset and generate the model file:
```bash
python train.py
```

### 2. Validating the Model
Run the validation script to evaluate the model's performance:
```bash
python validate.py
```

### 3. Serving Predictions
Ensure Redis is running (see instructions below for Windows), then start the FastAPI server:
```bash
python serve.py
```
Access the API at `http://localhost:8000` and send POST requests to the `/predict` endpoint with JSON payloads:
```json
{
  "text": "Your email content here..."
}
```

## API Usage

Send a POST request to `http://localhost:8000/predict` with the following JSON payload:
```bash
curl -X 'POST' \
  'http://localhost:8000/predict' \
  -H 'accept: application/json' \
  -H 'Content-Type: application/json' \
  -d '{
  "text": "todays floor meeting you may get a few pointed questions about today article about lays potential severance of $ 80 mm"
}'
```

The API responds with a JSON object containing:
- **`prediction`**: The predicted class name (e.g., "Phishing Email" or "Safe Email").
- **`probability`**: The confidence score of the prediction.

Example response:
```json
{
  "prediction": "Safe Email",
  "probability": 0.7791625553383463
}
```
