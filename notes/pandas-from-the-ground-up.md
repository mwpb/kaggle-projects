# Pandas from the ground up

Brandon Rhodes at PyCon 2015.

https://www.youtube.com/watch?v=5JnMutdy6Fw

https://github.com/brandon-rhodes/pycon-pandas-tutorial.git

## IPython tips

Two editing modes:-

1. insert mode
2. normal mode after hitting escape

In normal mode `a` inserts a cell above and `b` inserts a cell below.
In normal mode `h` shows the help page.
(Also `x` will 'cut' a cell which can be disconcerting.)

Usually want:
* `%matplotlib inline` which will plot inline

## Introduction

Using pandas effectively is often about exploration.

API reference is very useful:

pandas.pydata.org/pandas-docs/dev/api.html

## Five fundamental features of DataFrame

1. len(df)
2. df.head(n = 5): returns a new DataFrame with first n rows
3. df.tail(n = 5): returns a new DataFrame with last n rows
4. df[condition] returns all rows matching the condition
	* df[cd1 & cd2]
	* df[cd1 | cd2] as pandas cannot override and and or
	* condition could be a mask df.year > 1980
6. df.sort_values('column_name'), df.sort_index()

## More tips and plotting

* string operations accessible under df.column.str.startswith
* df.column.value_counts() counts occurrences of each value

* df.plot(x = 'col_x', y = 'col_y', kind = 'scatter')

## Paying attention to indexes

Very general purpose tool.
Organise data and provide fast access to data.

(Always start with df.head().)
When using `df[mask]` one looks through the *entire* DataFrame.
(This can be time consuming: check with `%%time`.)

`c = df.set_index(['column_name'])` replaces the index (on the left hand side) with the column specified. 
(And removes the title column.)
(The `append` optional argument tells pandas whether or not to keep the existing index.)

Then `c.loc['index_value']` where `loc` stands for location.
However an index only really helps pandas search if it is ordered.
Then it can use a divide and conquer algorithm.

`c = df.set_index(['title']).sort_index()` does this and then lookup is very fast.

Actually one can put multiple columns into the index by passing in a list of columns. Then access using tuples.

`df.reset_index('column_name')` pulls the index into a column.

(Almost any pandas operation that takes a column can probably take a list of column names.)

## Groupby

Rarely do people manually `set_index` and `sort_index`.
Instead they throw data out.

`df.groupby(['column1', 'column2'])`
gives a groupby object. 
If one then calls `.size()` (for instance) on this object we see that:-
* each of the columns specified are *sorted* indexes of a Series.

(Often it is useful to include `ylim=0` in the `plot()` because pandas will put the smallest obtained value at the bottom.)

Also you don't have to groupby a named column.
One can groupby any Series provided that it is the same height as the table.
`df.groupby[df.year//10*10]`
This is just like using a mask to filter: the mask is another Series of the same height of the table.

## Unstack

Now we consider the row along the top.
It is also an index.

`stack` and `unstack` are the equivalents of `set_index` and `reset_index`.
`unstack(col_number)` or `unstack("column_name")` therefore moves a column/index into the top row.
(To remember this `unstack` moves a column up.)

To fill in NaN use `df.fillna(default)`.

Important rule:
a DataFrame has two indexes
therefore is you (un)stack too much and remove one of them then pandas will return an Series to you.

## Merge

Given two DataFrames.
`df1.merge(df2)` tries to automatically figure out which rows should be the same.
Sometimes you have to tell it which ones are the same.


1:55:34 - is a summary.