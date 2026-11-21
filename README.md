![Uploading Screenshot 2026-11-21 160914.png…]()


## Project Overview

This project uses the KNIME Analytics Platform to prepare and explore the Titanic passenger dataset, train a Decision Tree classification model, predict passenger survival, and evaluate the predictions.

## Workflow

The KNIME workflow is organized into data preparation, data exploration, model building, and report/export sections.

### 1. Data Preparation

1. **CSV Reader** – Imports the Titanic dataset.
2. **Statistics** – Generates descriptive statistics for the imported columns.
3. **Column Filter** – Keeps the passenger attributes required for analysis and modelling.
4. **Missing Value** – Handles missing values in the selected columns.
5. **Rule Engine** – Creates `SurvivedLabel` from the original `Survived` field, using `Yes` and `No` class labels.
6. **Row Filter** – Selects the records required for the analysis branch.

### 2. Data Grouping and Exploration

7. **GroupBy** – Groups records by `Sex` and calculates the mean of `Survived` and the passenger count.
8. **Statistics** – Inspects the prepared data and its distributions.
9. **Color Palette Designer** – Assigns colours to the `SurvivedLabel` categories.
10. **Bar Chart** – Compares the survival categories.
11. **Histogram** – Displays the distribution of passenger ages.
12. **Box Plot** – Examines the distributions of selected numerical attributes.
13. **Scatter Plot** – Displays selected passenger attributes as points for comparison.
14. **Linear Correlation** – Generates a correlation table for the selected columns.

The GroupBy output showed:
- Female passengers: mean survival value approximately **0.742**, across **314** records.
- Male passengers: mean survival value approximately **0.189**, across **577** records.

### 3. Decision Tree Modelling

15. **Column Filter and Table Partitioner** – Selects the modelling attributes and target column, then divides the data using stratified sampling based on `SurvivedLabel`. The first partition contains **70%** of the data and the second partition contains the remaining **30%**.
16. **Decision Tree Learner** – Trains a classification model using the first partition, with `SurvivedLabel` as the class column.
17. **Decision Tree Predictor** – Uses the trained model and the second partition to generate predicted survival labels and class probability columns.
18. **Scorer** – Compares `Prediction (SurvivedLabel)` with the actual `SurvivedLabel`.
19. **Decision Tree View** – Displays the trained decision tree and its decision branches.

### 4. Results

The Scorer output displayed the following confusion matrix:

| Actual class | Predicted No | Predicted Yes |
|---|---:|---:|
| No | 152 | 41 |
| Yes | 13 | 62 |

The overall accuracy displayed by the Scorer was **0.799** (approximately **79.9%**).

### 5. Exported Files

The workflow includes Excel Writer nodes for exporting the prepared data and analysis outputs. The exported Excel sheets include:

- `Prepared_Data`
- `Grouped_Analysis`
- Model-evaluation results

A CSV Writer is connected to the Decision Tree Predictor output. The prediction results are exported as:

- `LA3_Prediction_Results.csv`

The prediction CSV contains passenger attributes, the actual `SurvivedLabel`, class probability columns, and `Prediction (SurvivedLabel)`. The exported CSV was opened in Visual Studio Code for verification.

## Requirements

- KNIME Analytics Platform
- The Titanic dataset CSV used as the input to the CSV Reader
- Microsoft Excel or another spreadsheet application to view the exported `.xlsx` files
- Visual Studio Code or a text editor to inspect the exported `.csv` file

## How to Run

1. Open the KNIME workflow in KNIME Analytics Platform.
2. Make sure the Titanic dataset file is available at the location configured in the CSV Reader node.
3. Configure the CSV Reader if the dataset is stored in a different location.
4. Execute the data-preparation nodes in order.
5. Execute the GroupBy and data-exploration nodes to generate the analysis outputs and charts.
6. Execute the Column Filter and Table Partitioner nodes in the modelling branch.
7. Execute the Decision Tree Learner.
8. Execute the Decision Tree Predictor using the trained model and the second partition.
9. Execute the Scorer to view the confusion matrix and accuracy.
10. Execute the Decision Tree View to display the tree.
11. Configure the Excel Writer and CSV Writer output paths, then execute the writer nodes to save the results.

## Output

After successful execution, the workflow produces:
- Prepared passenger data
- Grouped survival analysis by sex
- Statistical summaries and visualizations
- A trained Decision Tree model and its tree view
- Predicted survival labels and class probabilities
- Scorer evaluation results
- Excel and CSV output files
"""

out_path = "/mnt/data/README.md"
pypandoc.convert_text(readme, "md", format="md", outputfile=out_path, extra_args=["--standalone"])
print(out_path)

