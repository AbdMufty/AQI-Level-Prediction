# Air Quality Index (AQI) Prediction Using Machine Learning

> A machine learning project that predicts air-quality categories from pollutant measurements and weather data, and compares multiple classification algorithms.

## Problem & Users

### Problem
Air pollution affects public health, but interpreting daily pollutant measurements can be difficult. This project explores whether air-quality measurements and meteorological variables can be used to classify daily Air Quality Index (AQI) levels.

### Intended Users
- Students learning data science and machine learning.
- Researchers exploring air-quality and weather data.
- Developers interested in environmental data analysis.

This project is for educational and exploratory use. It is not an official air-quality monitoring or public-health warning system.

## Features / Solution

- Combines daily AQI records with historical weather observations.
- Cleans and prepares data, including handling missing values.
- Explores data distributions and relationships using plots.
- Selects numeric features using correlation with the AQI value.
- Converts numeric AQI values into six categories:
  - Good
  - Moderate
  - Unhealthy for sensitive groups
  - Unhealthy
  - Very Unhealthy
  - Hazardous
- Scales features and addresses class imbalance using SMOTE or random oversampling.
- Trains and compares several classification models.
- Evaluates models with accuracy, precision, recall, F1-score, confusion matrices, cross-validation, learning curves, and training/prediction time.
- Demonstrates a prediction for a new set of pollutant and weather measurements.

## Architecture

The project is implemented as a Jupyter Notebook and follows this workflow:

1. **Load data:** Read daily AQI CSV files and retrieve historical weather data.
2. **Merge records:** Join AQI and weather observations by date.
3. **Clean data:** Remove unused columns and handle missing values.
4. **Explore and select features:** Inspect distributions and correlations, then select numeric variables associated with the AQI value.
5. **Create labels:** Convert the numeric AQI value into an AQI category.
6. **Prepare the dataset:** Encode the labels, scale input features, and split the data into training and test sets.
7. **Balance training classes:** Apply SMOTE or random oversampling to the training data.
8. **Train models:** Compare Logistic Regression, Random Forest, Support Vector Machine (SVM), K-Nearest Neighbors (KNN), Decision Tree, Gradient Boosting, CatBoost, and a Stacking Classifier.
9. **Evaluate:** Compare classification metrics and visualize results.
10. **Predict:** Use a trained model to classify a new observation.

### Technology Stack

- **Language:** Python
- **Notebook environment:** Jupyter Notebook
- **Data processing:** Pandas, NumPy
- **Visualization:** Matplotlib, Seaborn, Plotly
- **Machine learning:** Scikit-learn
- **Class balancing:** imbalanced-learn
- **Gradient boosting:** CatBoost
- **Weather data:** Meteostat
- **Version control:** Git and GitHub

## Prerequisites

- Python 3.10 or a compatible Python version
- Jupyter Notebook or JupyterLab
- Internet access to retrieve historical weather data through Meteostat
- The AQI CSV files expected by the notebook (see [Data / Model](#data--model-for-ai-projects))

## Installation

1. Clone this repository:

   ```bash
   git clone https://github.com/YOUR_USERNAME/aqi-prediction.git
   cd aqi-prediction
   ```

2. Create and activate a virtual environment.

   **Windows (PowerShell):**
   ```powershell
   python -m venv .venv
   .venv\Scripts\Activate.ps1
   ```

   **macOS / Linux:**
   ```bash
   python -m venv .venv
   source .venv/bin/activate
   ```

3. Install the main dependencies:

   ```bash
   python -m pip install --upgrade pip
   pip install numpy pandas matplotlib seaborn plotly tabulate meteostat scikit-learn imbalanced-learn catboost jupyter
   ```

4. Put the required AQI CSV files in the same directory as the notebook, unless you update the file paths in the notebook.

5. Launch Jupyter:

   ```bash
   jupyter notebook
   ```

6. Open `AQI Prediction .ipynb`.

## Quick Start / Usage

The notebook expects the following AQI files for the Pittsburgh analysis:

```text
aqidaily2017.csv
aqidaily2018.csv
aqidaily2019.csv
aqidaily2020.csv
aqidaily2021.csv
aqidaily2022.csv
aqidaily2023.csv
```

A later section also expects these files for the Bakersfield, California analysis:

```text
aqidaily16.csv
aqidaily17.csv
aqidaily18.csv
aqidaily19.csv
```

After placing the files in the expected location:

1. Start Jupyter Notebook.
2. Open `AQI Prediction .ipynb`.
3. Run the cells in order from top to bottom.
4. Review the visualizations, model evaluation metrics, and example prediction.

The notebook retrieves historical weather observations for Pittsburgh, Pennsylvania, and later for Bakersfield, California, using Meteostat. Internet access and availability of weather records are therefore required for those cells.

**Important:** The notebook depends on external CSV files that are not included with the notebook upload. The workflow will not run end-to-end until the required datasets are obtained and their filenames and columns match the notebook's expectations.

## Example Output

The notebook is designed to produce:

- AQI and weather data previews and missing-value summaries.
- Distribution plots and feature-correlation results.
- Classification reports for each model.
- Confusion-matrix heatmaps.
- Accuracy, weighted precision, weighted recall, and weighted F1-score comparisons.
- Cross-validation and learning-curve plots.
- Training-time and prediction-time comparisons.
- A predicted AQI category for a sample observation.

Illustrative category labels include `Good`, `Moderate`, `Unhealthy for sensitive groups`, `Unhealthy`, `Very Unhealthy`, and `Hazardous`. Actual scores and predictions depend on the datasets and execution environment; no performance figures are claimed here.

## Data / Model (for AI projects)

### Data

The notebook combines daily AQI CSV data with historical weather observations. The locations and periods represented in the notebook are:

- **Pittsburgh, Pennsylvania:** AQI files for 2017–2023, combined with weather data for the same period.
- **Bakersfield, California:** AQI files for 2016–2019, combined with weather data for the same period.

The feature set used in the notebook includes pollutant variables such as CO, Ozone, PM10, PM2.5 (named `PM25` in the notebook), and NO2, alongside weather variables such as maximum temperature (`tmax`) and wind speed (`wspd`) where available.

The notebook's AQI labels are generated from numeric AQI values using these ranges:

| AQI value used by notebook | Category |
| --- | --- |
| Below 51 | Good |
| 51–100 | Moderate |
| 101–150 | Unhealthy for sensitive groups |
| 151–200 | Unhealthy |
| 201–300 | Very Unhealthy |
| Above 300 | Hazardous |

These are the thresholds implemented in the notebook; verify them against the applicable official AQI standard before using the project outside an educational context.

### Models and evaluation

The notebook experiments with:
- Logistic Regression
- Random Forest
- Support Vector Machine (SVM)
- K-Nearest Neighbors (KNN)
- Decision Tree
- Gradient Boosting
- CatBoost
- Stacking Classifier

Evaluation includes accuracy, weighted precision, weighted recall, weighted F1-score, confusion matrices, cross-validation, learning curves, and runtime comparisons.

## Limitations

- The required AQI CSV datasets are external dependencies and are not included with the notebook by default.
- Results depend on data quality, coverage, feature availability, and the versions of the libraries used.
- AQI and weather data may have missing dates or inconsistent measurements.
- The notebook's correlation-based feature selection and preprocessing should be reviewed for data leakage before interpreting evaluation results.
- Scaling and resampling should be fitted only on training data; the preprocessing workflow should be audited before treating metrics as a reliable estimate of real-world performance.
- Model performance may vary between locations and time periods.
- The example prediction uses manually supplied feature values and should not be treated as a validated operational prediction service.
- This project is educational and must not replace official AQI reports or health guidance.

## Contributing

Contributions are welcome. You can open an issue to report a problem or suggest an improvement, or submit a pull request with a clear description of your changes.

Suggested improvements include documenting dataset sources, adding reproducible environment files, saving trained models, and validating preprocessing with a leakage-safe machine-learning pipeline.

## License

This project is licensed under the MIT License. See the [LICENSE](LICENSE) file for details.

Note: Third-party datasets and libraries may have separate license terms.

## Contact

**Author:** Abdullah Al Mufty  
**Email:** abdmufty28@gmail.com
