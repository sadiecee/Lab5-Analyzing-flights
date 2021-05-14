# **Analyzing Airport Data**
In this assignment we're going to analyze aiport data. We'll be downloading some data in a common file format, exploring it using Python to discover the distances of certain flights, and then creating a basic [histogram](https://en.wikipedia.org/wiki/Histogram) as our final output.  

### To complete this assignment you will need:
- A Google account. We'll be using Colab, but also space in your Google Drive: this will be nice example of hosting a small data science project with your own services.
- Data downloaded from the [OpenFlights Project](https://openflights.org/data.html). If, for some reason you can't access the site or download the data, there is a [data folder in this repo](data) that contains archived data you could use. That being said, I want you to use the most recent data you can get!

### What you will submit:
A link to your Github repo. The repo must contain your Python code (either as script in `.py` or a notebook in `.ipynb` format). There are four code challenges here, so be sure your code is well documented and shows us how you are solving each challenge! The `README` of your repo should briefly summarize the project (in your own words) and contain an embdded image of your final output. You do not need to include the data files you downloaded (as I have here), but can if you like. If you're going to use this repo as part of your portfolio I suggest that you include a "data" section in your readme that explains what data you've used and links to the pages where it can be downloaded (in fact, you can just copy that text from this repo!).

## Why is this lab important?
Up to now, we've been learning about the basics of Python and have done work manipulating strings, lists, dictionaries, and have started importing files such as `.txt` files. In this lab, we're going to be working with multiple files in `.csv` format. Spreadsheets are, for better or worse, the _lingua franca_ of humanitarian and international development data. As [Sarah Telford of the UN's Humanitarian Data Exchange platform tells it](https://www.devex.com/news/opinion-humanitarian-world-is-full-of-data-myths-here-are-the-most-popular-91959), "Big data is promising, but the challenge in the humanitarian sector is bringing together small amounts of non-standardized data, mostly stored in spreadsheets, from dozens of organizations to create a common picture of needs and response."

The ability to find tabular (ie. spreadsheet) data; explore it; manipulate it; and analyze it is a critical skill. Not only that, but just being able to provide basic graphical representation of quantitative information (our histogram of flight distances) to help decision makers understand the basics of data, is important. Again, to cite the article above, "...cleaning and combing data and making choices about how data will be presented... is different than drawing conclusions from the data to understand why a crisis is deteriorating, or to decide whether to prioritize a cash response rather than food distribution. Data experts create the visuals; subject matter experts do the analysis." It's important to understand that, sometimes, your role as a GIS analyst may be to prepare and display data for decision makers or subject matter experts (and [there are a LOT of them](https://blog.veritythink.com/post/60157407408/these-are-the-humanitarian-decision-makers)) for them to interpret.  

# Getting started
Before we get to the data, let's briefly touch on reading and writing comma-separated data, or data from `.csv` files. Comma-separated values is a way of expressing structured data in flat text files like this:

```
"Refugee_Camp_Name","Country","Population2006","Population2014"
"Kakuma","Kenya","90457","153959"
"Hagadera","Kenya","59185","106968"
"Adjumani","Uganda","54051","96926"
"Dagahaley","Kenya","39526","88486"
"Zaatari","Jordan","0","84773"
```
This is a commonly used format to get data in and out of programs like spreadsheet software, where the data are tabular. [Python comes with a CSV module](https://docs.python.org/3/library/csv.html) that provides one way to easily work with CSV-delimited data: Try downloading the `Camp_stats.csv` file, wihch is previewed above and [can be accessed in the data folder](data/Camp_stats.csv), to your desktop or local working environment. Then run the following code in Colab to choose it as a file:
```python
# Upload local script to Colab here.
from google.colab import files
uploaded = files.upload()
```
Now you can open the data up in Colab! Run the following code:
```python
import csv
f=open("Camp_stats.csv")
for row in csv.reader(f):
    print(row)
```
Each row is read as a list of strings representing the fields in the row.

## Why not use `.split()` or `.strip()`?

We already a learned another way to do this. We’ve learned `split(",")` to split each row of text into comma-delimited fields, and then `strip()` to take off the quote marks, in IDCE 302 using these methods to clean up the `.txt` survey file, if you recall!

There are a few good reasons to use the CSV module here:
*   The csv module makes it clear what you’re doing to anyone reading your code.
*   The csv module is less likely to contain an error that splits some lines the wrong way.
*   The csv module has a lot of other features ([documented here](https://docs.python.org/3/library/csv.html)) that allow it to process differently formatted files, so you can easily update your program if the file format changes.

# **Reading Airport Data**
We’re going process our own data now, using freely available airline data sets from the [OpenFlights project](https://openflights.org/). Visit the [OpenFlights data page](https://openflights.org/data.html) and download their airports data file - “airports.dat”. This is a file in CSV format, open it in a text editor if you want to have a look at it. If, for some reason, you can't access the OpenFlights page or download the data, there is an [archived data set in the data folder of this tutorial](data/airports.dat).

## Challenge 1

Can you use this file to print all of the airport names for a particular country (say, Australia or Russia)? To get you started, on the OpenFlights web page it shows that “Name” is the second field in each row of data. This means in the list of fields it will have index 1 (index 0 is the first field.)

As a starting point, here’s some code that prints the name of *every* airport:
```python
import csv
f = open("airports.dat")
for row in csv.reader(f):
    print(row[1])
```
Don't forget to start by uploading the airports.dat file!

# **Creating an Airline Route Histogram**

We’re going to combine everything we’ve learned into a more complex problem to solve.

OpenFlights distribute databases for both airline locations and airline route details. You can download the routes database “routes.dat” from the OpenFlights data page. This database stores every unique flight route that OpenFlights knows about. Take a moment to look at the fields available in the routes data (listed on the OpenFlights page.) Again, if for some reason, you can't access the OpenFlights page or download the data, there is an [archived data set in the data folder of this tutorial](data/routes.dat).

By using both data sources, we can calculate how far each route travels and then plot a histogram showing the distribution of distances flown.

This a multiple stage problem:
*   Read the airports file (airports.dat) and build a dictionary mapping the unique airport ID to the geographical coordinates (latitude & longitude.) This allows you to look up the location of each airport by its ID.
*   Read the routes file (routes.dat) and get the IDs of the source and destination airports. Look up the latitude and longitude based on the ID. Using those coordinates, calculate the length of the route and append it to a list of all route lengths.
*   Plot a histogram based on the route lengths, to show the distribution of different flight distances.

## Challenge 2 - Reading the airport database
Write code to read through “airports.dat” and create a dictionary mapping from an airport ID key (use the numeric ID in the first field) to the geographic coordinates. You may want to create two dictionaries, one holding latitudes and one holding longitudes.

Look back at the OpenFlights data page to see the fields available in the airports.dat file. Hint: I ended up having to look at a copy of their data in their Github repo.

## Challenge 3 - Route distances
Now that we have the lat/lon of each airport we can calculate the distance of each airline route.
For coding challenge 3, I used the lat/long dictories to calculate the distance between airports. It took the lat and long dictionaries (that it turned into a departure airport lat/long and arrival airport lat/long for the distance function calculation) as an input and produced a list of distances an output. 

## Challenge 4 - Histogram
The goal of coding challenge 4 was to create a histogram of distances. It took the list of distances as an input and produces a histogram as an output. I used the matplotlab, scripy and numpy libraries in python. 

### Debugging
I intially struggled with coding challenge three, especially with some of the syntax of running the program (both figuring out to convert the variables to floats and reminding myself on how to work with lists. I used https://stackoverflow.com/questions/31087111/typeerror-list-object-is-not-callable-in-python slack outflow page to figure it out. Additionally, in crafting my histogram in coding challenge 4, I read through this slack overflow forum https://stackoverflow.com/questions/33203645/how-to-plot-a-histogram-using-matplotlib-in-python-with-a-list-of-data. 
