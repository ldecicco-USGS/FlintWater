## An Analysis on Metropolitans Susceptible to Water Supply Metal Leaching as in the Flint Michigan Incident

###Introduction
As many have heard recently residents of Flint Michigan have been rightly outraged due to the high presence of toxic chemicals including lead in their drinking water. The question arises how did this occur and was it a forseeable incident? The backstory that led up to this incident can be generalized into a few main chapters.

1) Flint had long sourced their water from the Detroit Water and Sewerage Department (DWSD)
2) The city had financial incentive to reduce spending because they were under financial stress
3) Flint went into an agreement with the Karegnondi Water Authority (AWA) and their to be completed source from Lake Huron(end of 2016) 
4) The existing supplier DWSD provided their 12 month notice that their supply contract would end on April 2014
5) The flint river was relied on to supply water in the interim
6) The flint river contained significantly higher levels of chloride than the Detroit water source and no anti-corroding agents were applied

Three main ingredients can be observed leading to this incident.

1) **Incentive**: The city of Flint was under financial stress
2) **Opportunity:** A nearby water source already existed to fill the interim water supply needs
3) **Catalyst:** An aged iron and lead water system + higher than normal corrosive water +  negligence in not adding anti-corroding agents

###Hypothesis

In this analysis we will utilize Census Data as well as US Geological Wate Quality Survey Data to analyse the Flint incident and prevent similar instances. It is not meant to serve as conclusive evidence of any kind. The analysis is merely a laymen's work in progress to raise discussion and feedback on how to better prevent future incidents starting with Flint.

Before we begin let's check for and install any necesary packages for this story

```r
setwd("~/DSTribune/Stories/FlintWaterQuality")
list.of.packages <- c("ggplot2", "acs")
new.packages <- list.of.packages[!(list.of.packages %in% installed.packages()[,"Package"])]
if(length(new.packages)>0) {install.packages(new.packages)}
library(ggplot2)
library(acs)
```

```
## 
## Attaching package: 'acs'
```

```
## The following object is masked from 'package:base':
## 
##     apply
```

#### **Ingredient #1: Incentive**

For the financial piece of this analysis we will be relying upon the [America Community Survey](https://www.census.gov/programs-surveys/acs/) which is operated by the US Census Bureau. Programmatic access to this data is conveniently provided by the [acs package](https://cran.r-project.org/web/packages/acs/acs.pdf) in R authored and maintained by [Ezra Glenn of MIT](https://dusp.mit.edu/faculty/ezra-glenn).



Look at water main leaks and pipes

Water Quality

```r
temp <- tempfile()
download.file("http://waterqualitydata.us/Station/search?countrycode=US&statecode=US%3A26&countycode=US%3A26%3A049&mimeType=kml&zip=yes&sorted=no",temp)
data <- read.table(unz(temp, "station.kml"))
```

```
## Warning in read.table(unz(temp, "station.kml")): incomplete final line
## found by readTableHeader on '/tmp/RtmpRM3LWf/file8c6140aba3a:station.kml'
```

```r
unlink(temp)


download.file(url = "http://waterqualitydata.us/Station/search?countrycode=US&statecode=US%3A26&countycode=US%3A26%3A049&mimeType=kml&zip=yes&sorted=no", destfile = "stationLocations")
unzip("/home/john/DSTribune/Stories/FlintWaterQuality/stationLocations.zip")
```

```
## Warning in unzip("/home/john/DSTribune/Stories/FlintWaterQuality/
## stationLocations.zip"): error 1 in extracting from zip file
```

Comparison of Detroit water to Lake Huron water to Flint River water: pH and chlorides
download chloride data from USGS

ActivityMediaSubdivisionName = Surface Water
ActivityStartDate: filter for last decade
MonitoringLocationIdentifier    (Location filter)
ResultSampleFractionText = Dissolved
value = ResultMeasureValue
ResultStatusIdentifier = Accepted


```r
temp <- tempfile()
download.file(,temp, mode="wb")
```

```
## Error in shQuote(url): argument "url" is missing, with no default
```

```r
con <- unz(temp, "result.csv")
waterQuality <- read.table(con, header=T)
```

```
## Warning in open.connection(file, "rt"): cannot open zip file '/tmp/
## RtmpRM3LWf/file8c63a8d1114'
```

```
## Error in open.connection(file, "rt"): cannot open the connection
```

```r
unlink(temp)

download.file("http://waterqualitydata.us/Station/search?countrycode=US&statecode=US%3A26&countycode=US%3A26%3A049&sampleMedia=Water&characteristicType=Inorganics%2C+Major%2C+Non-metals&characteristicName=Chloride&mimeType=csv&zip=yes&sorted=no", destfile = "waterQualityMI")
unzip(zipfile = "result.csv")
```

```
## Warning in unzip(zipfile = "result.csv"): error 1 in extracting from zip
## file
```

```r
dd <- read.table("result.csv", sep=",", header=T)
```

```
## Warning in file(file, "rt"): cannot open file 'result.csv': No such file or
## directory
```

```
## Error in file(file, "rt"): cannot open the connection
```

