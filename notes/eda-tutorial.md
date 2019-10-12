# EDA tutorial - Exploratory data analysis

Chloe Mawer and Jonathan Whitmore

https://www.youtube.com/watch?v=W5WE9Db2RLU

https://github.com/cmawer/pycon-2017-eda-tutorial

Before we apply machine learning problems there is the EDA step.
In fact one usually does EDA at each data analysis cycle.

## Why we do EDA

### Reasons for the analyst

* Want to identify pattern and develop hypotheses.
* Inform model selection and feature engineering:
	* Test technical assumptions for various models.
* Build an intuition for the data.

### Reasons for the consumer

* Ensures that correct results are delivered.
* Ensures the correct question is being asked.
* Reveal business assumptions.
* Provides context.
* Leads to insights that would not otherwise have been found.

Do EDA every time one iterates through your analysis.
Helps to stay open-minded.
Test all of the assumptions that you might have.

1. Form hypotheses/develop investigation themes.
2. Wrangle data - getting into the correct form.
3. Assess data quality and profile.
	* understand what it represents
	* missing data etc..
4. Explore each individual variable in the dataset.
5. Assess the relationship between variables and the target.
6. Assess interactions between variables.
7. Explore data across many dimensions (not just pairwise comparison).

Aim:

* Capture a list of hypotheses and questions.
* Record things to watch out for in future analyses.
* Show intermediate results to colleagues: don't do EDA in a bubble!
* Position visualisations and results together; EDA relies on your natural pattern recognition abilities.

## Introduction to Jupyter notebooks

Tab is very useful.
`%%` introduces cell magic
`%` introduces line magic
`function?` displays signature and docstring
`function??` displays the source code

## Red card dataset

* Before doing something, have a question or hypothesis in mind.
	* Draw a plot of what you want to see on paper to sketch the idea.
	* Very helpful to get your mind thinking in a visual way.
	* Make a plan on how to get there.
* Ask some questions:
	* how do you know you aren't fooling yourself?
	* what else can I check if this is actually true?
	* what evidence could there be that it is wrong?

### DataFrame/Series tips

`df.describe()` gives summary statistics for whole DataFrame.

For a Series the `.nunique()` method gives the number of unique entries.

### Tidy data

Based on paper called `Tidy data` by Hadley Wickham.

* Each variable forms a column.
* Each observation forms a row.
* Each type of observational unit forms a table.

First step is to make sure we don't have anything crazy.
No unexpected repeated values.
Why does each player only have one team?

---> then save the new tables in files (usually compressed)

### Missing data

* Package called `missingno` which visualises missing values.
	* Use `msno.matrix()`. Perhaps only on a sample.
	* or `msno.bar()`
* Need to be quite sensitive about what data we are missing out on.
	* Analyse if there is a pattern to the missing data.
	* A selection bias?
	* `msno.heatmap()` shows the correlation of missing values
	* E.g. the same row is missing the same columns
	* Probably we need to drop some or all of the missing data.
		* Forced to drop if we are missing one of the factors we are studying.

### Feature engineering

* Figure out exactly what we want the response variable to be.
	* This could be unclear if e.g. given multiple values to 'average' over.
* Figure out the distribution of the response variable.
	* Seaborn `distplot`.
* Seaborn correlation plot can be useful.
	* Also there are statistical methods to do this.
* Go through each of the features and guess what ones might be important.
	* Perhaps create higher level categories.
	* Figure out which level of granularity is most important.
* Try to feature engineer *away* from DateTimes.

### Pairwise relationships

* `from pandas.tools.plotting import scatter_matrix`

### ...and then right at the end...

* run `pandas_profiling.ProfileReport(df)` which attempts a very rough eda
* can try to be too clever

1:31:26