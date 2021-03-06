Forecast with Single Confidence Interval Band
=============================================
By [Jay Thoden van Velzen](http://scn.sap.com/people/jay.thodenvanvelzen)

![Forecast with Single Confidence Interval](https://github.com/SAP/lumira-extension-viz/blob/master/Forecast_Single_Confidence_Interval/ForecastSingleConfidence.PNG)

This chart shows the visualization of actuals and forecast with a single confidence interval. Note that this chart doesn't
perform the forecast itself, but a visualization extension that allows to show the results of such forecast with the appropriate
confidence interval. It is important to include a confidence interval with the forecast to give a sense of how reliable/accurate/precise the forecast really is. You do not want to have your end user misunderstand the forecast and make
important decisions based on it, when the confidence interval could have shown there was a great deal of uncertainty involved with the forecast.

Have a look at the included data file for the required format. This has a seasonal aspect to it, which is reflected as well in the forecast.

Use of SVG Path mini language
-----------------------------
The chart doesn't look terribly complex, but I ran into an interesting issue: if you look at the data file, there are a large number of rows for columns that have no data. That is natural for a forecast, as first you'll have actuals, and then you have the forecast and the values for the confidence interval. Normal  d3.svg.line()  doesn't really work, then, because that really expects the dataset to be complete. (You could do it that way, but since null values are interpreted as zeroes, you get a weird "spike" to the 0 on the x-axis right before the forecast/confidence interval begins.) So, I am using the SVG path mini language directly. This means, then, generating a string of coordinates for the lines to be drawn. That looks something like this: M0,0L10,0L10,10L10,0L0,0 which would create a little square.  d3.svg.line()  and  d3.svg.area()  are basically helper functions around this.

Data file
---------
The data file was given to me by a colleague who had seen the forecast chart with 80 and 95% confidence intervals and wondered if we could do the same with just a single confidence interval, and sent me a sample file. Just like with the other chart, the forecast itself would need to be produced in a predictive/statistical tool (AFL PAL, Predictive Analysis, InfiniteInsight, R, SAS, SPSS, etc.) to do the calculations. 

Versioning
-------------------------------------------
SAP Lumira development progresses quickly, and this extension was originally built in a previous version. The extension works just fine in SAP Lumira 1.21, but VizPacker can't read this original profile file anymore and returns undefined. 

However, the .profile file for this has now been updated to correct this and should work just fine in newer VizPacker versions

Files
---------

* `Forecast Single Confidence.lums` - SAP Lumira file
* `forecast_city.csv` - Sample dataset
* `sap.viz.ext.forecastsingleconfidence.zip` - Extension file 

Data Binding
-------------------------------------------
<strong>Measures</strong>
* Measure
* PILower
* PIUpper
 
<strong>Dimensions</strong>
* YearMonthString
* Month
* Type
* Model
* ForecastBy

Resources
---------
* Blog [SAP Lumira Chart Extensions with a Predictive Flavor](http://scn.sap.com/community/lumira/blog/2015/01/27/sap-lumira-chart-extensions-with-a-predictive-flavor)
