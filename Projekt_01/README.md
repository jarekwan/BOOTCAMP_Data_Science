# RestCountries Data Analysis Project

This project presents a complete workflow for downloading, validating, cleaning, transforming, and analyzing country-level data from the public RestCountries API. The code implements a full Data Science pipeline: from raw JSON, through schema validation (Pydantic), missing-data analysis, feature transformations, statistics, regex validation, and visualizations.

## 1. Data Download from API
Data is downloaded from:
https://restcountries.com/v3.1/all?fields=name,capital,region,subregion,population,area,currencies,languages,timezones,flags

Main libraries used:
- requests – fetching JSON
- pandas – normalization and data handling
- json – structural inspection
- pydantic – strict schema validation

The project verifies the raw JSON response, checks status codes, prints structural information, and inspects key fields.

Colab Links:

Projekt1: https://colab.research.google.com/drive/14dhcRBR2VlQXfumiHCCb3OU23P4EIiF3?usp=sharing

Projekt1_light: https://colab.research.google.com/drive/18yJlYnC8yODdgqtXLjTE_0qojDpE0u33?usp=sharing

## 2. JSON Structure Analysis
A recursive function was implemented to describe the type of each field in the JSON document.  
The structure is printed in a human-readable tree using json.dumps().  
This reveals nested types (dict, list, str, int, float) and ensures full understanding of the dataset.

## 3. Pydantic Validation
Pydantic models defined:
- Flags
- NativeNameEntry
- Name
- Currency
- Country

Pydantic validates:
- types of each field
- optional keys
- nested structures (native names, currencies)
- lists (capital, timezones)

All countries are validated inside a list comprehension, with full error reporting for invalid entries.

## 4. Saving and Loading JSON
Raw JSON is saved to:
- countries.json

Then reloaded and normalized into a Pandas DataFrame using:
- pandas.json_normalize()

## 5. Manual DataFrame Validation
Checks performed:
- population is int
- area is int or float
- detection of rows with incorrect types
- detection of NaN values in all columns

Generated reports:
- braki.csv – missing values
- braki_procent.csv – percentage of missing values per column

Additional statistics:
- number of columns with missing data
- number of rows with missing data
- percentage of missing values sorted descending

## 6. Data Cleaning
Columns with more than 89% missing values were removed.

Missing values were filled using domain-specific rules:
- currencies.EUR.* → "not EUR"
- nativeName.fra.* and languages.fra → "nonFR"
- nativeName.eng.* and languages.eng → "nonENG"

After cleaning, checks were repeated:
- remaining columns with missing values
- remaining rows with missing values
- verification that DataFrame has no NaN

List of remaining columns saved to:
- pozostale_kolumny.csv

## 7. Type Consistency and Regex Validation
A set of selected columns was analyzed for consistent data types.  
Results saved to:
- typy_danych_sprawdzane.csv

Regex checks performed:
- capital names cleaned to letters and spaces only
- added column: capital_clean
- region names validated for alphabetic-only values

## 8. Statistical Analysis
For numerical columns:
- describe()
- means
- medians
- standard deviations

Saved to:
- statystyki_opisowe.csv

Additional operations:
- groupby(region) to compute average population and area
- pivot table of average population by region

## 9. NumPy Transformations
Added features:
- log_population, log_area (log1p)
- zscore_population, zscore_area (standardization)
- norm_population, norm_area (min-max normalization)

Saved to:
- kraje_z_normalizacja.csv

## 10. Visualizations
Matplotlib + Seaborn plots:
- histogram of population
- boxplot of area
- scatter plot: area vs population
- scatter plot: log(area) vs log(population)

These visualizations support exploration of distribution shapes and relationships.

## 11. Generated Files
The project automatically produces:
- countries.json
- braki.csv
- braki_procent.csv
- typy_danych_sprawdzane.csv
- pozostale_kolumny.csv
- kraje_z_normalizacja.csv
- statystyki_opisowe.csv

## 12. Summary
This project implements a complete EDA (Exploratory Data Analysis) pipeline:
1. Download raw JSON  
2. Analyze data structure  
3. Validate using Pydantic models  
4. Normalize and verify DataFrame  
5. Clean missing data  
6. Generate statistical reports  
7. Apply NumPy transformations  
8. Create visualizations  
9. Perform text validation with regex  

It demonstrates a full real-world workflow for preparing messy API data for analysis and modeling.

