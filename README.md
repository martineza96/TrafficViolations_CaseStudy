https://docs.google.com/presentation/d/1JM18MIVkmse6pizhs9QKPcZw9q7IZwXjyuT1YkPXo1o/edit?usp=sharing

Data was taken from the Maryland Department of Transportaion via Kaggle. 
EDA was as follows:
+ Frequency analysis of vairous aspects of the Data 
+ by year examination of violation frequency
![alt text][byYear]
+ Stops per day
![alt text][perDay]
+ Vehicle type
+ Viloation type

![alt text][vios]

I decided to plot a random sample of the geoposition data on a map of the realivat area, and using 30 thousand samples I generated a fairly accurate estimation of where all the speedtraps likely are in the Maryland/DC area.

![alt text][map]

If nothing else was learned from this project, I still earned how to find speedtraps and police hotspots. I have decied to do this with data from any region I end up living in. The full, zoomable heatmap code with streets is available in this repo.

Then we decided we wanted to look into more detail about the types of cars with violations
This lead to additonal data being procured from the EPA and the Ford Motor company.

Using Fuzzy String analysis via the FuzzyWuzzy module I matched the type and model of each vehicle to its correstponding EPA fule consumption estimate. Any rows that had a match confidence of below 80% were dropped.

In order to effectivly match models I needed to limit the search to a single vehicle type. I chose Ford, somewhat arbitraily as it was the Make I was working on when I had the idea. Then I created a dictionary of the unique models listed in police reports (often mispelled and never conforming to a standard) and compaired that dictionary to the list of Ford models provided by the EPA. This functioned as a 'translation dictionary' from police report to EPA official name.

Initially there was about 1.3 million rows of data in the violations data set with 35 columns ranging from time/date/geoposition of the stop to race gender and charge associated with the stop, as well as color, make and model of the vehicle being driven. In my analysis of the Ford data (both Violation and EPA) I was analyizing aproximately 60 thousand rows of data after cleaning and reducing the data set to most common variables and removing erronious or difficult to parse entries.

Eventually I was able to pull together frequency data for Ford Model violations and EPA fuel economy. Each model has three values associated with its fuel economy, its highway efficency, city efficency, and combined efficency.

![alt text][badscatter]

With a p value of -0.5906 it is not enough to reject any hypothesis.

But this data didnt account for the inherent frequency of cars on the road. To correct for this I went to Fords annual sales report and pulled out the data for annual sales of each model. Where there was a lack of information I assumed that the sales were proportionately distributed across the various subtypes of model in the same way as violations. Maintaining this ratio to ensure that the effects of frequency were appropreately mitigated as much as possible, resulting in the following plots and regressions.

![alt text][combo]

![alt text][hwy]

![alt text][city]

The null hypothesis was that EPA estimated MPG was unrelated to frequency of traffic stops/sale, but upon analysis it was discovered, with p values of 0.0021 combined,  0.0010 highway and 0.0031 city respectivly that the null hypothesis cannot be accepted and required further analysis.

[vios]: https://github.com/mkain112/TrafficViolations_CaseStudy/blob/master/10MostCommonViolations.png?raw=true
[map]: https://raw.githubusercontent.com/mkain112/TrafficViolations_CaseStudy/master/MarylandHeatMap.png "Full Zoom and more detail available in the repo"
[perDay]: https://github.com/mkain112/TrafficViolations_CaseStudy/blob/master/NumberOfTrafficStopsByDayOfYear.png?raw=true
[byYear]: https://github.com/mkain112/TrafficViolations_CaseStudy/blob/master/ViolationHistByYear.png?raw=true 
[badscatter]: https://github.com/mkain112/TrafficViolations_CaseStudy/blob/master/badscatter.png?raw=true
[city]: https://github.com/mkain112/TrafficViolations_CaseStudy/blob/master/cityregress.png?raw=true "City MPG vs Violations Per sale"
[hwy]: https://github.com/mkain112/TrafficViolations_CaseStudy/blob/master/hwyregress.png?raw=true "Highway MPG vs Violations Per sale"
[combo]: https://github.com/mkain112/TrafficViolations_CaseStudy/blob/master/comboregress.png?raw=true "Combined MPG vs Violations Per sale"
