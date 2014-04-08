---
title       : Interactive charts with googleVis in R
subtitle    : Tokyo R User Group, 17 April 2014
author      : Markus Gesmann 
job         : Maintainer and co-author of googleVis
framework   : io2012        # {io2012, html5slides, shower, dzslides, ...}
highlighter : highlight.js  # {highlight.js, prettify, highlight}
hitheme     : tomorrow      # 
widgets     : []            # {mathjax, quiz, bootstrap}
mode        : selfcontained # {standalone, draft}
license     : by-nc-sa
github      :
  user      : mages
  repo      : googleVis_Tokyo_April_2014
---

<style>
.title-slide {
  background-color: #FFFFFF;
}

.title-slide hgroup > h1{
 font-family: 'Oswald', 'Helvetica', sanserif; 
}

.title-slide hgroup > h1, 
.title-slide hgroup > h2 {
  color: 535E43;  /* ; #EF5150*/
}
</style>


## Disclaimer

1. I am an autodidact
2. What I present here works for me
3. Read and follow the official [Google Chart API documentation](https://developers.google.com/chart/) and [Terms of Service](https://developers.google.com/readme/terms)
4. Sometimes you have to re-load this presentation for the charts and all slides to appear

---

## Agenda

* Introduction and motivation
* Google Chart Tools
* R package googleVis
  * Concepts of googleVis
  * Recent developments





--- .segue .dark

## Introduction and motivation


--- .class #id 

## Hello, I am Markus Gesmann

* Manager of the Analysis team at [Lloyd's of London](http://www.lloyds.com)
* Mathematican, [University of Cologne](http://www.mi.uni-koeln.de)
* Maintainer and co-author of [ChainLadder](https://code.google.com/p/chainladder/) and [googleVis](http://github.com/mages/googleVis)
* Founder and co-organiser of the [Cologne R user group](http://www.meetup.com/KoelnRUG) and [R in Insurance](http://www.rininsurance.com) conference
* [Blogger](http://lamages.blogspot.com)

---

## I work here: Lloyd's of London

![](assets/img/Exterior.jpg)

---

## The leading specialty insurance market

![](assets/img/interior.jpg)

--- .class #id 

## Hans Rosling: No more boring data

<iframe width="420" height="315" src="http://www.youtube.com/embed/hVimVzgtD6w" frameborder="0" allowfullscreen></iframe>

---

## Motivation for googleVis

* Inspired by Hans Rosling’s talks we wanted to use interactive data visualisation tools to foster the dialogue between data analysts and others
* We wanted moving bubbles charts as well
* The software behind Hans’ talk was bought by Google and integrated as motion charts into their Visualisation API
* Ideally we wanted to use R, a language we knew
* Hence, we had to create an interface between the Google Chart Tools and R

--- .segue .dark

## Google Chart Tools

---

## Introduction to Google Chart Tools

* Google Chart Tools provide a way to visualize data on web sites
* The API makes it easy to create interactive charts
* It uses JavaScript and DataTable / JSON as input
* Output is either HTML5/SVG or Flash
* Browser with internet connection required to display chart
* Please read the Google [Terms of Service](https://developers.google.com/terms/) before you start

---

## Structure of Google Charts

The chart code has five generic parts:

1. References to Google's AJAX and Visualisation API
2. Data to visualize as a DataTable
3. Instance call to create the chart
4. Method call to draw the chart including options
5. HTML &lt;div&gt; element to add the chart to the page

---

## How hard can it be?

* Transform data into JSON object 
* Wrap some HTML and JavaScript around it 
* Thus, googleVis started life in August 2010


----

## Motion chart example


```r
plot(gvisMotionChart(Fruits, "Fruit", "Year",
                     options=list(width=600, height=400)))
```

<!-- MotionChart generated in R 3.0.2 by googleVis 0.5.0-4 package -->
<!-- Tue Apr  8 19:38:56 2014 -->


<!-- jsHeader -->
<script type="text/javascript">
 
// jsData 
function gvisDataMotionChartID2d46c24fde8 () {
var data = new google.visualization.DataTable();
var datajson =
[
 [
 "Apples",
2008,
"West",
98,
78,
20,
"2008-12-31" 
],
[
 "Apples",
2009,
"West",
111,
79,
32,
"2009-12-31" 
],
[
 "Apples",
2010,
"West",
89,
76,
13,
"2010-12-31" 
],
[
 "Oranges",
2008,
"East",
96,
81,
15,
"2008-12-31" 
],
[
 "Bananas",
2008,
"East",
85,
76,
9,
"2008-12-31" 
],
[
 "Oranges",
2009,
"East",
93,
80,
13,
"2009-12-31" 
],
[
 "Bananas",
2009,
"East",
94,
78,
16,
"2009-12-31" 
],
[
 "Oranges",
2010,
"East",
98,
91,
7,
"2010-12-31" 
],
[
 "Bananas",
2010,
"East",
81,
71,
10,
"2010-12-31" 
] 
];
data.addColumn('string','Fruit');
data.addColumn('number','Year');
data.addColumn('string','Location');
data.addColumn('number','Sales');
data.addColumn('number','Expenses');
data.addColumn('number','Profit');
data.addColumn('string','Date');
data.addRows(datajson);
return(data);
}
 
// jsDrawChart
function drawChartMotionChartID2d46c24fde8() {
var data = gvisDataMotionChartID2d46c24fde8();
var options = {};
options["width"] =    600;
options["height"] =    400;

    var chart = new google.visualization.MotionChart(
    document.getElementById('MotionChartID2d46c24fde8')
    );
    chart.draw(data,options);
    

}
  
 
// jsDisplayChart
(function() {
var pkgs = window.__gvisPackages = window.__gvisPackages || [];
var callbacks = window.__gvisCallbacks = window.__gvisCallbacks || [];
var chartid = "motionchart";
  
// Manually see if chartid is in pkgs (not all browsers support Array.indexOf)
var i, newPackage = true;
for (i = 0; newPackage && i < pkgs.length; i++) {
if (pkgs[i] === chartid)
newPackage = false;
}
if (newPackage)
  pkgs.push(chartid);
  
// Add the drawChart function to the global list of callbacks
callbacks.push(drawChartMotionChartID2d46c24fde8);
})();
function displayChartMotionChartID2d46c24fde8() {
  var pkgs = window.__gvisPackages = window.__gvisPackages || [];
  var callbacks = window.__gvisCallbacks = window.__gvisCallbacks || [];
  window.clearTimeout(window.__gvisLoad);
  // The timeout is set to 100 because otherwise the container div we are
  // targeting might not be part of the document yet
  window.__gvisLoad = setTimeout(function() {
  var pkgCount = pkgs.length;
  google.load("visualization", "1", { packages:pkgs, callback: function() {
  if (pkgCount != pkgs.length) {
  // Race condition where another setTimeout call snuck in after us; if
  // that call added a package, we must not shift its callback
  return;
}
while (callbacks.length > 0)
callbacks.shift()();
} });
}, 100);
}
 
// jsFooter
</script>
 
<!-- jsChart -->  
<script type="text/javascript" src="https://www.google.com/jsapi?callback=displayChartMotionChartID2d46c24fde8"></script>
 
<!-- divChart -->
  
<div id="MotionChartID2d46c24fde8"
  style="width: 600px; height: 400px;">
</div>


--- .segue .dark

## R package googleVis 

--- 

## Overview of googleVis

* [googleVis](http://github.com/mages/googleVis) is a package for [R](http://www.r-poject.org/) and provides an interface between R and the [Google Chart Tools](https://developers.google.com/chart/)

* The functions of the package allow users to visualize data with the Google Chart Tools without uploading their data to Google

* The output of googleVis functions is html code that contains the data and references to JavaScript functions hosted by Google

* To view the output a browser with an internet connection is required, the actual chart is rendered in the browser; some charts require Flash

* See also: **Using the Google Visualisation API with R**, 
  [The R Journal, 3(2):40-44, December 2011](http://journal.r-project.org/archive/2011-2/RJournal_2011-2_Gesmann+de~Castillo.pdf) and googleVis [package vignette](http://cran.r-project.org/web/packages/googleVis/vignettes/googleVis.pdf)

---

## googleVis version 0.5.0 provides interfaces to 

* Flash based
  * Motion Charts
  * Annotated Time Lines
  * Geo Maps
* HMTL5/SVG based
  * Maps, Geo Charts and Intensity Maps,
  * Tables, Gauges, Tree Maps, Timelines,
  * Line-, Bar-, Column-, Area- and Combo Charts,
  * Scatter-, Bubble-, Candlestick-, Pie- and Org Charts,
  * Annotation-, Calendar-, Histogram and Sankey Charts
* Support for roles and trendlines

Run ```demo(googleVis)``` to see examples of all charts and read the [vignette](http://cran.r-project.org/web/packages/googleVis/vignettes/googleVis.pdf) for more details.

----

## Key ideas of googleVis

* Create wrapper functions in R which generate html files with references to Google's Chart Tools API
* Transform R data frames into [JSON](http://www.json.org/) objects with [RJSONIO](http://www.omegahat.org/RJSONIO/)


```r
library(RJSONIO)
dat <- data.frame(x = LETTERS[1:2], y = 1:2)
cat(toJSON(dat))
```

```
## {
##  "x": [ "A", "B" ],
## "y": [ 1, 2 ] 
## }
```

* Display the HTML output with the R HTTP help server

---

## The googleVis concept

* Charts: *'gvis' + ChartType*
* For a motion chart we have


```r
M <- gvisMotionChart(data, idvar='id', timevar='date', 
                     options=list(), chartid)
```


* Output of googleVis is a list of list

* Display the chart by simply plotting the output: ```plot(M)```
* Plot will generate a temporary html-file and open it in a new browser window 
* Specific parts can be extracted, e.g. 
  * the chart: ```M$html$chart``` or 
  * data: ```M$html$chart["jsData"]```

---

## gvis-Chart structure

List structure:

<img height=350 src="https://dl.dropbox.com/u/7586336/googleVisExamples/gvisObject.png" alt="gvis object structure" />

---

## Scatter chart


```r
df <- data.frame(year=1:11, x=1:11)
plot(gvisScatterChart(df,options=list(lineWidth=2)))
```

<!-- ScatterChart generated in R 3.0.2 by googleVis 0.5.0-4 package -->
<!-- Tue Apr  8 19:38:56 2014 -->


<!-- jsHeader -->
<script type="text/javascript">
 
// jsData 
function gvisDataScatterChartID2d47099c1cf () {
var data = new google.visualization.DataTable();
var datajson =
[
 [
 1,
1 
],
[
 2,
2 
],
[
 3,
3 
],
[
 4,
4 
],
[
 5,
5 
],
[
 6,
6 
],
[
 7,
7 
],
[
 8,
8 
],
[
 9,
9 
],
[
 10,
10 
],
[
 11,
11 
] 
];
data.addColumn('number','year');
data.addColumn('number','x');
data.addRows(datajson);
return(data);
}
 
// jsDrawChart
function drawChartScatterChartID2d47099c1cf() {
var data = gvisDataScatterChartID2d47099c1cf();
var options = {};
options["allowHtml"] = true;
options["lineWidth"] =      2;

    var chart = new google.visualization.ScatterChart(
    document.getElementById('ScatterChartID2d47099c1cf')
    );
    chart.draw(data,options);
    

}
  
 
// jsDisplayChart
(function() {
var pkgs = window.__gvisPackages = window.__gvisPackages || [];
var callbacks = window.__gvisCallbacks = window.__gvisCallbacks || [];
var chartid = "corechart";
  
// Manually see if chartid is in pkgs (not all browsers support Array.indexOf)
var i, newPackage = true;
for (i = 0; newPackage && i < pkgs.length; i++) {
if (pkgs[i] === chartid)
newPackage = false;
}
if (newPackage)
  pkgs.push(chartid);
  
// Add the drawChart function to the global list of callbacks
callbacks.push(drawChartScatterChartID2d47099c1cf);
})();
function displayChartScatterChartID2d47099c1cf() {
  var pkgs = window.__gvisPackages = window.__gvisPackages || [];
  var callbacks = window.__gvisCallbacks = window.__gvisCallbacks || [];
  window.clearTimeout(window.__gvisLoad);
  // The timeout is set to 100 because otherwise the container div we are
  // targeting might not be part of the document yet
  window.__gvisLoad = setTimeout(function() {
  var pkgCount = pkgs.length;
  google.load("visualization", "1", { packages:pkgs, callback: function() {
  if (pkgCount != pkgs.length) {
  // Race condition where another setTimeout call snuck in after us; if
  // that call added a package, we must not shift its callback
  return;
}
while (callbacks.length > 0)
callbacks.shift()();
} });
}, 100);
}
 
// jsFooter
</script>
 
<!-- jsChart -->  
<script type="text/javascript" src="https://www.google.com/jsapi?callback=displayChartScatterChartID2d47099c1cf"></script>
 
<!-- divChart -->
  
<div id="ScatterChartID2d47099c1cf"
  style="width: 600px; height: 500px;">
</div>


---

## Add additional columns to define roles


```r
df <- data.frame(year=1:11, x=1:11,
                 x.scope=c(rep(TRUE, 8), rep(FALSE, 3)),
                 y=11:1, y.html.tooltip=LETTERS[11:1],                 
                 y.certainty=c(rep(TRUE, 5), rep(FALSE, 6)),
                 y.emphasis=c(rep(FALSE, 4), rep(TRUE, 7)))
plot(gvisScatterChart(df,options=list(lineWidth=2)))
```

<!-- ScatterChart generated in R 3.0.2 by googleVis 0.5.0-4 package -->
<!-- Tue Apr  8 19:38:56 2014 -->


<!-- jsHeader -->
<script type="text/javascript">
 
// jsData 
function gvisDataScatterChartID2d47e8336c9 () {
var data = new google.visualization.DataTable();
var datajson =
[
 [
 1,
1,
true,
11,
"K",
true,
false 
],
[
 2,
2,
true,
10,
"J",
true,
false 
],
[
 3,
3,
true,
9,
"I",
true,
false 
],
[
 4,
4,
true,
8,
"H",
true,
false 
],
[
 5,
5,
true,
7,
"G",
true,
true 
],
[
 6,
6,
true,
6,
"F",
false,
true 
],
[
 7,
7,
true,
5,
"E",
false,
true 
],
[
 8,
8,
true,
4,
"D",
false,
true 
],
[
 9,
9,
false,
3,
"C",
false,
true 
],
[
 10,
10,
false,
2,
"B",
false,
true 
],
[
 11,
11,
false,
1,
"A",
false,
true 
] 
];
data.addColumn('number','year');
data.addColumn('number','x');
data.addColumn({type: 'boolean', role: 'scope'});
data.addColumn('number','y');
data.addColumn({type: 'string', role: 'tooltip', 'p': {'html': true}});
data.addColumn({type: 'boolean', role: 'certainty'});
data.addColumn({type: 'boolean', role: 'emphasis'});
data.addRows(datajson);
return(data);
}
 
// jsDrawChart
function drawChartScatterChartID2d47e8336c9() {
var data = gvisDataScatterChartID2d47e8336c9();
var options = {};
options["allowHtml"] = true;
options["lineWidth"] =      2;

    var chart = new google.visualization.ScatterChart(
    document.getElementById('ScatterChartID2d47e8336c9')
    );
    chart.draw(data,options);
    

}
  
 
// jsDisplayChart
(function() {
var pkgs = window.__gvisPackages = window.__gvisPackages || [];
var callbacks = window.__gvisCallbacks = window.__gvisCallbacks || [];
var chartid = "corechart";
  
// Manually see if chartid is in pkgs (not all browsers support Array.indexOf)
var i, newPackage = true;
for (i = 0; newPackage && i < pkgs.length; i++) {
if (pkgs[i] === chartid)
newPackage = false;
}
if (newPackage)
  pkgs.push(chartid);
  
// Add the drawChart function to the global list of callbacks
callbacks.push(drawChartScatterChartID2d47e8336c9);
})();
function displayChartScatterChartID2d47e8336c9() {
  var pkgs = window.__gvisPackages = window.__gvisPackages || [];
  var callbacks = window.__gvisCallbacks = window.__gvisCallbacks || [];
  window.clearTimeout(window.__gvisLoad);
  // The timeout is set to 100 because otherwise the container div we are
  // targeting might not be part of the document yet
  window.__gvisLoad = setTimeout(function() {
  var pkgCount = pkgs.length;
  google.load("visualization", "1", { packages:pkgs, callback: function() {
  if (pkgCount != pkgs.length) {
  // Race condition where another setTimeout call snuck in after us; if
  // that call added a package, we must not shift its callback
  return;
}
while (callbacks.length > 0)
callbacks.shift()();
} });
}, 100);
}
 
// jsFooter
</script>
 
<!-- jsChart -->  
<script type="text/javascript" src="https://www.google.com/jsapi?callback=displayChartScatterChartID2d47e8336c9"></script>
 
<!-- divChart -->
  
<div id="ScatterChartID2d47e8336c9"
  style="width: 600px; height: 500px;">
</div>


---

## Line chart with options set


```r
df <- data.frame(label=c("US", "GB", "BR"), val1=c(1,3,4), val2=c(23,12,32))
Line <- gvisLineChart(df, xvar="label", yvar=c("val1","val2"),
        options=list(title="Hello World", legend="bottom",
                titleTextStyle="{color:'red', fontSize:18}",                         
                vAxis="{gridlines:{color:'red', count:3}}",
                hAxis="{title:'My Label', titleTextStyle:{color:'blue'}}",
                series="[{color:'green', targetAxisIndex: 0}, 
                         {color: 'blue',targetAxisIndex:1}]",
                vAxes="[{title:'Value 1 (%)', format:'##,######%'}, 
                                  {title:'Value 2 (\U00A3)'}]",                          
                curveType="function", width=500, height=300                         
                ))
```

Options in googleVis have to follow the Google Chart API options

---

## Line chart with options

```r
plot(Line)
```

<!-- LineChart generated in R 3.0.2 by googleVis 0.5.0-4 package -->
<!-- Tue Apr  8 19:38:56 2014 -->


<!-- jsHeader -->
<script type="text/javascript">
 
// jsData 
function gvisDataLineChartID2d458820702 () {
var data = new google.visualization.DataTable();
var datajson =
[
 [
 "US",
1,
23 
],
[
 "GB",
3,
12 
],
[
 "BR",
4,
32 
] 
];
data.addColumn('string','label');
data.addColumn('number','val1');
data.addColumn('number','val2');
data.addRows(datajson);
return(data);
}
 
// jsDrawChart
function drawChartLineChartID2d458820702() {
var data = gvisDataLineChartID2d458820702();
var options = {};
options["allowHtml"] = true;
options["title"] = "Hello World";
options["legend"] = "bottom";
options["titleTextStyle"] = {color:'red', fontSize:18};
options["vAxis"] = {gridlines:{color:'red', count:3}};
options["hAxis"] = {title:'My Label', titleTextStyle:{color:'blue'}};
options["series"] = [{color:'green', targetAxisIndex: 0}, 
                         {color: 'blue',targetAxisIndex:1}];
options["vAxes"] = [{title:'Value 1 (%)', format:'##,######%'}, 
                                  {title:'Value 2 (£)'}];
options["curveType"] = "function";
options["width"] =    500;
options["height"] =    300;

    var chart = new google.visualization.LineChart(
    document.getElementById('LineChartID2d458820702')
    );
    chart.draw(data,options);
    

}
  
 
// jsDisplayChart
(function() {
var pkgs = window.__gvisPackages = window.__gvisPackages || [];
var callbacks = window.__gvisCallbacks = window.__gvisCallbacks || [];
var chartid = "corechart";
  
// Manually see if chartid is in pkgs (not all browsers support Array.indexOf)
var i, newPackage = true;
for (i = 0; newPackage && i < pkgs.length; i++) {
if (pkgs[i] === chartid)
newPackage = false;
}
if (newPackage)
  pkgs.push(chartid);
  
// Add the drawChart function to the global list of callbacks
callbacks.push(drawChartLineChartID2d458820702);
})();
function displayChartLineChartID2d458820702() {
  var pkgs = window.__gvisPackages = window.__gvisPackages || [];
  var callbacks = window.__gvisCallbacks = window.__gvisCallbacks || [];
  window.clearTimeout(window.__gvisLoad);
  // The timeout is set to 100 because otherwise the container div we are
  // targeting might not be part of the document yet
  window.__gvisLoad = setTimeout(function() {
  var pkgCount = pkgs.length;
  google.load("visualization", "1", { packages:pkgs, callback: function() {
  if (pkgCount != pkgs.length) {
  // Race condition where another setTimeout call snuck in after us; if
  // that call added a package, we must not shift its callback
  return;
}
while (callbacks.length > 0)
callbacks.shift()();
} });
}, 100);
}
 
// jsFooter
</script>
 
<!-- jsChart -->  
<script type="text/javascript" src="https://www.google.com/jsapi?callback=displayChartLineChartID2d458820702"></script>
 
<!-- divChart -->
  
<div id="LineChartID2d458820702"
  style="width: 500px; height: 300px;">
</div>


---

## Displaying geographical information

Plot countries' S&P credit rating sourced from Wikipedia

```r
library(XML)
url <- "http://en.wikipedia.org/wiki/List_of_countries_by_credit_rating"
x <- readHTMLTable(readLines(url), which=3)
levels(x$Rating) <- substring(levels(x$Rating), 4, 
                            nchar(levels(x$Rating)))
x$Ranking <- x$Rating
levels(x$Ranking) <- nlevels(x$Rating):1
x$Ranking <- as.character(x$Ranking)
x$Rating <- paste(x$Country, x$Rating, sep=": ")
G <- gvisGeoChart(x, "Country", "Ranking", hovervar="Rating",
                options=list(gvis.editor="S&P",
                             projection="kavrayskiy-vii",
                             colorAxis="{colors:['#91BFDB', '#FC8D59']}"))
```


---

## Chart countries' S&P credit rating


```r
plot(G)
```

<!-- GeoChart generated in R 3.0.2 by googleVis 0.5.0-4 package -->
<!-- Tue Apr  8 19:39:00 2014 -->


<!-- jsHeader -->
<script type="text/javascript">
 
// jsData 
function gvisDataGeoChartID2d4409a41b3 () {
var data = new google.visualization.DataTable();
var datajson =
[
 [
 "Albania",
"Albania: 1",
6 
],
[
 "Angola",
"Angola: a3",
5 
],
[
 "Argentina",
"Argentina: 3",
8 
],
[
 "Armenia",
"Armenia: a2",
4 
],
[
 "Australia",
"Australia: aa",
1 
],
[
 "Austria",
"Austria: aa",
1 
],
[
 "Azerbaijan",
"Azerbaijan: aa3",
10 
],
[
 "Bahamas",
"Bahamas: 3",
8 
],
[
 "Bahrain",
"Bahrain: aa1",
9 
],
[
 "Bangladesh",
"Bangladesh: a3",
5 
],
[
 "Barbados",
"Barbados: aa3",
10 
],
[
 "Belarus",
"Belarus: 3",
8 
],
[
 "Belgium",
"Belgium: a3",
5 
],
[
 "Belize",
"Belize: 3",
8 
],
[
 "Bermuda",
"Bermuda: a2",
4 
],
[
 "Bolivia",
"Bolivia: a3",
5 
],
[
 "Bosnia and Herzegovina",
"Bosnia and Herzegovina: 3",
8 
],
[
 "Botswana",
"Botswana: 2",
7 
],
[
 "Brazil",
"Brazil: aa2",
2 
],
[
 "Bulgaria",
"Bulgaria: aa2",
2 
],
[
 "Cambodia",
"Cambodia: 2",
7 
],
[
 "Canada",
"Canada: aa",
1 
],
[
 "Cayman Islands",
"Cayman Islands: a3",
5 
],
[
 "Chile",
"Chile: a3",
5 
],
[
 "China",
"China: a3",
5 
],
[
 "Colombia",
"Colombia: aa3",
10 
],
[
 "Costa Rica",
"Costa Rica: aa3",
10 
],
[
 "Croatia",
"Croatia: aa3",
10 
],
[
 "Cuba",
"Cuba: aa1",
9 
],
[
 "Cyprus",
"Cyprus: aa3",
10 
],
[
 "Czech Republic",
"Czech Republic: 1",
6 
],
[
 "Denmark",
"Denmark: aa",
1 
],
[
 "Dominican Republic",
"Dominican Republic: 1",
6 
],
[
 "Ecuador",
"Ecuador: aa1",
9 
],
[
 "Egypt",
"Egypt: aa1",
9 
],
[
 "El Salvador",
"El Salvador: a2",
4 
],
[
 "Estonia",
"Estonia: 1",
6 
],
[
 "Fiji",
"Fiji: 1",
6 
],
[
 "Finland",
"Finland: aa",
1 
],
[
 "France",
"France: a1",
3 
],
[
 "Georgia",
"Georgia: a3",
5 
],
[
 "Germany",
"Germany: aa",
1 
],
[
 "Greece",
"Greece: aa3",
10 
],
[
 "Guatemala",
"Guatemala: a1",
3 
],
[
 "Honduras",
"Honduras: 2",
7 
],
[
 "Hong Kong",
"Hong Kong: a1",
3 
],
[
 "Hungary",
"Hungary: a1",
3 
],
[
 "Iceland",
"Iceland: aa3",
10 
],
[
 "India",
"India: aa3",
10 
],
[
 "Indonesia",
"Indonesia: aa3",
10 
],
[
 "Ireland",
"Ireland: aa3",
10 
],
[
 "Isle of Man",
"Isle of Man: aa",
1 
],
[
 "Israel",
"Israel: 1",
6 
],
[
 "Italy",
"Italy: aa2",
2 
],
[
 "Jamaica",
"Jamaica: 3",
8 
],
[
 "Japan",
"Japan: a3",
5 
],
[
 "Jordan",
"Jordan: a2",
4 
],
[
 "Kazakhstan",
"Kazakhstan: aa2",
2 
],
[
 "Kuwait",
"Kuwait: a2",
4 
],
[
 "Latvia",
"Latvia: aa2",
2 
],
[
 "Lebanon",
"Lebanon: 1",
6 
],
[
 "Lithuania",
"Lithuania: aa1",
9 
],
[
 "Luxembourg",
"Luxembourg: aa",
1 
],
[
 "Macao",
"Macao: a3",
5 
],
[
 "Malaysia",
"Malaysia: 3",
8 
],
[
 "Malta",
"Malta: 1",
6 
],
[
 "Mauritius",
"Mauritius: aa2",
2 
],
[
 "Mexico",
"Mexico: 3",
8 
],
[
 "Moldova",
"Moldova: 3",
8 
],
[
 "Mongolia",
"Mongolia: 1",
6 
],
[
 "Montenegro",
"Montenegro: a3",
5 
],
[
 "Morocco",
"Morocco: a1",
3 
],
[
 "Netherlands",
"Netherlands: aa",
1 
],
[
 "New Zealand",
"New Zealand: aa",
1 
],
[
 "Nicaragua",
"Nicaragua: 3",
8 
],
[
 "Norway",
"Norway: aa",
1 
],
[
 "Oman",
"Oman: 1",
6 
],
[
 "Pakistan",
"Pakistan: aa1",
9 
],
[
 "Panama",
"Panama: aa2",
2 
],
[
 "Papua New Guinea",
"Papua New Guinea: 1",
6 
],
[
 "Paraguay",
"Paraguay: 1",
6 
],
[
 "Peru",
"Peru: aa2",
2 
],
[
 "Philippines",
"Philippines: aa3",
10 
],
[
 "Poland",
"Poland: 2",
7 
],
[
 "Portugal",
"Portugal: a3",
5 
],
[
 "Qatar",
"Qatar: a2",
4 
],
[
 "Romania",
"Romania: aa3",
10 
],
[
 "Russia",
"Russia: aa1",
9 
],
[
 "Saudi Arabia",
"Saudi Arabia: a3",
5 
],
[
 "Senegal",
"Senegal: 1",
6 
],
[
 "Serbia",
"Serbia: 1",
6 
],
[
 "Singapore",
"Singapore: aa",
1 
],
[
 "Slovakia",
"Slovakia: 1",
6 
],
[
 "Slovenia",
"Slovenia: a1",
3 
],
[
 "South Africa",
"South Africa: aa1",
9 
],
[
 "South Korea",
"South Korea: a3",
5 
],
[
 "Spain",
"Spain: aa2",
2 
],
[
 "Sri Lanka",
"Sri Lanka: 1",
6 
],
[
 "St. Vincent & the Grenadines",
"St. Vincent & the Grenadines: 1",
6 
],
[
 "Suriname",
"Suriname: 1",
6 
],
[
 "Sweden",
"Sweden: aa",
1 
],
[
 "Switzerland",
"Switzerland: aa",
1 
],
[
 "Taiwan",
"Taiwan: a3",
5 
],
[
 "Thailand",
"Thailand: aa1",
9 
],
[
 "Trinidad and Tobago",
"Trinidad and Tobago: aa1",
9 
],
[
 "Tunisia",
"Tunisia: aa3",
10 
],
[
 "Turkey",
"Turkey: aa3",
10 
],
[
 "Ukraine",
"Ukraine: aa1",
9 
],
[
 "United Arab Emirates",
"United Arab Emirates: a2",
4 
],
[
 "United Kingdom",
"United Kingdom: a1",
3 
],
[
 "United States",
"United States: aa",
1 
],
[
 "Uruguay",
"Uruguay: aa3",
10 
],
[
 "Venezuela",
"Venezuela: 2",
7 
],
[
 "Vietnam",
"Vietnam: 1",
6 
] 
];
data.addColumn('string','Country');
data.addColumn('string','Rating');
data.addColumn('number','Ranking');
data.addRows(datajson);
return(data);
}
 
// jsDrawChart
function drawChartGeoChartID2d4409a41b3() {
var data = gvisDataGeoChartID2d4409a41b3();
var options = {};
options["width"] =    556;
options["height"] =    347;
options["projection"] = "kavrayskiy-vii";
options["colorAxis"] = {colors:['#91BFDB', '#FC8D59']};

    chartGeoChartID2d4409a41b3 = new google.visualization.ChartWrapper({
    dataTable: data,       
    chartType: 'GeoChart',
    containerId: 'GeoChartID2d4409a41b3',
    options: options
    });
    chartGeoChartID2d4409a41b3.draw();
    

}

  function openEditorGeoChartID2d4409a41b3() {
  var editor = new google.visualization.ChartEditor();
  google.visualization.events.addListener(editor, 'ok',
  function() { 
  chartGeoChartID2d4409a41b3 = editor.getChartWrapper();  
  chartGeoChartID2d4409a41b3.draw(document.getElementById('GeoChartID2d4409a41b3')); 
  }); 
  editor.openDialog(chartGeoChartID2d4409a41b3);
  }
    
 
// jsDisplayChart
(function() {
var pkgs = window.__gvisPackages = window.__gvisPackages || [];
var callbacks = window.__gvisCallbacks = window.__gvisCallbacks || [];
var chartid = "charteditor";
  
// Manually see if chartid is in pkgs (not all browsers support Array.indexOf)
var i, newPackage = true;
for (i = 0; newPackage && i < pkgs.length; i++) {
if (pkgs[i] === chartid)
newPackage = false;
}
if (newPackage)
  pkgs.push(chartid);
  
// Add the drawChart function to the global list of callbacks
callbacks.push(drawChartGeoChartID2d4409a41b3);
})();
function displayChartGeoChartID2d4409a41b3() {
  var pkgs = window.__gvisPackages = window.__gvisPackages || [];
  var callbacks = window.__gvisCallbacks = window.__gvisCallbacks || [];
  window.clearTimeout(window.__gvisLoad);
  // The timeout is set to 100 because otherwise the container div we are
  // targeting might not be part of the document yet
  window.__gvisLoad = setTimeout(function() {
  var pkgCount = pkgs.length;
  google.load("visualization", "1", { packages:pkgs, callback: function() {
  if (pkgCount != pkgs.length) {
  // Race condition where another setTimeout call snuck in after us; if
  // that call added a package, we must not shift its callback
  return;
}
while (callbacks.length > 0)
callbacks.shift()();
} });
}, 100);
}
 
// jsFooter
</script>
 
<!-- jsChart -->  
<script type="text/javascript" src="https://www.google.com/jsapi?callback=displayChartGeoChartID2d4409a41b3"></script>
 
<!-- divChart -->
<input type='button' onclick='openEditorGeoChartID2d4409a41b3()' value='S&P'/>  
<div id="GeoChartID2d4409a41b3"
  style="width: 556px; height: 347px;">
</div>


---

## Geo chart with markers
Display earth quakes in Japan of last 30 days

```r
library(XML)
eq <- read.csv("http://earthquake.usgs.gov/earthquakes/feed/v0.1/summary/2.5_week.csv")
eq$loc=paste(eq$Latitude, eq$Longitude, sep=":")

G <- gvisGeoChart(eq, "loc", "Depth", "Magnitude",
                   options=list(displayMode="Markers", 
                   colorAxis="{colors:['purple', 'red', 'orange', 'grey']}", 
                   region="JP",
                   backgroundColor="lightblue"))
```


---

## Geo chart of earth quakes

```r
plot(G)
```

<!-- GeoChart generated in R 3.0.2 by googleVis 0.5.0-4 package -->
<!-- Tue Apr  8 19:39:01 2014 -->


<!-- jsHeader -->
<script type="text/javascript">
 
// jsData 
function gvisDataGeoChartID2d44f4f6fe7 () {
var data = new google.visualization.DataTable();
var datajson =
[
 [
 -33.609,
179.347,
29.9,
4.8 
],
[
 60.539,
-142.73,
3.7,
2.7 
],
[
 36.268,
141.876,
28.1,
4.9 
],
[
 -4.325,
150.315,
462.2,
4.6 
],
[
 19.383,
-155.272,
2.4,
2.6 
],
[
 -34.395,
-72.522,
21.3,
4.6 
],
[
 47.054,
152.852,
79.6,
4.5 
],
[
 -5.425,
153.129,
41.5,
4.5 
],
[
 -20.571,
-71.028,
14.6,
4.4 
],
[
 -20.486,
-70.933,
7.1,
5.7 
],
[
 19.59,
-65.301,
77,
3.3 
],
[
 17.872,
-94.916,
58.3,
4.5 
],
[
 -20.599,
-70.78,
15.1,
4.5 
],
[
 60.141,
-153.841,
100,
2.8 
],
[
 -20.521,
-70.639,
17.1,
5.2 
],
[
 -20.53,
-70.683,
16.2,
5 
],
[
 -19.901,
-70.856,
17.3,
5 
],
[
 31.876,
-116.199,
13.1,
3.2 
],
[
 -19.777,
-70.563,
26.8,
4.6 
],
[
 35.92,
-97.244,
6,
2.6 
],
[
 -5.684,
152.865,
40,
4.2 
],
[
 -7.393,
119.879,
439.7,
4.6 
],
[
 46.124,
-119.025,
0.2,
2.7 
],
[
 35.891,
-97.269,
5.3,
2.9 
],
[
 37.352,
138.781,
13.4,
4.7 
],
[
 44.623,
6.759,
10,
4.7 
],
[
 33.276,
-116.832,
8.4,
2.5 
],
[
 41.738,
-120.03,
16.1,
2.7 
],
[
 35.891,
-97.27,
5.3,
2.6 
],
[
 35.893,
-97.293,
5.3,
3.1 
],
[
 -20.133,
-70.428,
29.4,
4.9 
],
[
 -23.202,
-175.369,
78.4,
4.7 
],
[
 62.143,
-152.1,
100,
2.8 
],
[
 12.859,
120.895,
53.8,
4.8 
],
[
 18.627,
-64.829,
31,
2.8 
],
[
 35.893,
-97.293,
5,
2.5 
],
[
 35.892,
-97.29,
5,
2.6 
],
[
 35.89,
-97.273,
5.2,
4.2 
],
[
 -8.216,
-71.579,
559.7,
5.1 
],
[
 -6.697,
154.795,
82.6,
4.8 
],
[
 -20.141,
-70.914,
10,
5.1 
],
[
 -20.144,
-70.835,
11.3,
5.4 
],
[
 -20.157,
-70.867,
7.9,
5.8 
],
[
 14.537,
-92.57,
73.2,
4.7 
],
[
 17.457,
-94.495,
142.4,
4.5 
],
[
 36.379,
-96.95,
5,
2.5 
],
[
 -7.048,
131.6,
35,
4.8 
],
[
 -20.509,
-70.983,
14.9,
4.8 
],
[
 50.481,
156.214,
78.8,
5.4 
],
[
 17.158,
-84.727,
16.6,
4.4 
],
[
 28.816,
130.003,
10,
4.7 
],
[
 53.19,
171.009,
24.8,
5.3 
],
[
 19.059,
-67.636,
9,
2.7 
],
[
 -20.7,
-70.947,
14.2,
4.9 
],
[
 36.215,
-89.41,
6.1,
3.1 
],
[
 18.924,
-66.657,
59,
2.7 
],
[
 36.285,
-96.961,
8,
3 
],
[
 52.453,
-169.004,
17.5,
3.1 
],
[
 45.398,
-122.904,
19.5,
3.3 
],
[
 36.822,
-98.23,
8.4,
3.5 
],
[
 -20.088,
-69.369,
86.3,
4.2 
],
[
 36.033,
-97.095,
6.9,
2.7 
],
[
 -20.022,
-177.578,
413.1,
4.6 
],
[
 35.938,
-97.259,
3.5,
2.9 
],
[
 32.763,
60.044,
10.2,
4.1 
],
[
 60.526,
-147.057,
12.2,
3.3 
],
[
 -19.816,
-70.49,
28.4,
4.2 
],
[
 -20.017,
-177.492,
359.9,
4.4 
],
[
 50.599,
159.947,
36.5,
4.6 
],
[
 60.112,
-153.373,
157.4,
4 
],
[
 19.836,
-155.355,
33,
2.6 
],
[
 -21.518,
-179.023,
578.7,
4.9 
],
[
 50.112,
87.768,
15.4,
4.8 
],
[
 35.893,
-97.264,
5,
2.7 
],
[
 35.89,
-97.269,
5.1,
4.2 
],
[
 35.892,
-97.267,
5,
3 
],
[
 -20.411,
-71.072,
8.3,
5.3 
],
[
 56.757,
-153.564,
17,
3.2 
],
[
 13.981,
-91.869,
62.9,
4.7 
],
[
 51.515,
-176.157,
36.2,
3.6 
],
[
 40.61,
-116.63,
null,
2.6 
],
[
 -19.81,
-70.88,
14.5,
4.1 
],
[
 31.069,
49.735,
10,
4.4 
],
[
 43.089,
-126.648,
10,
2.9 
],
[
 48.515,
153.144,
146.8,
4.4 
],
[
 -20.791,
-70.779,
15.7,
4.8 
],
[
 -19.198,
-173.588,
10,
5.2 
],
[
 -20.878,
-70.682,
21.4,
3.9 
],
[
 25.587,
93.999,
55.2,
4.4 
],
[
 53.139,
153.191,
500.5,
4.2 
],
[
 -17.986,
-178.506,
569.6,
4.4 
],
[
 60.187,
-153.751,
100,
2.6 
],
[
 18.845,
-156.795,
28.7,
2.5 
],
[
 44.727,
-110.771,
4.9,
2.5 
],
[
 44.728,
-110.774,
5.1,
2.8 
],
[
 50.217,
-129.89,
10,
4.5 
],
[
 33.155,
-116.467,
14.7,
2.9 
],
[
 19.346,
-155.217,
7.7,
3 
],
[
 -2.677,
138.332,
46.8,
4.4 
],
[
 59.866,
-149.971,
51.4,
2.7 
],
[
 57.223,
-153.637,
41,
2.5 
],
[
 40.249,
-121.15,
7.4,
2.6 
],
[
 60.311,
-152.966,
100,
2.9 
],
[
 -20.75,
-70.664,
16.2,
4.6 
],
[
 -19.712,
-71.233,
16.8,
4.1 
],
[
 -20.142,
-70.928,
19.9,
3.9 
],
[
 -20.634,
-70.985,
23.2,
4.1 
],
[
 60.328,
-152.214,
87.6,
2.9 
],
[
 40.329,
-124.315,
24.6,
2.6 
],
[
 54.986,
-159.254,
25.6,
3 
],
[
 -16.706,
-173.99,
87.8,
4.7 
],
[
 -20.353,
-70.864,
10,
4.8 
],
[
 18.604,
-67.085,
72,
2.6 
],
[
 36.133,
-97.633,
2.5,
3.8 
],
[
 12.243,
144.091,
10,
4.6 
],
[
 59.043,
-152.826,
100,
2.7 
],
[
 30.95,
56.457,
13.4,
4.1 
],
[
 -20.668,
-70.742,
14.1,
4 
],
[
 -20.309,
-70.792,
10,
4.6 
],
[
 36.081,
-97.548,
6,
2.9 
],
[
 38.854,
17.246,
57.5,
4.9 
],
[
 -20.281,
-70.047,
49.8,
4.6 
],
[
 18.403,
-66.941,
135,
3 
],
[
 55.838,
161.671,
79.3,
4.4 
],
[
 -19.938,
-70.822,
12.5,
4.7 
],
[
 -20.275,
-70.284,
36,
4.6 
],
[
 -20.09,
-70.91,
9.9,
4.8 
],
[
 35.892,
-97.25,
7.9,
2.6 
],
[
 -20.131,
-70.445,
19,
5.3 
],
[
 -20.632,
-70.691,
17.7,
4.7 
],
[
 36.587,
-97.607,
2.8,
2.5 
],
[
 -20.591,
-71.034,
6.7,
4.1 
],
[
 -20.672,
-70.497,
32.5,
5 
],
[
 -20.781,
-70.686,
22.9,
4.8 
],
[
 18.809,
-64.439,
59,
3.2 
],
[
 -3.815,
142.005,
62.6,
5.2 
],
[
 47.156,
147.426,
302.5,
4.7 
],
[
 61.275,
-148.185,
31.2,
2.5 
],
[
 36.284,
-97.546,
5,
3 
],
[
 -32.7,
-71.378,
32.2,
5.4 
],
[
 -19.918,
-71.205,
20.1,
4.3 
],
[
 -19.975,
-71.077,
15.9,
4.3 
],
[
 -19.743,
-70.985,
16,
4.2 
],
[
 39.219,
142.438,
42.6,
5.3 
],
[
 -20.023,
-70.934,
11.8,
4.4 
],
[
 58.836,
-152.974,
66,
3.2 
],
[
 -20.052,
-70.527,
25.3,
5 
],
[
 53.301,
-164.153,
25.6,
2.5 
],
[
 18.41,
-64.347,
4,
3.2 
],
[
 28.155,
103.641,
26.2,
5.4 
],
[
 -53.59,
24.753,
10,
5.2 
],
[
 35.913,
-97.281,
1.9,
2.5 
],
[
 51.185,
-178.185,
47.5,
4.7 
],
[
 -22.53,
-174.092,
13.9,
4.8 
],
[
 -20.612,
-70.798,
18.5,
4 
],
[
 60.01,
-152.736,
100,
2.6 
],
[
 60.382,
-152.549,
100,
2.5 
],
[
 -16.486,
-74.157,
24.4,
4.7 
],
[
 19.256,
-155.239,
30.3,
2.7 
],
[
 37.234,
23.769,
107,
5.5 
],
[
 19.115,
-66.402,
36,
2.6 
],
[
 35.889,
-97.283,
5,
3.4 
],
[
 -20.063,
-70.844,
18.6,
4.6 
],
[
 -19.91,
-70.882,
11.5,
4.1 
],
[
 -19.686,
-70.94,
9.9,
4.2 
],
[
 32.671,
-115.848,
7.7,
2.6 
],
[
 -20.42,
-70.854,
10,
4.9 
],
[
 -19.923,
-70.938,
19.7,
4.8 
],
[
 -19.774,
-70.998,
24,
4.2 
],
[
 38.82,
-122.761,
3.1,
2.7 
],
[
 51.254,
-177.918,
23.5,
2.9 
],
[
 -10.53,
161.672,
63.8,
6 
],
[
 36.802,
-97.746,
5,
2.7 
],
[
 18.346,
-67.431,
11,
2.6 
],
[
 -20.611,
-70.682,
17.6,
5.2 
],
[
 -31.51,
-70.357,
94.5,
5.4 
],
[
 -20.038,
-70.997,
13.1,
5.1 
],
[
 37.346,
-113.8,
-0.7,
3.5 
],
[
 -36.518,
-96.748,
10,
4.7 
],
[
 36.527,
70.184,
200,
4 
],
[
 -19.918,
-71.147,
15.5,
4.1 
],
[
 53.34,
-164.268,
19.7,
3.7 
],
[
 -19.794,
-70.833,
19.2,
4.1 
],
[
 -20.038,
-70.858,
10,
3.6 
],
[
 -20.132,
-70.402,
35.8,
3.8 
],
[
 -20.568,
-70.862,
17.9,
4.6 
],
[
 23.074,
93.182,
47.7,
4.1 
],
[
 35.895,
-97.268,
4.2,
3 
],
[
 -20.591,
-70.896,
22.2,
4.5 
],
[
 39.233,
-120.104,
0.4,
2.7 
],
[
 -22.187,
-70.308,
59.5,
4.7 
],
[
 38.449,
-122.254,
8.2,
3.6 
],
[
 -20.651,
-70.657,
18.6,
4.7 
],
[
 35.903,
-97.245,
4.2,
3.2 
],
[
 35.9,
-97.26,
5,
3.5 
],
[
 38.2,
20.46,
5,
4 
],
[
 60.27,
-152.507,
90.9,
2.9 
],
[
 -20.621,
-70.739,
20,
6.1 
],
[
 26.213,
100.679,
10,
4.4 
],
[
 -20.164,
-70.681,
23.5,
4.9 
],
[
 -20.176,
-70.452,
30.5,
4.1 
],
[
 -20.397,
-70.55,
17.4,
4.3 
],
[
 -19.697,
-178.059,
588,
4.9 
],
[
 59.278,
-152.642,
83.9,
2.5 
],
[
 36.653,
-98.117,
7.6,
2.9 
],
[
 36.445,
-97.091,
4.5,
3.1 
],
[
 -20.351,
-70.819,
10,
5.1 
],
[
 62.883,
-150.803,
100,
2.9 
],
[
 18.056,
-65.055,
19,
2.9 
],
[
 34.141,
-117.459,
7,
2.9 
],
[
 51.552,
-175.163,
25.7,
4 
],
[
 34.045,
-118.943,
11.7,
3.1 
],
[
 58.854,
-150.804,
20.5,
2.6 
],
[
 35.891,
-97.27,
4.8,
3.3 
],
[
 36.83,
121.718,
33.4,
4.4 
],
[
 32.566,
132.056,
41.7,
4.6 
],
[
 -20.809,
-70.546,
19.1,
4.2 
],
[
 40.552,
-116.262,
10.1,
2.9 
],
[
 -20.549,
-70.938,
1,
4.9 
],
[
 -20.618,
-71.001,
11.7,
5.2 
],
[
 -18.007,
-178.494,
584.9,
5.3 
],
[
 19.251,
-66.946,
35,
2.9 
],
[
 45.523,
26.368,
130.6,
4.5 
],
[
 -20.643,
-70.352,
29.8,
4.6 
],
[
 -20.176,
-71.154,
10.6,
5.1 
],
[
 27.793,
-111.526,
13.4,
4.2 
],
[
 44.526,
-111.141,
14.4,
2.5 
],
[
 48.466,
153.008,
155.2,
4.3 
],
[
 -20.613,
-70.895,
10.1,
4.9 
],
[
 -5.406,
102.137,
11.1,
5.6 
],
[
 -20.558,
-70.708,
14.9,
5.6 
],
[
 -34.69,
54.266,
10,
5 
],
[
 -20.222,
-70.468,
26.1,
5 
],
[
 -20.504,
-70.653,
22.8,
4.7 
],
[
 -19.912,
-71.003,
14.6,
4.8 
],
[
 61.071,
-141.293,
16.7,
2.6 
],
[
 59.252,
-136.336,
7.1,
3.4 
],
[
 -20.284,
-70.885,
26.7,
4.8 
],
[
 66.286,
-149.839,
13,
2.5 
],
[
 66.202,
-149.545,
15.7,
2.6 
],
[
 -20.663,
-70.667,
17.8,
4.9 
],
[
 -19,
-69.348,
103,
4.9 
],
[
 61.055,
-149.832,
14.5,
2.6 
],
[
 -20.773,
-70.401,
26.9,
5.5 
],
[
 -20.458,
-70.598,
20.9,
5.2 
],
[
 -20.807,
-70.549,
24.3,
6.2 
],
[
 -19.824,
-70.943,
16.6,
4.8 
],
[
 -20.747,
-70.689,
10,
4.9 
],
[
 13.174,
-90.339,
83.2,
4.4 
],
[
 -20.633,
-70.804,
18.2,
5.2 
],
[
 -20.381,
-70.593,
20,
4.5 
],
[
 -19.855,
-70.773,
21.3,
5.1 
],
[
 -20.755,
-70.649,
31.5,
4.9 
],
[
 -20.633,
-70.734,
10,
5.8 
],
[
 -20.722,
-70.582,
16.7,
5.6 
],
[
 -20.518,
-70.498,
31.1,
7.7 
],
[
 -20.074,
-70.952,
14.7,
4.9 
],
[
 -20.268,
-70.556,
22.8,
6.5 
],
[
 13.353,
-89.183,
71.2,
4.4 
],
[
 -19.725,
-71.165,
19,
5.1 
],
[
 39.196,
141.766,
55.6,
5.6 
],
[
 59.839,
-153.613,
100,
3 
],
[
 63.487,
-151.285,
14.6,
3.9 
],
[
 59.576,
-152.872,
100,
2.5 
],
[
 -20.389,
-70.601,
22.8,
4.8 
],
[
 53.154,
-164.542,
56.2,
2.7 
],
[
 -19.987,
-70.975,
17.6,
4.6 
],
[
 -19.634,
-71.487,
13.5,
4.6 
],
[
 -20.049,
-71.079,
15,
4.3 
],
[
 -20.412,
-70.53,
24.2,
5.1 
],
[
 -19.898,
-70.908,
13,
4.5 
],
[
 35.794,
-96.971,
4.3,
2.5 
],
[
 58.644,
-156.257,
189,
2.5 
],
[
 -20.01,
-71.191,
18.6,
4 
],
[
 36.577,
-97.631,
5,
2.9 
],
[
 -19.765,
-70.299,
36.2,
4.9 
],
[
 -6.522,
103.757,
19.9,
4.7 
],
[
 39.279,
-122.79,
7.5,
3.3 
],
[
 7.904,
-82.345,
31.6,
6 
],
[
 18.366,
-64.197,
43,
2.8 
],
[
 58.235,
-151.563,
13.6,
3.3 
],
[
 -19.757,
-70.757,
20,
4.5 
],
[
 -19.811,
-70.647,
22.1,
4 
],
[
 53.464,
-163.466,
24.9,
2.6 
],
[
 -5.343,
152.574,
50.4,
4.7 
],
[
 -19.759,
-70.621,
22.7,
4.5 
],
[
 -19.886,
-70.769,
10,
4.4 
],
[
 51.68,
-175.407,
26.6,
2.6 
],
[
 51.63,
179.991,
14.1,
2.6 
],
[
 -20.06,
-70.856,
10,
4.2 
],
[
 -7.836,
110.463,
13.8,
4.1 
],
[
 -19.982,
-70.919,
16.5,
5.1 
],
[
 -19.961,
-70.986,
10,
5.4 
],
[
 14.415,
56.234,
10,
4.8 
],
[
 58.017,
-156.148,
100,
2.7 
],
[
 67.376,
-164.588,
20,
2.9 
],
[
 16.84,
-94.526,
120.8,
4.2 
],
[
 -20.198,
-70.863,
10,
5 
],
[
 35.513,
-97.291,
4.9,
2.7 
],
[
 -20.105,
-70.377,
10,
5.1 
],
[
 -20.127,
-70.878,
10,
5.2 
],
[
 18.724,
-66.335,
87,
2.6 
],
[
 -19.613,
-70.359,
10,
5.1 
],
[
 -19.924,
-70.983,
10,
5 
],
[
 61.615,
-150.855,
59,
2.5 
],
[
 -20.443,
-70.617,
10,
4.7 
],
[
 51.343,
-178.911,
43.2,
2.6 
],
[
 -19.749,
-71.132,
10,
5 
],
[
 -20.154,
-70.851,
10,
5.8 
],
[
 35.921,
-97.242,
6.4,
2.7 
],
[
 -19.847,
-70.939,
10,
5.1 
],
[
 -19.929,
-70.869,
10,
4.9 
],
[
 -19.604,
-70.674,
10,
4.9 
],
[
 68.764,
-147.846,
33.4,
2.7 
],
[
 -19.493,
-70.619,
10,
4.7 
],
[
 -19.9,
-70.929,
10,
5.2 
],
[
 -20.175,
-70.505,
10,
4.5 
],
[
 -19.33,
-70.812,
10,
5 
],
[
 -10.806,
164.04,
26.2,
5.1 
],
[
 -19.89,
-71.034,
10,
4.9 
],
[
 -19.334,
-70.899,
10,
4.8 
],
[
 61.109,
-147.186,
0.1,
2.5 
],
[
 18.946,
-66.792,
33,
2.8 
],
[
 61.016,
-151.039,
65.5,
2.5 
],
[
 -20.249,
-70.875,
10,
4.9 
],
[
 -19.233,
-70.776,
10,
4.8 
],
[
 -20.004,
-70.825,
10,
5.2 
],
[
 -20.105,
-70.744,
10,
4.7 
],
[
 -19.438,
-70.808,
10,
5.3 
],
[
 -19.813,
-70.509,
32.8,
4.7 
],
[
 36.6,
-97.639,
5,
3.1 
],
[
 63.529,
-147.746,
16.2,
3.1 
],
[
 -20.042,
-70.544,
21.5,
5.4 
],
[
 -20.249,
-70.687,
12.6,
5.5 
],
[
 -19.909,
-70.726,
10,
5.6 
],
[
 -19.625,
-70.809,
10,
5.7 
],
[
 -19.846,
-70.874,
10,
5.8 
],
[
 -19.426,
-70.264,
18.1,
6.2 
],
[
 -20.059,
-70.603,
28.1,
5.2 
],
[
 -19.637,
-70.797,
10,
4.2 
],
[
 -19.642,
-70.817,
20.1,
8.2 
],
[
 -46.755,
-10.634,
10,
5.3 
],
[
 66.99,
-143.523,
13.1,
2.5 
],
[
 31.202,
128.031,
10,
4.7 
],
[
 61.724,
-152.016,
108.7,
2.6 
],
[
 62.208,
-151.29,
82.6,
2.5 
],
[
 40.725,
-125.236,
24.1,
2.9 
],
[
 -6.394,
130.907,
119.1,
4.5 
],
[
 57.114,
-149.587,
27.2,
2.6 
],
[
 33.911,
-117.95,
4,
3 
],
[
 36.589,
-121.189,
7.3,
2.6 
],
[
 26.259,
93.009,
47.8,
4.4 
] 
];
data.addColumn('number','Latitude');
data.addColumn('number','Longitude');
data.addColumn('number','Depth');
data.addColumn('number','Magnitude');
data.addRows(datajson);
return(data);
}
 
// jsDrawChart
function drawChartGeoChartID2d44f4f6fe7() {
var data = gvisDataGeoChartID2d44f4f6fe7();
var options = {};
options["width"] =    556;
options["height"] =    347;
options["displayMode"] = "Markers";
options["colorAxis"] = {colors:['purple', 'red', 'orange', 'grey']};
options["region"] = "JP";
options["backgroundColor"] = "lightblue";

    var chart = new google.visualization.GeoChart(
    document.getElementById('GeoChartID2d44f4f6fe7')
    );
    chart.draw(data,options);
    

}
  
 
// jsDisplayChart
(function() {
var pkgs = window.__gvisPackages = window.__gvisPackages || [];
var callbacks = window.__gvisCallbacks = window.__gvisCallbacks || [];
var chartid = "geochart";
  
// Manually see if chartid is in pkgs (not all browsers support Array.indexOf)
var i, newPackage = true;
for (i = 0; newPackage && i < pkgs.length; i++) {
if (pkgs[i] === chartid)
newPackage = false;
}
if (newPackage)
  pkgs.push(chartid);
  
// Add the drawChart function to the global list of callbacks
callbacks.push(drawChartGeoChartID2d44f4f6fe7);
})();
function displayChartGeoChartID2d44f4f6fe7() {
  var pkgs = window.__gvisPackages = window.__gvisPackages || [];
  var callbacks = window.__gvisCallbacks = window.__gvisCallbacks || [];
  window.clearTimeout(window.__gvisLoad);
  // The timeout is set to 100 because otherwise the container div we are
  // targeting might not be part of the document yet
  window.__gvisLoad = setTimeout(function() {
  var pkgCount = pkgs.length;
  google.load("visualization", "1", { packages:pkgs, callback: function() {
  if (pkgCount != pkgs.length) {
  // Race condition where another setTimeout call snuck in after us; if
  // that call added a package, we must not shift its callback
  return;
}
while (callbacks.length > 0)
callbacks.shift()();
} });
}, 100);
}
 
// jsFooter
</script>
 
<!-- jsChart -->  
<script type="text/javascript" src="https://www.google.com/jsapi?callback=displayChartGeoChartID2d44f4f6fe7"></script>
 
<!-- divChart -->
  
<div id="GeoChartID2d44f4f6fe7"
  style="width: 556px; height: 347px;">
</div>


---

## Google Map - NEW individual markers

```r
df <- data.frame(Adress=c("EC3M 7HA", "東京都新宿区北新宿2-21-1"),
                 Tip=c("Lloyd's", "Tokyo R User Group"))
plot(gvisMap(df, "Adress", "Tip",
              options=list(mapType='normal',
                icons="{'default': {'normal': 'http://icons.iconarchive.com/icons/icons-land/vista-map-markers/48/Map-Marker-Ball-Azure-icon.png',
                                               'selected': 'http://icons.iconarchive.com/icons/icons-land/vista-map-markers/48/Map-Marker-Ball-Right-Azure-icon.png'}
                                  }", width=800, height=250)))
```

<iframe src="https://dl.dropboxusercontent.com/u/7586336/blogger/MapTokyoRUserGroup.html" width=600 height=300 frameborder=0>Loading</iframe>
---

## Timeline - NEW

```r
dat <- data.frame(Room=c("Room 1","Room 2","Room 3"),
                  Language=c("Japanese", "English", "German"),
                  start=as.POSIXct(c("2014-04-17 14:00", "2014-04-17 15:00",
                                     "2014-04-17 14:30")),
                  end=as.POSIXct(c("2014-04-17 15:00", "2014-04-17 16:00",
                                   "2014-04-17 15:30")))
plot(gvisTimeline(data=dat, rowlabel="Room", barlabel="Language",
                  start="start", end="end", options=list(width=800, height=250)))
```

<!-- Timeline generated in R 3.0.2 by googleVis 0.5.0-4 package -->
<!-- Tue Apr  8 19:39:01 2014 -->


<!-- jsHeader -->
<script type="text/javascript">
 
// jsData 
function gvisDataTimelineID2d4683bcf5e () {
var data = new google.visualization.DataTable();
var datajson =
[
 [
 "Room 1",
"Japanese",
new Date(2014,3,17,14,0,0),
new Date(2014,3,17,15,0,0) 
],
[
 "Room 2",
"English",
new Date(2014,3,17,15,0,0),
new Date(2014,3,17,16,0,0) 
],
[
 "Room 3",
"German",
new Date(2014,3,17,14,30,0),
new Date(2014,3,17,15,30,0) 
] 
];
data.addColumn('string','Room');
data.addColumn('string','Language');
data.addColumn('datetime','start');
data.addColumn('datetime','end');
data.addRows(datajson);
return(data);
}
 
// jsDrawChart
function drawChartTimelineID2d4683bcf5e() {
var data = gvisDataTimelineID2d4683bcf5e();
var options = {};
options["width"] =    800;
options["height"] =    250;

    var chart = new google.visualization.Timeline(
    document.getElementById('TimelineID2d4683bcf5e')
    );
    chart.draw(data,options);
    

}
  
 
// jsDisplayChart
(function() {
var pkgs = window.__gvisPackages = window.__gvisPackages || [];
var callbacks = window.__gvisCallbacks = window.__gvisCallbacks || [];
var chartid = "timeline";
  
// Manually see if chartid is in pkgs (not all browsers support Array.indexOf)
var i, newPackage = true;
for (i = 0; newPackage && i < pkgs.length; i++) {
if (pkgs[i] === chartid)
newPackage = false;
}
if (newPackage)
  pkgs.push(chartid);
  
// Add the drawChart function to the global list of callbacks
callbacks.push(drawChartTimelineID2d4683bcf5e);
})();
function displayChartTimelineID2d4683bcf5e() {
  var pkgs = window.__gvisPackages = window.__gvisPackages || [];
  var callbacks = window.__gvisCallbacks = window.__gvisCallbacks || [];
  window.clearTimeout(window.__gvisLoad);
  // The timeout is set to 100 because otherwise the container div we are
  // targeting might not be part of the document yet
  window.__gvisLoad = setTimeout(function() {
  var pkgCount = pkgs.length;
  google.load("visualization", "1", { packages:pkgs, callback: function() {
  if (pkgCount != pkgs.length) {
  // Race condition where another setTimeout call snuck in after us; if
  // that call added a package, we must not shift its callback
  return;
}
while (callbacks.length > 0)
callbacks.shift()();
} });
}, 100);
}
 
// jsFooter
</script>
 
<!-- jsChart -->  
<script type="text/javascript" src="https://www.google.com/jsapi?callback=displayChartTimelineID2d4683bcf5e"></script>
 
<!-- divChart -->
  
<div id="TimelineID2d4683bcf5e"
  style="width: 800px; height: 250px;">
</div>


---

## Sankey chart - NEW

```r
dat <- data.frame(From=c(rep("A",3), rep("B", 3)), 
                  To=c(rep(c("X", "Y", "Z"),2)),
                  Weight=c(5,7,6,2,9,4))
plot(gvisSankey(dat, from="From", to="To", weight="Weight",
                options=list(height=250)))
```

<!-- Sankey generated in R 3.0.2 by googleVis 0.5.0-4 package -->
<!-- Tue Apr  8 19:39:01 2014 -->


<!-- jsHeader -->
<script type="text/javascript">
 
// jsData 
function gvisDataSankeyID2d42eab59c8 () {
var data = new google.visualization.DataTable();
var datajson =
[
 [
 "A",
"X",
5 
],
[
 "A",
"Y",
7 
],
[
 "A",
"Z",
6 
],
[
 "B",
"X",
2 
],
[
 "B",
"Y",
9 
],
[
 "B",
"Z",
4 
] 
];
data.addColumn('string','From');
data.addColumn('string','To');
data.addColumn('number','Weight');
data.addRows(datajson);
return(data);
}
 
// jsDrawChart
function drawChartSankeyID2d42eab59c8() {
var data = gvisDataSankeyID2d42eab59c8();
var options = {};
options["width"] =    400;
options["height"] =    250;

    var chart = new google.visualization.Sankey(
    document.getElementById('SankeyID2d42eab59c8')
    );
    chart.draw(data,options);
    

}
  
 
// jsDisplayChart
(function() {
var pkgs = window.__gvisPackages = window.__gvisPackages || [];
var callbacks = window.__gvisCallbacks = window.__gvisCallbacks || [];
var chartid = "sankey";
  
// Manually see if chartid is in pkgs (not all browsers support Array.indexOf)
var i, newPackage = true;
for (i = 0; newPackage && i < pkgs.length; i++) {
if (pkgs[i] === chartid)
newPackage = false;
}
if (newPackage)
  pkgs.push(chartid);
  
// Add the drawChart function to the global list of callbacks
callbacks.push(drawChartSankeyID2d42eab59c8);
})();
function displayChartSankeyID2d42eab59c8() {
  var pkgs = window.__gvisPackages = window.__gvisPackages || [];
  var callbacks = window.__gvisCallbacks = window.__gvisCallbacks || [];
  window.clearTimeout(window.__gvisLoad);
  // The timeout is set to 100 because otherwise the container div we are
  // targeting might not be part of the document yet
  window.__gvisLoad = setTimeout(function() {
  var pkgCount = pkgs.length;
  google.load("visualization", "1", { packages:pkgs, callback: function() {
  if (pkgCount != pkgs.length) {
  // Race condition where another setTimeout call snuck in after us; if
  // that call added a package, we must not shift its callback
  return;
}
while (callbacks.length > 0)
callbacks.shift()();
} });
}, 100);
}
 
// jsFooter
</script>
 
<!-- jsChart -->  
<script type="text/javascript" src="https://www.google.com/jsapi?callback=displayChartSankeyID2d42eab59c8"></script>
 
<!-- divChart -->
  
<div id="SankeyID2d42eab59c8"
  style="width: 400px; height: 250px;">
</div>


---

## Calendar chart - NEW

```r
plot(gvisCalendar(Cairo, datevar="Date",
                  numvar="Temp",
                  options=list(calendar="{ cellSize: 10 }"))
```

<iframe src="https://dl.dropboxusercontent.com/u/7586336/blogger/CalendarCario.html" width=600 height=400>Loading</iframe>

---

## Annotation Chart - NEW


```r
xtable(tail(Stock, 3))
```

<!-- html table generated in R 3.0.2 by xtable 1.7-3 package -->
<!-- Tue Apr  8 19:39:01 2014 -->
<TABLE border=1>
<TR> <TH>  </TH> <TH> Date </TH> <TH> Device </TH> <TH> Value </TH> <TH> Title </TH> <TH> Annotation </TH>  </TR>
  <TR> <TD align="right"> 10 </TD> <TD align="right"> 13882.00 </TD> <TD> Pens </TD> <TD align="right"> 14334.00 </TD> <TD> Out of stock </TD> <TD> Ran out of stock of pens at 4pm </TD> </TR>
  <TR> <TD align="right"> 11 </TD> <TD align="right"> 13883.00 </TD> <TD> Pens </TD> <TD align="right"> 66467.00 </TD> <TD>  </TD> <TD>  </TD> </TR>
  <TR> <TD align="right"> 12 </TD> <TD align="right"> 13884.00 </TD> <TD> Pens </TD> <TD align="right"> 39463.00 </TD> <TD>  </TD> <TD>  </TD> </TR>
   </TABLE>

```r
A <- gvisAnnotationChart(Stock, datevar="Date",
                         numvar="Value", idvar="Device",
                         titlevar="Title", annotationvar="Annotation",
                         options=list(displayAnnotations=TRUE,
                                      legendPosition='newRow',
                                      width=600, height=300)
                         )
```


---

## Annotation Chart - NEW


```r
plot(A, tag='chart')
```

<iframe src="https://dl.dropboxusercontent.com/u/7586336/blogger/AnnotationChart.html" frameborder="0" width="600" height="400">Loading</iframe>

---

## Merging gvis-objects


```r
G <- gvisGeoChart(Exports, "Country", "Profit", 
                  options=list(width=250, height=120))
B <- gvisBarChart(Exports[,1:2], yvar="Profit", xvar="Country",                  
                  options=list(width=250, height=260, legend='none'))
M <- gvisMotionChart(Fruits, "Fruit", "Year",
                     options=list(width=400, height=380))
GBM <- gvisMerge(gvisMerge(G,B, horizontal=FALSE), 
                 M, horizontal=TRUE, tableOptions="cellspacing=5")
```


---

## Display merged gvis-objects

```r
plot(GBM)
```

<iframe src="https://dl.dropboxusercontent.com/u/7586336/googleVisExamples/gvisMergeExample.html" frameborder="0", width="620", height="420">Loading</iframe>

---

## Embedding googleVis chart into your web page

Suppose you have an existing web page and would like to integrate the output of a googleVis function, such as ```gvisMotionChart```.

In this case you only need the chart output from ```gvisMotionChart```. So you can either copy and paste the output from the R console


```r
print(M, "chart")  #### or cat(M$html$chart)
```

into your existing html page, or write the content directly into a file


```r
print(M, "chart", file = "myfilename")
```

and process it from there.

---

## Embedding googleVis output via iframe

* Embedding googleVis charts is often easiest done via the iframe tag:
* Host the googleVis output on-line, e.g. public Dropbox folder
* Use the iframe tag on your page:

```
<iframe width=620 height=300 frameborder="0"
src="http://dl.dropbox.com/u/7586336/RSS2012/line.html">
Your browser does not support iframe
</iframe>
```

---

## iFrame output

<iframe width=620 height=300 frameborder="0" src="http://dl.dropbox.com/u/7586336/RSS2012/line.html">You browser does not support iframe</iframe>

---

## Including googleVis output in knitr with plot statement

* With version 0.3.2 of googleVis `plot.gvis` gained the argument `'tag'`, which works similar to the argument of the same name in `print.gvis`. 

* By default the tag argument is `NULL` and `plot.gvis` has the same behaviour as in the previous versions of googleVis. 

* Change the tag to `'chart'` and `plot.gvis` will produce the same output as `print.gvis`. 

* Thus, setting the `gvis.plot.tag` value to `'chart'` in `options()` will return the HTML code of the chart when the file is parsed with `knitr`. 

* See the example in `?plot.gvis` for more details

---

## Further reading and examples

* [Shiny by RStudio](http://www.rstudio.com/shiny/)
* [First steps with googleVis on shiny](http://lamages.blogspot.co.uk/2013/02/first-steps-of-using-googlevis-on-shiny.html)
* [RStudio Glimmer Server](http://glimmer.rstudio.com:8787)
* [BI Dashbord with shiny and rCharts](http://glimmer.rstudio.com/reinholdsson/shiny-dashboard/)
* [Shiny examples with slidify](https://github.com/ramnathv/shinyExamples)
* [Shiny on R-Bloggers](http://www.r-bloggers.com/?s=shiny)


--- .segue .dark

## The End. Questions? 

----

## How I created these slides


```r
library(slidify)
author("googleVis_Tokyo_April_2014")
## Edit the file index.Rmd file and then
slidify("index.Rmd")
```


---

## Other R packages

* [rCharts](http://ramnathv.github.io/rCharts/)
* [clickme](https://github.com/nachocab/clickme)
* [R animation package allows to create SWF, GIF and MPEG directly](http://animation.yihui.name/)
* [iplots: iPlots - interactive graphics for R](http://cran.r-project.org/web/packages/iplots/)
* [Acinonyx aka iPlots eXtreme](http://rforge.net/Acinonyx/index.html)
* [gridSVG: Export grid graphics as SVG](http://cran.r-project.org/web/packages/gridSVG/index.html)
* [plotGoogleMaps: Plot HTML output with Google Maps API and your own data](http://cran.r-project.org/web/packages/plotGoogleMaps/)
* [RgoogleMaps: Overlays on Google map tiles in R](http://cran.r-project.org/web/packages/RgoogleMaps/index.html)

---

## Thanks

* Google, who make the visualisation API available
* All the guys behind www.gapminder.org and Hans Rosling for telling
    everyone that data is not boring 
* Sebastian Perez Saaibi for his inspiring talk on 'Generator
    Tool for Google Motion Charts' at the R/RMETRICS conference 2010
* Henrik Bengtsson for providing the 'R.rsp: R Server Pages'
    package and his reviews and comments
* Duncan Temple Lang for providing the 'RJSONIO' package
* Deepayan Sarkar for showing us in the lattice package how to deal
    with lists of options  
* Paul Cleary for a bug report on the handling of months:
    Google date objects expect the months Jan.- Dec. as 0 - 11 and
    not 1 - 12.
* Ben Bolker for comments on plot.gvis and the usage of temporary
    files  


---

## Thanks 

* John Verzani for pointing out how to use the R http help server
* Cornelius Puschmann and Jeffrey Breen for highlighting a
    dependency issue with RJONSIO version 0.7-1
* Manoj Ananthapadmanabhan and Anand Ramalingam for providing
    ideas and code to animate a Google Geo Map
* Rahul Premraj for pointing out a rounding issue with Google Maps 
* Mike Silberbauer for an example showing how to shade the
    areas in annotated time line charts
* Tony Breyal for providing instructions on changing the Flash
    security settings to display Flash charts locally 
* Alexander Holcroft for reporting a bug in gvisMotionChart
    when displaying data with special characters in column names
* Pat Burns for pointing out typos in the vignette

---

## Thanks

* Jason Pickering for providing a patch to allow for quarterly 
    and weekly time dimensions to be displayed with gvisMotionChart
* Oliver Jay and Wai Tung Ho for reporting an issue with one-row 
    data sets
* Erik Bülow for pointing out how to load the Google API via a
    secure connection
* Sebastian Kranz for comments to enhance the argument list for
    gvisMotionChart to make it more user friendly 
* Sebastian Kranz and Wei Luo for providing ideas and code to
    improve the transformation of R data frames into JSON code
* Sebastian Kranz for reporting a bug in version 0.3.0
* Leonardo Trabuco for helping to clarify the usage of the
    argument state in the help file of gvisMotionChart
* Mark Melling for reporting an issue with jsDisplayChart and
    providing a solution

---

## Thanks

* Joe Cheng for code contribution to make googleVis work with shiny
* John Maindonald for reporting that the WorldBank demo didn't 
    download all data, but only the first 12000 records.
* Sebastian Campbell for reporting a typo in the Andrew and Stock
    data set and pointing out that the core charts, such as line
  charts accept also date variables for the x-axis. 
* John Maindonald for providing a simplified version of the
    WorldBank demo using the WDI package.
* John Muschelli for suggesting to add 'hovervar' as an additional
    argument to gvisGeoChart.
* Jacqueline Buros for providing code to include formats parameter 
    to gvisTable()
* JJ Allaire for pointing out how to use the viewer pane in RStudio
  o Oliver Gjoneski and Ashton Trey Belew for patches on roles and tooltips
* [Ramnath Vaidyanathan](https://github.com/ramnathv) for slidify.

---
## Session Info


```r
sessionInfo()
```

```
## R version 3.0.2 (2013-09-25)
## Platform: x86_64-apple-darwin10.8.0 (64-bit)
## 
## locale:
## [1] de_DE.UTF-8/de_DE.UTF-8/de_DE.UTF-8/C/de_DE.UTF-8/de_DE.UTF-8
## 
## attached base packages:
## [1] stats     graphics  grDevices utils     datasets  methods   base     
## 
## other attached packages:
## [1] XML_3.95-0.2      RJSONIO_1.0-3     xtable_1.7-3      googleVis_0.5.0-4
## [5] slidify_0.4      
## 
## loaded via a namespace (and not attached):
##  [1] codetools_0.2-8 digest_0.6.4    evaluate_0.5.3  formatR_0.10   
##  [5] knitr_1.5       markdown_0.6.5  stringr_0.6.2   tools_3.0.2    
##  [9] whisker_0.3-2   yaml_2.1.11
```

