# Stage 1: The World Wide Web and World Wide Geography

In this stage, you will write code to scrape some data from a webpage,
save it in json format, load the data to Pandas DataFrames,
and answer various questions about the data.

#### Question 1: what is the total area across all the countries in our dataset?

Write code to pull the data from here (do not manually download): https://raw.githubusercontent.com/tylerharter/caraza-harter-com/master/tyler/cs301/fall19/data/countries.json

Create a `download_countries()` function, which downloads the json file from the above url using `requests` module (requests.get() method) and then saves the `countries.json` file using json.dump() method. Make sure to call this function only once in your notebook.

Then create a Dataframe from this file and calculate the total area.

*Hint 1*: `pd.read_json(FILENAME)` will return a DataFrame by reading from
 the JSON file.  If the file contains list of dictionaries, each dictionary will be a row in the DataFrame.

*Hint 2*: review how to extract a single column as a Series from a
 DataFrame. You can add all the values in a Series with the `.sum()`
 method.

#### Question 2: How many countries do we have in our dataset?

----

Now, we will scrape some some data from here: http://techslides.com/list-of-countries-and-capitals
It contains the table of all the countries and capitals with latitude and longitude in tabular format.
Do not download the data using the csv or json file download link.
You need to write the code to scrape the data from this table.
Start by install `Beautiful Soup` and `requests` using pip.


Create a `download_capitals()` function, which should do the following:
* Download the html for the webpage using `requests` module (Hint: requests.get() method)
* Use beautiful soup to convert html text to soup.
* Find the table containing the data (Hint: .find() or .find_all() methods can be used).
* Find all the rows in the table (Note: rows are inside 'tr' html tag and data is in 'td' tag).
* Create a dictionary containing country name, capital and location coordinate. Create a list of dictionaries for all the countries.
<!-- * We only want those rows which are also present in `countries` variable. You need to filter and keep only such countries in our list. -->
* Save this list into file titled `capitals.json`. You can use json.dump() method. You file should look something like this.

```
[
  {
    "capital": "Brasilia",
    "country": "Brazil",
    "latitude": -15.783333333333333,
    "longitude": -47.916667
  },
  {
    "capital": "Nouakchott",
    "country": "Mauritania",
    "latitude": 18.066666666666666,
    "longitude": -15.966667000000001
  },
  {
    "capital": "Bern",
    "country": "Switzerland",
    "latitude": 46.91666666666666,
    "longitude": 7.466667
  },
  .
  .
  .
]
```
----
Now that we have completed our `download_countries()` and `download_capitals()` function, we want to make sure that we only download the data once and not every time we run the notebook. For this, we will provide you with the code of some basic caching. Copy paste the following code into your notebook. Use only `get_json()` function to read json file and do not call `download_countries()` or `download_capitals()` anywhere else in your notebook.

```python
def get_json(filename):
  if not os.path.exists(filename):
    if (filename=='countries.json'):
      download_countries()
    if (filename=='capitals.json'):
      download_capitals()

  with open(filename) as json_file:
    data = json.load(json_file)
  return data
```


#### Question 3: How many capitals do we have in the world?

Load the list of capitals in a variable named `capital_rows` using `get_json("capitals.json")`. Number of capitals would be the length of this capitals list. Return `len(capital_rows)` in your notebook.

----
You should note that we have more countries in our scraped dataset than our countries.json file. This is a common problem that data analysts face when we try to use two different datasets. Lets remove extra countries in our scraped dataset and make sure `capital_rows` only contains countries that are also in `countries.json` before you move to the next questoins.

Create a DataFrame with `capitals = DataFrame(capital_rows)`. Use `capitals` and `countries` to answer the following questions.

#### Question 4: what is the capital of Bermuda?

Now we can begin to answer more complex questions using our newly constructed DataFrame.

Our first task will be determining the capital of Bermuda.


*Hint*: you can use fancy indexing to extract the row where the
 `Country` equals "China".  Then, extract the `Capital` Series, from
 which you can grab the only value with the
 [Series.item()](https://pandas.pydata.org/pandas-docs/stable/generated/pandas.Series.item.html)
 function.

#### Question 5: Which country's capital is Maputo?

#### Question 6: which 5 countries have the southern-most capitals?

Produce a Python list of the 5, with southernmost first.

*Hint*: look at the documentation examples of how to sort a
 DataFrame with the
 [sort_values](https://pandas.pydata.org/pandas-docs/stable/generated/pandas.DataFrame.sort_values.html)
 function.

#### Question 7: which 3 countries have the northern-most capitals?

#### Question 8: for "birth-rate" and "death-rate", what are various summary statistics (e.g., mean, max, standard deviation, etc)?

*Format*: use the
 [describe](https://pandas.pydata.org/pandas-docs/stable/generated/pandas.DataFrame.describe.html)
 function on a DataFrame that contains `birth-rate` and `death-rate`
 columns.  You may include summary statistics for other columns in
 your output, as long as your summary table has stats for birth and
 death.

#### Question 9: for columns `literacy` and `phones`, what are various summary statistics?

*Format*: a table generated by the `describe` function.

In [some
 countries](https://en.wikipedia.org/wiki/Decimal_separator#Arabic_numerals),
 it is standard to use commas instead of periods to indicate decimals.
 The `literacy` and `phone` data is formatted this way (i.e., decimal
 numbers represented as strings, with commas for decimals).  You'll
 need to reformat the data to use periods (instead of commas), then
 convert the column of strings to a column of floats.

*Hint*: learn how to use the
 [astype](https://pandas.pydata.org/pandas-docs/stable/generated/pandas.DataFrame.astype.html)
 and
 [replace](https://pandas.pydata.org/pandas-docs/stable/generated/pandas.Series.str.replace.html)
 Pandas functions.

#### Question 10: what is the largest land-locked country in Europe?

A "land-locked" country is one that has zero coastline.  Largest is in terms of **area**.

#### Question 11: what is the largest land-locked country in Africa?

#### Question 12: what is the largest land-locked country in South America?

#### Question 13: what is the distance between Camp Randall Stadium and the Wisconsin State Capital?

This isn't related to countries, but it's a good warmup for the next
problems.  Your answer should be about 1.433899492072933 miles.

Assumptions:
* the latitude/longitude of Randall Stadium is 43.070231,-89.411893
* the latitude/longitude of the Wisconsin Capital is 43.074645,-89.384113
* use the Haversine formula: [http://www.movable-type.co.uk/scripts/gis-faq-5.1.html](http://www.movable-type.co.uk/scripts/gis-faq-5.1.html)
* the radius of the earth is 3956 miles
* answer in miles

If you find code online that computes the Haversine distance for you,
great!  You are allowed to use it as long as (1) it works and (2) you
cite the source with a comment.  Note that we won't help you
troubleshoot Haversine functions you didn't write yourself during
office hours, so if you want help, you should start from scratch on
this one.

If you decide to implement it yourself (it's fun!), here are some tips:
* review the formula: [http://www.movable-type.co.uk/scripts/gis-faq-5.1.html](http://www.movable-type.co.uk/scripts/gis-faq-5.1.html)
* remember that latitude and longitude are in degrees, but sin, cos, and other Python math functions usually expect radians.  Consider [math.radians](https://docs.python.org/3/library/math.html#math.radians)
* This means that before you do anything with the long and latitudes make sure to convert them to radians as your FIRST STEP
* people often use x^N to mean x raised to the Nth power.  Make sure you write it as x**N in Python.



#### Question 14: what is the distance between India and Brazil?

For the coordinates of a country, use its capital.

#### Question 15: What are the distances between Chile, Guyana, and Colombia?

Your result should be DataFrame with 3 rows (for each country) and 3
columns (again for each country).  The value in each cell should be
the distance between the country of the row and the country of the
column. For a general idea of what this should look like, open the
`expected.html` file you downloaded.  When displaying the distance
between a country and itself, the table should should NaN (instead of
0).

#### Question 16: what is the distance between every pair of South American countries?

Your result should be a table with 12 rows (for each country) and 12
columns (again for each country).  The value in each cell should be
the distance between the country of the row and the country of the
column.  For a general idea of what this should look like, open the
expected.html file you downloaded.  When displaying the distance
between a country and itself, the table should should NaN (instead of
0).

#### Question 17: what is the most central South American country?

This is the country that has the shortest average distance to other
South American countries.

*Hint 1*: check out the following Pandas functions:
* [DataFrame.mean](https://pandas.pydata.org/pandas-docs/stable/generated/pandas.DataFrame.mean.html)
* [Series.sort_values](https://pandas.pydata.org/pandas-docs/stable/generated/pandas.Series.sort_values.html) (note this is not the same as the DataFrame.sort_values function you've used before)

*Hint 2*: a Pandas Series contains indexed values.  If you have a
 Series `s` and you want just the values, you can use `s.values`; if
 you want just the index, you can use `s.index`.  Both of these
 objects can readily be converted to lists.

#### Question 18: What is the least central South American country?

This one has the largest average distance to other countries.

#### Question 19: how close is each country in South America to it's nearest neighbor?

The answer should be in a table with countries as the index and two
columns: `nearest` will contain the name of the nearest country and
`distance` will contain the distance to that nearest country.

*Hint 1*: find a Series of numerical data you can experiment with
 (perhaps from one of the DataFrames you've been using for this
 project).  If your Series is named `s`, try running `s.min()`.
 Unsurprisingly, this returns the smallest value in the Series.  Now
 try running `s.idxmin()`.  What does it seem to be doing?

*Hint 2*: if you run `df.min()` on a DataFrame, Pandas applies that
 function to every column Series in the DataFrame.  The returned value
 is a Series.  The index of the returned Series contains the columns
 of the DataFrame, and the values of the returned Series contain the
 minimum values.  If you run `df.idxmin()` on a DataFrame, the
 returned values contain indexes from the DataFrame.

 #### Question 20: how far is each country in South America to it's furthest neighbor?

 The answer should be in a table with countries as the index and two
 columns: `furthest` will contain the name of the furthest country and
 `distance` will contain the distance to that nearest country