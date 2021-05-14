# **Analyzing Airport Data**
### Overview:
The goal of this code is to take two different data files on airport data, one containing the lat/longs of the airports and another containing the airline routes (ie the airports that the airplanes flew in between and their frequency) and produce a histogram of the distances flown on flights. It includes four coding challenges or steps to accomplishing this, which you can see detailed below. The repo contains the code itself, a PNG of the histogram produced, and a file including the datafiles used to create the histogram. See the bottom of this page to download the data for yourself. 

## Challenge 1
For the first coding challenge, we used the airport.dat file in order to print only airport names for a given country. This code took "airport.dat" as an input and produced a list of airports for a particular country as an output. 

## Challenge 2 - Reading the airport database
For this part of the code, we iterated through "airports.dat" in order to create two dictionaries. The first one mapped the airport ID key field (field 0) to the latitude (field 6) and the second one mapped the airport ID key field (field 0) to the longitude (field 7). It took "airports.dat" as an input and produced the two dictionaries (latitudes and longitudes) as an output. 

## Challenge 3 - Route distances
Now that we have the lat/lon of each airport we can calculate the distance of each airline route.
For coding challenge 3, I used the lat/long dictories to calculate the distance between airports. It took the lat and long dictionaries (that it turned into a departure airport lat/long and arrival airport lat/long for the distance function calculation) as an input and produced a list of distances an output. 

## Challenge 4 - Histogram
The goal of coding challenge 4 was to create a histogram of distances. It took the list of distances as an input and produces a histogram as an output. I used the matplotlab, scripy and numpy libraries in python. 

### Debugging
I intially struggled with coding challenge three, especially with some of the syntax of running the program (both figuring out to convert the variables to floats and reminding myself on how to work with lists. I used https://stackoverflow.com/questions/31087111/typeerror-list-object-is-not-callable-in-python slack outflow page to figure it out. Additionally, in crafting my histogram in coding challenge 4, I read through this slack overflow forum https://stackoverflow.com/questions/33203645/how-to-plot-a-histogram-using-matplotlib-in-python-with-a-list-of-data. 

### Data:
- Data downloaded from the [OpenFlights Project](https://openflights.org/data.html). If, for some reason you can't access the site or download the data, there is a [data folder in this repo](data) that contains archived data you could use. 

