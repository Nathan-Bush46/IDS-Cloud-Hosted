# Data Manipulation with Jupyter Notebook

## Overview
This project demonstrates how to perform basic data manipulation tasks and create a scatter plot using a cloud-hosted Jupyter Notebook, such as Google Colab. It leverages the `pandas` library for data processing and `matplotlib` for data visualization.

## Requirements
1. **Cloud-hosted Jupyter Notebook**: To get started, set up a cloud-hosted Jupyter Notebook environment (e.g., [Google Colab](https://colab.research.google.com/)).
2. **Sample Dataset**: A CSV file with at least two columns: `stem-height` and `stem-width`.

## Setup Instructions
1. **Open Jupyter Notebook**: Start a new notebook on Google Colab or another cloud-based Jupyter platform.
2. **Install Libraries (if needed)**: Execute the following to ensure the required packages are installed.
   ```python
   !pip install pandas matplotlib
   ```
3. **Import Libraries**:
   ```python
   import pandas as pd
   import matplotlib.pyplot as plt
   ```

## Function: `calculate`
This function performs basic statistical analysis on specified columns of a dataset and optionally saves a scatter plot image.

### Parameters
- `file_path` (str): Path to the CSV file containing the dataset.
- `path_of_image` (str, optional): Directory path to save the scatter plot image. If `None`, the image is not saved.

### Returns
- List of tuples containing the mean, median, and standard deviation for the columns `stem-height` and `stem-width`.

### Usage
1. Upload the dataset (CSV format) to your notebook environment.
2. Define the `calculate` function in a cell:
   ```python
   def calculate(file_path, path_of_image=None):
       raw_training = pd.read_csv(file_path)
       df_train_x = raw_training.iloc[:, :-1]
       mean = ("mean\n", df_train_x[["stem-height", "stem-width"]].mean())
       median = ("median\n", df_train_x[["stem-height", "stem-width"]].median())
       std = ("std\n", df_train_x[["stem-height", "stem-width"]].std())
       df_train_x.plot.scatter("stem-width", "stem-height")
       if path_of_image:
           plt.savefig(path_of_image + "scatter_plot.png")
           plt.close()
       return [mean, median, std]
   ```
3. Call the `calculate` function:
   ```python
   results = calculate('path/to/your/dataset.csv', path_of_image='path/to/save/image/')
   print(results)
   ```
4. **Output**: The function will return mean, median, and standard deviation values for `stem-height` and `stem-width` and save a scatter plot to the specified directory if a path is provided.

## Example
For a dataset called `sample_data.csv`, run:
```python
results = calculate("sample_data.csv", "output/")
print(results)
```

This will display the statistics and save a scatter plot in the `output/` directory.

---

### Notes
- Ensure the dataset contains columns named `stem-height` and `stem-width`.
- When saving the plot, the function saves it as `scatter_plot.png` in the specified directory.

