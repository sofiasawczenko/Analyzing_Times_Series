# Alucar - Analisando as Vendas

This project analyzes the sales data of the company "Alucar" from the years 2017 and 2018, utilizing Python's `pandas` for data manipulation and `seaborn` for visualizing trends in the data.

## Overview

The dataset used in this project contains monthly sales data for Alucar, with two primary columns:
- `mes`: The month of the sale (in YYYY-MM-DD format)
- `vendas`: The number of sales for that month

This analysis involves several steps:
1. Importing and cleaning the data.
2. Visualizing sales trends over time.
3. Calculating and visualizing the month-to-month increase in sales.
4. Calculating and visualizing the acceleration of sales increases.

## Requirements

Ensure you have the following libraries installed:
- pandas
- seaborn
- matplotlib

Install the necessary libraries by running:
```bash
pip install pandas seaborn matplotlib
```

## Steps

### 1. Loading the Data
The dataset is loaded from a CSV file alucar.csv and displayed to inspect the first few rows.

```bash
import pandas as pd
alucar = pd.read_csv('dados/alucar.csv')
alucar.head()
```
### 2. Data Inspection
The number of rows and columns are checked, and the data types of the columns are inspected:

```bash
print('Quantidade de linhas e colunas:', alucar.shape)
print('Quantidade de dados nulos', alucar.isna().sum().sum())
print(alucar.dtypes)
```
### 3. Data Cleaning
The mes column, initially in object format, is converted to a datetime format for better handling:

```bash
alucar['mes'] = pd.to_datetime(alucar['mes'])
alucar.dtypes
```
### 4. Visualization - Sales Over Time
We use seaborn to create a line plot to visualize how sales have evolved over time from January 2017 to December 2018:

```bash
import seaborn as sns
from matplotlib import pyplot as plt

sns.lineplot(x='mes', y='vendas', data=alucar)
```
### 5. Visualizing Sales Increase
We calculate the month-to-month increase in sales using the diff() function:

```bash
alucar['aumento'] = alucar['vendas'].diff()
This creates a new column, aumento, representing the sales increase each month. The increase is visualized with a line plot:
```
```bash
sns.lineplot(x='mes', y='aumento', data=alucar)
```
### 6. Custom Plotting Function
A custom function plotar() is defined to easily generate line plots with customizable titles, labels, and axes:

```bash
def plotar(titulo, labelx, labely, x, y, dataset):
    sns.set_palette('Accent')
    sns.set_style('darkgrid')
    ax = sns.lineplot(x=x, y=y, data=dataset)
    ax.figure.set_size_inches(12, 6)
    ax.set_title(titulo, loc='left', fontsize=18)
    ax.set_xlabel(labelx, fontsize=14)
    ax.set_ylabel(labely, fontsize=14)
    ax = ax
```
This function is then used to plot the sales increase over time:

```bash
plotar('Aumento das vendas da Alucar de 2017 e 2018', 'Tempo', 'Aumento', 'mes', 'aumento', alucar)
```

### 7. Calculating Acceleration of Sales Increase
To analyze the acceleration of sales increases, we calculate the second derivative (change in increase):

```bash
alucar['aceleracao'] = alucar['aumento'].diff()
This is visualized using the same plotar() function:
```
```bash
plotar('Aceleração das vendas da Alucar de 2017 e 2018', 'Tempo', 'Aceleração', 'mes', 'aceleracao', alucar)
```

## Results
The analysis helps to understand the monthly trends, increases, and acceleration in the sales data. Visualizations provide insights into how Alucar's sales have grown over time and how the growth rate has changed.

## Conclusion
This project demonstrates a simple yet effective analysis of time series sales data using Python, pandas, and seaborn. The techniques covered include data cleaning, trend visualization, and calculating the rate of change (increase and acceleration) in the data.
