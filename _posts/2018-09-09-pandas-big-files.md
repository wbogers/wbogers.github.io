---
layout: post
title: Python - using pandas to process big csv-files
subtitle: Optimizing performance
tags: [Python, pandas, performance, settings]
---

Recently at work I had some issues in a Python project with the performance of *pandas* when processing big csv-files. Although the dataset I'm talking about here was not extremely big in terms of the number of records - around 600.000 rows with several dozens of columns - the calculations which were performed involved almost every column in the dataset (including looking up additional values for every column that was used and adding new columns with the calculated results on the fly). Around the time this issue arose, an article on the [Real Python](https://realpython.com) website (see reference at the bottom of this article) gave some very useful pointers regarding the various options that are available to speed up *pandas*. After trying out various possibilities (and combinations of several options) I ended up with code which performed about 10 times faster as the original code. I hope you'll find these tips useful.

## To make a long story short

In my specific case I had no other options available than looping over the rows in the *pandas* DataFrame and updating columns in the original Dataframe with calculated results: a vectorized approach was not easily possible (and also didn't have the fastest performance in this case, to be honest). For this scenario the following settings proved to be crucial to get the best performance:

* Process the file in chunks using the *chunksize* parameter of the *read_csv()* method of a DataFrame.
* Don't use *iterrows()* on a DataFrame, use *itertuples()* instead.
* Don't use the *loc* function of a DataFrame to write the results back to the DataFrame, use the *at* function.

By applying these three points, I was able to get a tremendous performance boost. In the screenshot below I have added a very simple example to show what I did.

![pandas_csv_example](/img/pandas_big_csv_example.jpeg)

## Notes

The use of the *chunksize* parameter eases the memory usage when processing a large *pandas* DataFrame. Initially I read in the complete dataset and noticed that processing the DataFrame slowed over time: by using chunks the performance becomes very predictable and stable, since each chunk is processed in about the same amount of time. It also makes it very easy to add a counter to your program to report on the status of the processing.

Using *itertuples()* instead of *iterrows()* changes the overhead associated with the returned values: in the case of *iterrows()* this is a *pandas* Series, in the case of *itertuples()* it is a much more efficient tuple of values that is returned. The looping is similar, but there is a difference in the way values are retrieved from a row during processing: in the tuple case this works by using an index, so in the example above I added functionality to translate column names in the DataFrame to indices we can use in the tuple. This is done pure for convenience and readability.

I am used to using the *loc* method when working with a *pandas* DataFrame, but in this specific case this proved not to be the most efficient option: the *at* method had a much better performance. The *loc* method has a bit more overhead during usage, so for this scenario (speed) it was not the best choice.


## Additional resources

1. [Fast, Flexible, Easy and Intuitive: How to Speed Up Your Pandas Projects](https://realpython.com/fast-flexible-pandas/)
2. [pandas documentation: read_csv / chunksize](https://pandas.pydata.org/pandas-docs/stable/generated/pandas.read_csv.html)
3. [pandas documentation: itertuples](https://pandas.pydata.org/pandas-docs/stable/generated/pandas.DataFrame.itertuples.html)
4. [pandas documentation: at](http://pandas.pydata.org/pandas-docs/stable/generated/pandas.DataFrame.at.html)
