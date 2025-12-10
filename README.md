# Machine Learning Project for Data Science Bootcamp by neuefische

This repository contains files for the ML Project during week 7-8 of the Data Science bootcamp by neuefische. This project was performed by Apostolos Koumparos, Karl Rackwitz, Stephanie Behrens, and Tim Dannenfeld. The goal of this project was to predict PM2.5 concentrations in the atmosphere by utilizing machine learning algorithms. 

The provided data set was acquired from https://zindi.africa/competitions/zindiweekendz-learning-urban-air-pollution-challenge. It contains over 30,000 measurements from over 300 different, unspecified locations over a timeframe of 3 months (January to April 2020). Measured metrics include temperature, precipitation, wind, and humidity, as well as densities and concentrations of gases like NO2, O3, CO, SO2, etc. For each measurement the dependent variable of the PM2.5 concentration is given.

## Project Structure

- `eda` – main notebook / script containing:
  - Exploratory Data Analysis (EDA)
  - Feature engineering
  - Model training and evaluation
- `data/` – raw and/or processed data 
- `presentation/` – slides from the project presentation (optional)

> Note: The **EDA file is the main entry point** to follow the full workflow from data exploration to model evaluation.

---

## Approach

1. **Exploratory Data Analysis (EDA)**
   - Understand distributions, missing values, and relationships between pollutants and PM2.5
   - Identify important features (e.g. CO and other gases, weather variables)

2. **Baseline Model**
   - Simple **Linear Regression** using a small subset of features (e.g. rainfall, humidity, wind speed)
   - Serves as a benchmark for more complex models

3. **Optimized Machine Learning Model**
   - **RandomForestRegressor** trained on a richer feature set (weather + gas densities)
   - Hyperparameter tuning with cross-validation
   - Strong reduction in prediction error compared to the baseline

4. **Expert Models & Blending**
   - Data split into categories such as:
     - Climate zones  
     - Urban vs. rural areas  
     - Air pollution levels  
     - Wind speed bins  
   - Separate **Linear Regression “expert models”** trained per category  
   - A blending model combines these expert predictions into a single final estimate

---

## Results (RMSE)

- Baseline Linear Regression: **≈ 42.5 μg/m³**  
- Tuned Random Forest: **≈ 28.7 μg/m³**  
- Blended expert model: **≈ 27.6 μg/m³** (best performance) :contentReference[oaicite:1]{index=1}

These results show that **PM2.5 can be predicted reasonably well** from weather and satellite-derived gas measurements, even where no ground sensors are available.

---

## Set up your Environment

### **`macOS`** type the following commands : 

- For installing the virtual environment you can either use the [Makefile](Makefile) and run `make setup` or install it manually with the following commands:

     ```BASH
    make setup
    ```
    After that active your environment by following commands:
    ```BASH
    source .venv/bin/activate
    ```
Or ....
- Install the virtual environment and the required packages by following commands:

    ```BASH
    pyenv local 3.11.3
    python -m venv .venv
    source .venv/bin/activate
    pip install --upgrade pip
    pip install -r requirements.txt
    ```
    
### **`WindowsOS`** type the following commands :

- Install the virtual environment and the required packages by following commands.

   For `PowerShell` CLI :

    ```PowerShell
    pyenv local 3.11.3
    python -m venv .venv
    .venv\Scripts\Activate.ps1
    python -m pip install --upgrade pip
    pip install -r requirements.txt
    ```

    For `Git-bash` CLI :
  
    ```BASH
    pyenv local 3.11.3
    python -m venv .venv
    source .venv/Scripts/activate
    python -m pip install --upgrade pip
    pip install -r requirements.txt
    ```

    **`Note:`**
    If you encounter an error when trying to run `pip install --upgrade pip`, try using the following command:
    ```Bash
    python.exe -m pip install --upgrade pip
    ```

## Usage

In order to train the model and store test data in the data folder and the model in models run:

**`Note`**: Make sure your environment is activated.

```bash
python example_files/train.py  
```

In order to test that predict works on a test set you created run:

```bash
python example_files/predict.py models/linear_regression_model.sav data/X_test.csv data/y_test.csv
```


## to be continued ...
