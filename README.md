# TrafficViolations_CaseStudy
1 - 3 page github Readme with above information included
Outline the process for the data pipeline

Data was taken from the Maryland Department of Transportaion via Kaggle. 
EDA was as follows:
+ Frequency analysis of vairous aspects of the Data 
+ by year examination of stops
+ feature type
+ Vehicle color
+ Vehicle type
+ Viloation type

I decided to plot a random sample of the geoposition data on a map of the realivat area, and using 30 thousand samples I generated a fairly accurate estimation of where all the speedtraps likely are in the Maryland/DC area.

![alt text][map]

[map]: https://raw.githubusercontent.com/mkain112/TrafficViolations_CaseStudy/master/MarylandHeatMap.png "Full Zoom and more detail available in the repo"

If nothing else was learned from this project, I still earned how to find speedtraps and police hotspots. If nothing else I have decied to do this with data from any region I end up living in. The full heatmap code is available in this repo.

Then we decided we wanted to look into more detail about the types of cars with violations
This lead to additonal data being procured from the EPA and the Ford Motor company.

Using Fuzzy String analysis via the FuzzyWuzzy module I matched the type and model of each vehicle to its correstponding EPA fule consumption estimate. Any rows that had a match confidence of below 80% were dropped.

In order to effectivly match models I needed to limit the search to a single vehicle type. I chose Ford, somewhat arbitraily as it was the Make i was working on when I had the idea.

There was about 1.3 million rows of data in the violations data set with 35 columns ranging from time/date/geoposition of the stop to race gender and charge associated with the stop, as well as color, make and model of the vehicle being driven. In my analysis of the Ford data (both Violation and EPA) I was analyizing aproximately 60 thousand rows of data after cleaning and reducing the data set to most common variables and removing erronious or difficult to parse entries.



Multiple Data Visualizations
Outline Hypothesis Tests and results
Notebook containing EDA
Title that is NOT ‘Capstone 1’
