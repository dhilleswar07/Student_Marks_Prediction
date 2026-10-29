# Student Result Predictor

A Streamlit app that predicts whether a student is likely to **Pass** or **Fail** using study habits and background information. The app loads a trained Random Forest model and displays the prediction confidence.

## Features

- Collects weekly study hours, attendance, previous exam score, extracurricular participation, and home internet access (based on the model's input columns).
- Encodes categorical answers using the encoders saved with the model.
- Shows a Pass/Fail prediction, confidence score, and the inputs used.
- Caches the model bundle so it is loaded once per app session.

## Requirements

- Python 3.9 or newer
- The packages listed in `requirements.txt`
- A compatible `model.pkl` file in the project root

## Setup and run

1. Clone the repository and move into its directory:

   ```bash
   git clone https://github.com/dhilleswar07/Student_Marks_Prediction.git
   cd Student_Marks_Prediction
   ```

2. (Recommended) Create and activate a virtual environment:

   ```bash
   python -m venv .venv
   ```

   On Windows PowerShell:

   ```powershell
   .venv\Scripts\Activate.ps1
   ```

   On macOS or Linux:

   ```bash
   source .venv/bin/activate
   ```

3. Install dependencies:

   ```bash
   pip install -r requirements.txt
   ```

4. Ensure `model.pkl` is present in the project root, then start the app:

   ```bash
   streamlit run app.py
   ```

Streamlit will print a local URL to open in your browser.

## Model bundle

The app expects `model.pkl` to be a joblib-serialized dictionary with these keys:

| Key | Expected value |
| --- | --- |
| `model` | A fitted classifier supporting `predict` and `predict_proba` |
| `encoders` | A dictionary mapping categorical column names to fitted encoders with `classes_` and `transform` |
| `columns` | The ordered feature column names expected by the classifier |

The classifier must return the string labels `Pass` or `Fail` from `predict`. The categorical encoders' `classes_` values are shown as choices in the app. The app's friendly input settings include `study_hours`, `attendance_pct`, `previous_score`, `extra_curricular`, and `internet_access`; any additional columns use a default numeric input unless they have a saved encoder.

The model is loaded from the current project directory. Keep the model and app inputs aligned with the same training schema and preprocessing.

## Project files

```text
Student_Marks_Prediction/
├── app.py            # Streamlit user interface and prediction flow
├── model.pkl         # Trained model and categorical encoders (required)
├── requirements.txt  # Python dependencies
└── README.md
```

## Usage

Enter the requested student details and select **Predict Result**. The app shows the predicted result and the classifier's highest class probability as confidence. This is an educational demonstration and should not be treated as a definitive assessment of a student's ability or outcome.
