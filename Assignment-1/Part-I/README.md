# TOPSIS Implementation for Multi-Criteria Decision Making

## Overview

This project implements the **TOPSIS (Technique for Order of Preference by Similarity to Ideal Solution)** method for multi-criteria decision-making analysis. TOPSIS is a widely used decision-making technique that helps in ranking alternatives based on multiple criteria.

## Methodology

### What is TOPSIS?

TOPSIS is based on the concept that the best alternative should have the shortest geometric distance from the **Positive Ideal Solution (PIS)** and the longest geometric distance from the **Negative Ideal Solution (NIS)**.

### Step-by-Step Process

#### 1. **Input Data Preparation**
The input data consists of:
- A decision matrix with alternatives (rows) and criteria (columns)
- First column: Names/identifiers of alternatives
- Remaining columns: Numerical values for each criterion
- Weights for each criterion
- Impact direction for each criterion (+ for beneficial, - for non-beneficial)

#### 2. **Normalization**
Each element of the decision matrix is normalized using vector normalization:

$$r_{ij} = \frac{x_{ij}}{\sqrt{\sum_{i=1}^{m} x_{ij}^2}}$$

Where:
- $r_{ij}$ = normalized value
- $x_{ij}$ = original value
- $m$ = number of alternatives

#### 3. **Weighted Normalized Decision Matrix**
The normalized values are multiplied by their respective weights:

$$v_{ij} = w_j \times r_{ij}$$

Where:
- $v_{ij}$ = weighted normalized value
- $w_j$ = weight for criterion $j$

#### 4. **Ideal Solutions**

**Positive Ideal Solution (Best):**
- For beneficial criteria (+): Maximum value
- For non-beneficial criteria (-): Minimum value

$$V^+ = \{v_1^+, v_2^+, ..., v_n^+\}$$

**Negative Ideal Solution (Worst):**
- For beneficial criteria (+): Minimum value
- For non-beneficial criteria (-): Maximum value

$$V^- = \{v_1^-, v_2^-, ..., v_n^-\}$$

#### 5. **Distance Calculation**

**Distance from Positive Ideal Solution:**

$$S_i^+ = \sqrt{\sum_{j=1}^{n} (v_{ij} - v_j^+)^2}$$

**Distance from Negative Ideal Solution:**

$$S_i^- = \sqrt{\sum_{j=1}^{n} (v_{ij} - v_j^-)^2}$$

#### 6. **TOPSIS Score Calculation**
The relative closeness to the ideal solution:

$$C_i = \frac{S_i^-}{S_i^+ + S_i^-}$$

Where:
- $C_i$ ranges from 0 to 1
- Higher values indicate better alternatives

#### 7. **Ranking**
Alternatives are ranked in descending order of their TOPSIS scores.

## Usage

### Command Line Syntax

```bash
python topsis.py <InputDataFile> <Weights> <Impacts> <OutputResultFileName>
```

### Parameters

- **InputDataFile**: Excel file (.xlsx) containing the decision matrix
- **Weights**: Comma-separated numerical weights for each criterion (e.g., "1,1,1,2,1")
- **Impacts**: Comma-separated impact directions (+ or -) for each criterion (e.g., "+,+,-,+,+")
- **OutputResultFileName**: Name of the output CSV file

### Example

```bash
python topsis.py data.xlsx "1,1,1,2,1" "+,+,-,+,+" output.csv
```

## How to Upload/Prepare Your Input File

### File Format Requirements

Your input file **must be** an Excel file with the `.xlsx` extension. Other formats (CSV, XLS, TXT) are not supported.

### File Structure

The Excel file should be structured as follows:

1. **First Column**: Names or identifiers of alternatives (e.g., M1, M2, Product A, etc.)
2. **Remaining Columns**: Numerical criteria values (at least 2 criteria columns required)
3. **Header Row**: Include descriptive headers for each column

### Step-by-Step File Preparation

#### Option 1: Create a New Excel File

1. **Open Microsoft Excel, Google Sheets, or LibreOffice Calc**
2. **Create the following structure**:

   | Alternative | Criterion 1 | Criterion 2 | Criterion 3 | ... |
   |-------------|-------------|-------------|-------------|-----|
   | Item1       | 0.75        | 85          | 12.5        | ... |
   | Item2       | 0.82        | 90          | 10.2        | ... |
   | Item3       | 0.68        | 78          | 15.8        | ... |

3. **Save the file**:
   - Click **File > Save As**
   - Choose **Excel Workbook (.xlsx)** format
   - Save it in the same directory as `topsis.py`
   - Give it a meaningful name (e.g., `my_data.xlsx`)

#### Option 2: Use the Sample Template

You can use the provided `data.xlsx` file as a template:

1. **Make a copy** of `data.xlsx`
2. **Rename it** to your desired filename
3. **Replace the data** with your own values
4. **Keep the structure**:
   - First column for names
   - Remaining columns for numeric criteria
   - Header row with column names

### File Location

Place your input Excel file in **one of these locations**:

1. **Same directory as topsis.py** (Recommended):
   ```
   Assignment-1/Part-I/
   ├── topsis.py
   ├── your_data.xlsx  ← Your file here
   └── README.md
   ```
   Then use: `python topsis.py your_data.xlsx "..." "..." output.csv`

2. **Different directory** (Use absolute or relative path):
   ```bash
   python topsis.py /path/to/your_data.xlsx "1,1,1" "+,+,-" result.csv
   ```

### Important Requirements

✅ **DO:**
- Use `.xlsx` format (Excel 2007 and later)
- Include at least 3 columns (1 for names + minimum 2 criteria)
- Use numeric values only in criteria columns (columns 2 onwards)
- Include a header row with column names
- Ensure no empty cells in criteria columns
- Save the file before running the program

❌ **DON'T:**
- Use CSV, TXT, or old XLS format
- Put text/strings in criteria columns (except headers)
- Leave criteria cells empty
- Use special characters or formulas in data cells
- Have less than 3 columns total

### Verification Checklist

Before running TOPSIS, verify your file:

- [ ] File has `.xlsx` extension
- [ ] File has at least 3 columns (1 identifier + 2+ criteria)
- [ ] First column contains alternative names/IDs
- [ ] Columns 2 to last contain only numeric values
- [ ] No empty cells in the data range
- [ ] Header row is present
- [ ] File is saved and closed (not open in Excel)
- [ ] File is accessible from the command line path you're using

### Example: Creating a Custom Input File

Let's say you want to compare 4 smartphones based on 3 criteria:

**Step 1**: Create an Excel file with this structure:

| Phone Model | Price  | Rating | Battery Life |
|-------------|--------|--------|--------------|
| Phone A     | 599.99 | 4.5    | 24           |
| Phone B     | 799.99 | 4.8    | 30           |
| Phone C     | 499.99 | 4.2    | 20           |
| Phone D     | 699.99 | 4.6    | 28           |

**Step 2**: Save as `phones.xlsx` in the Part-I directory

**Step 3**: Run the command:
```bash
python topsis.py phones.xlsx "1,2,1" "-,+,+" results.csv
```

Where:
- Weights: `"1,2,1"` (Rating is twice as important)
- Impacts: `"-,+,+"` (Lower price is better, higher rating and battery are better)

### Troubleshooting File Issues

**Error: "Input file not found"**
- Check the file path is correct
- Ensure the file exists in the specified location
- Use quotes around paths with spaces: `"my data.xlsx"`

**Error: "Unable to read input file"**
- Verify the file is in `.xlsx` format
- Make sure the file is not corrupted
- Close the file if it's open in Excel
- Check file permissions (must be readable)

**Error: "Input file must contain three or more columns"**
- Add more criteria columns (need at least 2 criteria + 1 name column)

**Error: "From 2nd to last columns must contain numeric values only"**
- Remove any text from criteria columns (keep text only in first column)
- Check for hidden characters or spaces
- Ensure cells don't contain formulas, only values

## Input Validation

The program performs comprehensive validation checks:

1. ✓ Correct number of parameters (4 required)
2. ✓ File existence check
3. ✓ Minimum 3 columns requirement
4. ✓ Numeric values validation (from 2nd to last column)
5. ✓ Matching counts (weights, impacts, and criteria columns)
6. ✓ Numeric weights validation
7. ✓ Impact symbols validation (must be + or -)
8. ✓ Comma-separated format validation

## Sample Data

### Input Data (data.xlsx)

| Fund Name | P1   | P2   | P3  | P4   | P5    |
|-----------|------|------|-----|------|-------|
| M1        | 0.84 | 0.71 | 6.7 | 42.1 | 12.59 |
| M2        | 0.91 | 0.83 | 7.0 | 31.7 | 10.11 |
| M3        | 0.79 | 0.62 | 4.8 | 46.7 | 13.23 |
| M4        | 0.78 | 0.61 | 6.4 | 42.4 | 12.55 |
| M5        | 0.94 | 0.88 | 3.6 | 62.2 | 16.91 |
| M6        | 0.88 | 0.77 | 6.5 | 51.5 | 14.91 |
| M7        | 0.66 | 0.44 | 5.3 | 48.9 | 13.83 |
| M8        | 0.93 | 0.86 | 3.4 | 37.0 | 10.55 |

**Criteria:**
- P1, P2, P4, P5: Beneficial (higher is better) - Impact: +
- P3: Non-beneficial (lower is better) - Impact: -

**Weights:** 1, 1, 1, 2, 1 (P4 has double weight)

## Results

### Result Table (output.csv)

| Fund Name | P1   | P2   | P3  | P4   | P5    | TOPSIS Score | Rank |
|-----------|------|------|-----|------|-------|--------------|------|
| M1        | 0.84 | 0.71 | 6.7 | 42.1 | 12.59 | 0.3769       | 6    |
| M2        | 0.91 | 0.83 | 7.0 | 31.7 | 10.11 | 0.3068       | 8    |
| M3        | 0.79 | 0.62 | 4.8 | 46.7 | 13.23 | 0.4841       | 3    |
| M4        | 0.78 | 0.61 | 6.4 | 42.4 | 12.55 | 0.3360       | 7    |
| M5        | 0.94 | 0.88 | 3.6 | 62.2 | 16.91 | **0.9772**   | **1** |
| M6        | 0.88 | 0.77 | 6.5 | 51.5 | 14.91 | 0.5903       | 2    |
| M7        | 0.66 | 0.44 | 5.3 | 48.9 | 13.83 | 0.4395       | 5    |
| M8        | 0.93 | 0.86 | 3.4 | 37.0 | 10.55 | 0.4566       | 4    |

### Analysis of Results

#### Best Alternative: **M5** (Rank 1)
- TOPSIS Score: **0.9772** (closest to ideal)
- Strengths:
  - Highest P1 (0.94), P2 (0.88), and P5 (16.91)
  - Excellent P4 performance (62.2) - double weighted criterion
  - Lowest P3 (3.6) - beneficial since P3 is non-beneficial
- M5 is clearly the best choice with significantly higher score

#### Second Best: **M6** (Rank 2)
- TOPSIS Score: **0.5903**
- Balanced performance across all criteria
- Strong P4 (51.5) and P5 (14.91) values

#### Third Best: **M3** (Rank 3)
- TOPSIS Score: **0.4841**
- Good P4 (46.7) and P5 (13.23)
- Low P3 (4.8) is advantageous

#### Worst Alternative: **M2** (Rank 8)
- TOPSIS Score: **0.3068** (farthest from ideal)
- Weaknesses:
  - Lowest P4 (31.7) despite double weight
  - Lowest P5 (10.11)
  - Highest P3 (7.0) - disadvantageous

### Performance Distribution

```
High Performers (Score > 0.5):
- M5: 0.9772 ⭐⭐⭐⭐⭐
- M6: 0.5903 ⭐⭐⭐⭐

Medium Performers (0.4 < Score < 0.5):
- M3: 0.4841 ⭐⭐⭐
- M8: 0.4566 ⭐⭐⭐
- M7: 0.4395 ⭐⭐⭐

Low Performers (Score < 0.4):
- M1: 0.3769 ⭐⭐
- M4: 0.3360 ⭐⭐
- M2: 0.3068 ⭐
```

## Visualization Recommendations

To better understand the results, consider creating the following visualizations:

### 1. **Bar Chart - TOPSIS Scores**
```python
import matplotlib.pyplot as plt
import pandas as pd

df = pd.read_csv('output.csv')
plt.figure(figsize=(10, 6))
plt.bar(df['Fund Name'], df['Topsis Score'], color='skyblue', edgecolor='navy')
plt.xlabel('Fund Name', fontsize=12)
plt.ylabel('TOPSIS Score', fontsize=12)
plt.title('TOPSIS Scores for All Alternatives', fontsize=14, fontweight='bold')
plt.axhline(y=0.5, color='r', linestyle='--', label='Threshold (0.5)')
plt.legend()
plt.grid(axis='y', alpha=0.3)
plt.tight_layout()
plt.savefig('topsis_scores_bar.png', dpi=300)
plt.show()
```

### 2. **Radar Chart - Multi-Criteria Comparison**
```python
import matplotlib.pyplot as plt
import pandas as pd
import numpy as np

df = pd.read_csv('output.csv')
categories = ['P1', 'P2', 'P3', 'P4', 'P5']

fig, ax = plt.subplots(figsize=(10, 10), subplot_kw=dict(projection='polar'))

angles = np.linspace(0, 2 * np.pi, len(categories), endpoint=False).tolist()
angles += angles[:1]

for idx, row in df.iterrows():
    values = row[categories].tolist()
    values += values[:1]
    ax.plot(angles, values, 'o-', linewidth=2, label=row['Fund Name'])
    ax.fill(angles, values, alpha=0.15)

ax.set_theta_offset(np.pi / 2)
ax.set_theta_direction(-1)
ax.set_thetagrids(np.degrees(angles[:-1]), categories)
ax.set_ylim(0, max(df[categories].max()))
ax.set_title('Multi-Criteria Performance Comparison', fontsize=16, fontweight='bold', pad=20)
ax.legend(loc='upper right', bbox_to_anchor=(1.3, 1.1))
ax.grid(True)

plt.tight_layout()
plt.savefig('radar_chart.png', dpi=300)
plt.show()
```

### 3. **Heatmap - Criteria Performance**
```python
import matplotlib.pyplot as plt
import pandas as pd
import seaborn as sns

df = pd.read_csv('output.csv')
data = df.set_index('Fund Name')[['P1', 'P2', 'P3', 'P4', 'P5']]

plt.figure(figsize=(10, 6))
sns.heatmap(data, annot=True, fmt='.2f', cmap='YlGnBu', cbar_kws={'label': 'Value'})
plt.title('Heatmap of Criteria Performance', fontsize=14, fontweight='bold')
plt.xlabel('Criteria', fontsize=12)
plt.ylabel('Alternatives', fontsize=12)
plt.tight_layout()
plt.savefig('criteria_heatmap.png', dpi=300)
plt.show()
```

### 4. **Ranking Visualization**
```python
import matplotlib.pyplot as plt
import pandas as pd

df = pd.read_csv('output.csv')
df_sorted = df.sort_values('Rank')

plt.figure(figsize=(10, 6))
colors = plt.cm.RdYlGn_r(df_sorted['Rank'] / df_sorted['Rank'].max())
plt.barh(df_sorted['Fund Name'], df_sorted['Topsis Score'], color=colors, edgecolor='black')
plt.xlabel('TOPSIS Score', fontsize=12)
plt.ylabel('Fund Name', fontsize=12)
plt.title('Ranking of Alternatives (Best to Worst)', fontsize=14, fontweight='bold')

for i, (score, rank) in enumerate(zip(df_sorted['Topsis Score'], df_sorted['Rank'])):
    plt.text(score + 0.01, i, f'Rank {rank}', va='center', fontsize=10)

plt.xlim(0, 1.1)
plt.grid(axis='x', alpha=0.3)
plt.tight_layout()
plt.savefig('ranking_horizontal.png', dpi=300)
plt.show()
```

## Key Insights

1. **M5 is the clear winner** with a TOPSIS score of 0.9772, significantly outperforming all other alternatives
2. **Large performance gap** between M5 (0.9772) and M6 (0.5903) - more than 60% difference
3. **P4 (double weighted)** is a critical criterion - alternatives with high P4 values rank better
4. **P3 (non-beneficial)** - lower values contribute to higher ranking
5. **Six alternatives** scored below 0.5, indicating moderate to poor performance

## Dependencies

```
pandas
numpy
openpyxl
```

Install using:
```bash
pip install pandas numpy openpyxl
```

## Error Handling

The program includes robust error handling for:
- Missing or incorrect number of arguments
- File not found errors
- Invalid file format
- Non-numeric values in criteria columns
- Mismatched dimensions (weights, impacts, columns)
- Invalid impact symbols
- Invalid weight values
- Empty or improperly formatted inputs

## Conclusion

This TOPSIS implementation provides a systematic and objective approach to multi-criteria decision-making. The results clearly identify M5 as the superior alternative, with M6 and M3 as reasonable second and third choices. The significant score differences validate the discriminating power of the TOPSIS method when properly weighted criteria are used.

---

**Author**: Predictive Analysis Assignment  
**Date**: January 19, 2026  
**Course**: Predictive Analysis - A1
