TOPSIS Analysis Package

A Python library for performing TOPSIS (Technique for Order of Preference by Similarity to Ideal Solution) analysis on numerical datasets. This tool supports both command-line functionality and a programmatically importable module for analyzing datasets with numerical entries (e.g., int32, int64, float32, float64).
Overview

TOPSIS is a decision-making technique used to rank alternatives based on their proximity to an ideal solution, considering multiple criteria. This package handles data normalization, assigns weights to criteria, and factors in whether criteria should be maximized or minimized.
Installation

pip install topsis-102217132

Usage
As a Python Module

from topsis_analysis import run

# Perform TOPSIS analysis
result_df = run(
    input_df,           # Pandas DataFrame with numerical columns
    weights,            # List of numerical weights for each criterion
    impacts,            # List of '+' (maximize) or '-' (minimize) for each criterion
)

Command-Line Tool

python -m topsis_analysis <input_csv_path> <weights> <impacts> <output_csv_path>

Parameters
General Parameters (Module & CLI):

    Input Data:
        Must consist solely of numerical values (int32, int64, float32, float64)
        The first column will serve as the identifier (index)
        Datasets with missing values are not supported.

    Weights:
        Must sum up to 1
        The number of weights must equal the number of numerical columns (excluding the identifier/index column)
        For the module: Provide as a Python list of floats
        For CLI: Provide as a comma-separated string (e.g., "0.3,0.4,0.3")

    Impacts:
        Use '+' for criteria to maximize and '-' for criteria to minimize
        The number of impacts should match the number of numerical columns (excluding the identifier/index column)
        For the module: Provide as a Python list of strings
        For CLI: Provide as a comma-separated string (e.g., "-,+,+,-")

CLI-Only Parameters:

    output_csv_path: File path where the output CSV will be saved.

Example Usage
As a Python Module

import pandas as pd
from topsis_analysis import run

# Read the input dataset
data = pd.read_csv('input_data.csv')

# Define weights and impacts
weights = [0.3, 0.4, 0.3]
impacts = ['+', '+', '-']

# Run TOPSIS
result = run(data, weights, impacts)

# Save the results
result.to_csv('result.csv', index=False)

Using the CLI

python -m topsis-102217132 input_data.csv 0.3,0.4,0.3 +,+,- result.csv

Input CSV Format Example

Model,Price,Storage,Battery,Performance
A,799,256,12,85
B,999,512,10,92
C,699,128,15,78

Output CSV Example

Model,Price,Storage,Battery,Performance,TOPSIS Score,Rank
A,799,256,12,85,0.534,2
B,999,512,10,92,0.687,1
C,699,128,15,78,0.423,3

Error Handling

The package offers robust error validation to ensure the following:

    Matching numbers of weights, impacts, and criteria columns
    Presence of numerical data types
    No missing values in the input data
    Valid paths for reading/writing files (CLI)
    Proper '+' or '-' symbols in the impact list

Dependencies

    Python 3.7 or higher
    pandas
    numpy

Contribution

Contributions are highly appreciated! Feel free to open issues or submit pull requests for improvements.
License

This package is distributed under the MIT License. Refer to the LICENSE file for full details.
