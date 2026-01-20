# TOPSIS Python Package

This package implements the **TOPSIS (Technique for Order Preference by Similarity to Ideal Solution)**
method for multi-criteria decision making.

It is developed as **Part 2 of Predictive Analysis – Assignment 1** and is published as a Python package
on PyPI with a command-line interface (CLI).

---

## Installation

```bash
pip install topsis-shabd
```

---

## Usage

```bash
topsis <input_file.xlsx> "<weights>" "<impacts>" <output_file.csv>
```

### Example

```bash
topsis data.xlsx "1,1,1,2,1" "+,+,-,+,+" output.csv
```

### Parameters

- `input_file.xlsx` : Excel file containing the decision matrix  
- `weights` : Comma-separated numerical weights for each criterion  
- `impacts` : Comma-separated impacts (`+` for beneficial, `-` for non-beneficial)  
- `output_file.csv` : Output CSV file containing TOPSIS scores and ranks  

---

## Output

The output file contains:
- Original data
- TOPSIS score for each alternative
- Rank based on TOPSIS score (higher is better)

---

## PyPI Link

https://pypi.org/project/topsis-shabd/

---

## Author

Shabd Sharma  
Predictive Analysis – Assignment 1 (Part 2)
