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

<!-- MotionChart generated in R 3.1.0 by googleVis 0.5.2 package -->
<!-- Wed Apr 16 22:13:06 2014 -->


<!-- jsHeader -->
<script type="text/javascript">
 
// jsData 
function gvisDataMotionChartID68fe5f65d953 () {
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
function drawChartMotionChartID68fe5f65d953() {
var data = gvisDataMotionChartID68fe5f65d953();
var options = {};
options["width"] =    600;
options["height"] =    400;

    var chart = new google.visualization.MotionChart(
    document.getElementById('MotionChartID68fe5f65d953')
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
callbacks.push(drawChartMotionChartID68fe5f65d953);
})();
function displayChartMotionChartID68fe5f65d953() {
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
<script type="text/javascript" src="https://www.google.com/jsapi?callback=displayChartMotionChartID68fe5f65d953"></script>
 
<!-- divChart -->
  
<div id="MotionChartID68fe5f65d953"
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

## googleVis version 0.5.1 provides interfaces to 

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

<!-- ScatterChart generated in R 3.1.0 by googleVis 0.5.2 package -->
<!-- Wed Apr 16 22:13:06 2014 -->


<!-- jsHeader -->
<script type="text/javascript">
 
// jsData 
function gvisDataScatterChartID68fe179f0913 () {
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
function drawChartScatterChartID68fe179f0913() {
var data = gvisDataScatterChartID68fe179f0913();
var options = {};
options["allowHtml"] = true;
options["lineWidth"] =      2;

    var chart = new google.visualization.ScatterChart(
    document.getElementById('ScatterChartID68fe179f0913')
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
callbacks.push(drawChartScatterChartID68fe179f0913);
})();
function displayChartScatterChartID68fe179f0913() {
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
<script type="text/javascript" src="https://www.google.com/jsapi?callback=displayChartScatterChartID68fe179f0913"></script>
 
<!-- divChart -->
  
<div id="ScatterChartID68fe179f0913"
  style="width: 600px; height: 500px;">
</div>


---

## Add additional columns to define roles - NEW


```r
df <- data.frame(year=1:11, x=1:11,
                 x.scope=c(rep(TRUE, 8), rep(FALSE, 3)),
                 y=11:1, y.html.tooltip=LETTERS[11:1],                 
                 y.certainty=c(rep(TRUE, 5), rep(FALSE, 6)),
                 y.emphasis=c(rep(FALSE, 4), rep(TRUE, 7)))
plot(gvisScatterChart(df,options=list(lineWidth=2)))
```

<!-- ScatterChart generated in R 3.1.0 by googleVis 0.5.2 package -->
<!-- Wed Apr 16 22:13:06 2014 -->


<!-- jsHeader -->
<script type="text/javascript">
 
// jsData 
function gvisDataScatterChartID68fe4a0cca82 () {
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
function drawChartScatterChartID68fe4a0cca82() {
var data = gvisDataScatterChartID68fe4a0cca82();
var options = {};
options["allowHtml"] = true;
options["lineWidth"] =      2;

    var chart = new google.visualization.ScatterChart(
    document.getElementById('ScatterChartID68fe4a0cca82')
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
callbacks.push(drawChartScatterChartID68fe4a0cca82);
})();
function displayChartScatterChartID68fe4a0cca82() {
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
<script type="text/javascript" src="https://www.google.com/jsapi?callback=displayChartScatterChartID68fe4a0cca82"></script>
 
<!-- divChart -->
  
<div id="ScatterChartID68fe4a0cca82"
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

<!-- GeoChart generated in R 3.1.0 by googleVis 0.5.2 package -->
<!-- Wed Apr 16 22:13:07 2014 -->


<!-- jsHeader -->
<script type="text/javascript">
 
// jsData 
function gvisDataGeoChartID68fedc342c9 () {
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
function drawChartGeoChartID68fedc342c9() {
var data = gvisDataGeoChartID68fedc342c9();
var options = {};
options["width"] =    556;
options["height"] =    347;
options["projection"] = "kavrayskiy-vii";
options["colorAxis"] = {colors:['#91BFDB', '#FC8D59']};

    chartGeoChartID68fedc342c9 = new google.visualization.ChartWrapper({
    dataTable: data,       
    chartType: 'GeoChart',
    containerId: 'GeoChartID68fedc342c9',
    options: options
    });
    chartGeoChartID68fedc342c9.draw();
    

}

  function openEditorGeoChartID68fedc342c9() {
  var editor = new google.visualization.ChartEditor();
  google.visualization.events.addListener(editor, 'ok',
  function() { 
  chartGeoChartID68fedc342c9 = editor.getChartWrapper();  
  chartGeoChartID68fedc342c9.draw(document.getElementById('GeoChartID68fedc342c9')); 
  }); 
  editor.openDialog(chartGeoChartID68fedc342c9);
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
callbacks.push(drawChartGeoChartID68fedc342c9);
})();
function displayChartGeoChartID68fedc342c9() {
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
<script type="text/javascript" src="https://www.google.com/jsapi?callback=displayChartGeoChartID68fedc342c9"></script>
 
<!-- divChart -->
<input type='button' onclick='openEditorGeoChartID68fedc342c9()' value='S&P'/>  
<div id="GeoChartID68fedc342c9"
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

<!-- GeoChart generated in R 3.1.0 by googleVis 0.5.2 package -->
<!-- Wed Apr 16 22:13:08 2014 -->


<!-- jsHeader -->
<script type="text/javascript">
 
// jsData 
function gvisDataGeoChartID68fee55a12e () {
var data = new google.visualization.DataTable();
var datajson =
[
 [
 62.886,
-149.935,
76.2,
5.1 
],
[
 -6.766,
154.839,
52,
5.4 
],
[
 -16.6,
-73.765,
98.2,
4.3 
],
[
 59.856,
-153.109,
100,
2.7 
],
[
 37.296,
142.067,
44.8,
4.9 
],
[
 37.076,
143.467,
32.2,
4.6 
],
[
 -9.435,
117.94,
63,
4.7 
],
[
 18.972,
-66.75,
59,
2.9 
],
[
 19.087,
-66.792,
33,
3 
],
[
 19.043,
-66.664,
65,
2.8 
],
[
 19.162,
-66.789,
30,
2.9 
],
[
 19.174,
-66.779,
23,
2.7 
],
[
 19.188,
-66.797,
24,
3.1 
],
[
 38.308,
141.998,
48.4,
4.6 
],
[
 19.15,
-66.779,
29,
2.8 
],
[
 19.225,
-66.796,
23,
2.8 
],
[
 19.174,
-66.781,
36,
3.3 
],
[
 19.073,
-66.081,
25,
2.6 
],
[
 38.834,
-122.809,
1.6,
2.7 
],
[
 18.875,
-64.273,
31,
3 
],
[
 -5.041,
152.24,
54.8,
4.8 
],
[
 60.038,
-153.208,
100,
2.5 
],
[
 36.112,
141.896,
39,
4.5 
],
[
 8.408,
-82.734,
44.1,
4.8 
],
[
 39.226,
142.217,
35,
4.4 
],
[
 -11.138,
161.619,
35,
4.9 
],
[
 60.336,
-148.659,
10.2,
2.5 
],
[
 -11.085,
161.601,
37.4,
4.7 
],
[
 -11.574,
162.168,
35,
4.6 
],
[
 19.396,
-64.478,
28,
3.4 
],
[
 18.456,
-68.798,
113,
3.4 
],
[
 -5.039,
102.692,
45.9,
4.8 
],
[
 63.61,
-149.833,
133.9,
3.4 
],
[
 -18.105,
-177.96,
623.3,
4.7 
],
[
 -20.128,
-70.797,
12,
4.7 
],
[
 -20.203,
-70.779,
19.7,
5.3 
],
[
 19.377,
-64.525,
26,
3.4 
],
[
 36.134,
-97.63,
4.9,
2.8 
],
[
 16.287,
145.673,
531.2,
4.5 
],
[
 51.756,
-172.649,
45.4,
3.4 
],
[
 -11.395,
162.902,
35,
4.6 
],
[
 52.273,
179.406,
92.2,
3 
],
[
 43.566,
144.02,
94.8,
4 
],
[
 51.754,
178.25,
123.2,
4.1 
],
[
 -5.642,
153.797,
47.2,
5.3 
],
[
 -21.996,
-176.358,
176,
4.6 
],
[
 -20.181,
-70.846,
15.2,
4.9 
],
[
 36.233,
140.934,
42.2,
4.7 
],
[
 -20.563,
-70.98,
15.4,
3.8 
],
[
 58.758,
-154.366,
100,
2.8 
],
[
 -20.219,
-70.836,
9.6,
4.7 
],
[
 -20.209,
-70.915,
21.5,
4.5 
],
[
 62.497,
-150.45,
61.6,
2.9 
],
[
 -20.191,
-70.734,
15.3,
5.2 
],
[
 -20.227,
-70.831,
18.7,
5.2 
],
[
 11.839,
-88.242,
10,
4.6 
],
[
 -11.12,
161.698,
35,
4.8 
],
[
 52.378,
178.709,
55.8,
2.8 
],
[
 31.139,
-115.618,
22.8,
3 
],
[
 1.746,
127.567,
54.4,
4.5 
],
[
 36.578,
-121.052,
6.2,
2.9 
],
[
 -36.058,
-101.187,
10,
5.6 
],
[
 46.182,
142.964,
348,
4.2 
],
[
 19.49,
-155.701,
9.1,
2.5 
],
[
 -5.598,
147.227,
191.8,
4.5 
],
[
 13.966,
-91.627,
62.2,
4.4 
],
[
 19.378,
-155.23,
2.9,
2.6 
],
[
 18.976,
-63.764,
43,
4 
],
[
 51.496,
179.013,
75.8,
2.7 
],
[
 -53.527,
8.704,
11.7,
6.9 
],
[
 44.695,
-114.326,
5,
2.5 
],
[
 44.577,
-114.323,
5,
2.5 
],
[
 19.136,
-64.419,
16,
2.7 
],
[
 44.726,
-114.332,
5,
2.5 
],
[
 8.914,
126.486,
45.6,
5 
],
[
 18.07,
-65.015,
3,
2.7 
],
[
 -11.399,
162.931,
22.1,
4.7 
],
[
 -11.161,
161.668,
35,
4.8 
],
[
 -11.32,
162.853,
35,
4.9 
],
[
 -11.28,
162.926,
27.3,
5.3 
],
[
 -11.317,
162.779,
32.4,
5.1 
],
[
 -11.505,
162.86,
35,
4.7 
],
[
 -11.491,
162.881,
35,
4.7 
],
[
 -12.501,
-75.159,
92.2,
4.9 
],
[
 44.657,
-114.348,
5,
2.7 
],
[
 -18.594,
-70.862,
33.4,
4.5 
],
[
 -11.121,
161.711,
35.1,
4.8 
],
[
 31.523,
-115.47,
11.4,
3.8 
],
[
 -11.55,
161.936,
33.7,
4.7 
],
[
 34.108,
25.856,
9.8,
5 
],
[
 44.651,
-114.273,
5,
4.4 
],
[
 -6.583,
155.03,
55,
4.7 
],
[
 44.664,
-114.324,
5,
3 
],
[
 36.293,
-97.266,
5,
2.5 
],
[
 36.284,
-97.267,
5,
2.6 
],
[
 40.216,
-125.124,
4.6,
2.7 
],
[
 -11.085,
161.755,
35,
4.9 
],
[
 3.865,
96.733,
93.6,
4.6 
],
[
 51.664,
-177.155,
55.9,
2.7 
],
[
 -20.904,
-178.674,
548.9,
4.6 
],
[
 33.638,
-116.76,
13.1,
2.8 
],
[
 18.862,
-63.94,
28,
2.8 
],
[
 -20.596,
-70.924,
10,
4.7 
],
[
 15.376,
-91.744,
203.8,
4.6 
],
[
 35.795,
-97.514,
8.9,
3 
],
[
 -23.41,
-179.754,
527.7,
4.6 
],
[
 -11.073,
161.554,
37.9,
4.7 
],
[
 18.879,
-64.308,
37,
2.5 
],
[
 60.13,
-153.317,
100,
2.6 
],
[
 -10.747,
161.487,
34,
5 
],
[
 40.565,
-125.166,
11.1,
2.6 
],
[
 61.503,
-140.617,
null,
2.7 
],
[
 -11.123,
161.706,
35,
4.8 
],
[
 3.717,
-31.296,
10,
5.2 
],
[
 -11.273,
161.718,
35,
5.2 
],
[
 51.182,
-179.068,
67.4,
4.6 
],
[
 -11.525,
162.025,
27.7,
4.6 
],
[
 -11.184,
161.896,
35,
4.8 
],
[
 61.498,
-146.624,
13.6,
2.7 
],
[
 -11.27,
161.78,
35,
5.9 
],
[
 59.675,
-152.575,
5,
2.6 
],
[
 -20.764,
-70.694,
15.4,
5.3 
],
[
 53.166,
-166.73,
25.6,
3.6 
],
[
 12.176,
-86.297,
14.8,
5.1 
],
[
 -11.523,
162.647,
36.6,
5 
],
[
 12.299,
-86.273,
10,
4.4 
],
[
 -11.51,
162.456,
35,
4.9 
],
[
 60.894,
-147.116,
15.4,
3.1 
],
[
 -5.814,
148.711,
119.1,
4.6 
],
[
 -18.954,
175.871,
88.8,
4.9 
],
[
 -11.541,
161.961,
39.8,
5.3 
],
[
 40.74,
-124.496,
18.6,
2.8 
],
[
 18.661,
-66.81,
71,
2.8 
],
[
 51.455,
-178.483,
32.8,
3.5 
],
[
 -6.99,
154.969,
39.8,
4.7 
],
[
 -11.328,
162.285,
14.9,
4.8 
],
[
 -20.203,
-71.009,
11.7,
4.1 
],
[
 35.793,
-97.494,
6.4,
3.7 
],
[
 -11.093,
161.705,
35,
4.6 
],
[
 -11.634,
161.894,
35,
4.8 
],
[
 35.781,
-97.489,
5,
2.9 
],
[
 35.778,
-97.488,
7.1,
3.8 
],
[
 61.234,
-150.911,
64.5,
3.4 
],
[
 -11.45,
161.702,
35,
4.8 
],
[
 -11.482,
162.706,
37.5,
4.7 
],
[
 -11.411,
162.636,
22.6,
4.9 
],
[
 -11.226,
162.067,
33.7,
5 
],
[
 15.412,
-104.403,
35,
4.3 
],
[
 -11.13,
162.038,
35,
5.9 
],
[
 19.46,
-68.805,
78,
3.4 
],
[
 -6.738,
154.916,
35,
5.3 
],
[
 -11.218,
161.923,
35,
5.6 
],
[
 35.771,
-97.482,
6.3,
2.5 
],
[
 -11.457,
162.329,
31.4,
5.7 
],
[
 -11.451,
162.069,
35,
7.4 
],
[
 -11.356,
162.598,
20,
4.7 
],
[
 -20.621,
-70.715,
18.6,
5.3 
],
[
 44.586,
-114.292,
5,
2.6 
],
[
 15.307,
-104.707,
10,
4.5 
],
[
 -11.039,
162.025,
10,
4.9 
],
[
 -11.336,
162.198,
10,
4.8 
],
[
 7.587,
-37.154,
10,
4.8 
],
[
 -11.187,
162.039,
34.9,
4.7 
],
[
 -11.32,
161.942,
8.1,
5.1 
],
[
 -11.238,
162.006,
21.1,
5 
],
[
 -11.052,
162.121,
11.7,
5.2 
],
[
 37.274,
141.322,
55.5,
4.8 
],
[
 -6.597,
155.222,
86.4,
4.7 
],
[
 -11.348,
162.587,
19.2,
4.9 
],
[
 15.41,
-104.75,
10,
4.4 
],
[
 -19.866,
-71.07,
21.8,
4.4 
],
[
 -21.154,
-68.705,
135.9,
4.4 
],
[
 41.206,
-119.819,
1.5,
2.9 
],
[
 -11.459,
162.787,
10,
4.8 
],
[
 17.704,
-95.026,
63.2,
4.6 
],
[
 -11.588,
162.083,
20,
4.6 
],
[
 -6.761,
154.994,
68.1,
4.6 
],
[
 -11.436,
162.474,
14.4,
4.9 
],
[
 19.408,
-67.265,
46,
2.7 
],
[
 31.867,
-115.851,
15.8,
2.7 
],
[
 -21.122,
-69.086,
114.4,
4.6 
],
[
 -11.082,
161.397,
20,
4.7 
],
[
 -11.236,
162.053,
19.1,
4.6 
],
[
 -23.428,
-68.065,
138.1,
4.5 
],
[
 18.799,
-67.218,
17,
2.5 
],
[
 -11.199,
161.928,
23.8,
4.8 
],
[
 -11.275,
161.643,
24,
4.6 
],
[
 -20.478,
-177.945,
518,
4.4 
],
[
 -11.638,
162.023,
18.1,
4.8 
],
[
 37.016,
71.257,
83.7,
4.3 
],
[
 -11.575,
161.846,
24.1,
4.9 
],
[
 32.995,
-117.784,
9.5,
2.6 
],
[
 35.777,
-97.508,
6.3,
2.5 
],
[
 35.449,
-84.467,
13.9,
2.8 
],
[
 46.781,
153.193,
36.1,
4.8 
],
[
 86.687,
45.393,
10,
4.6 
],
[
 19.445,
-155.317,
4.3,
2.5 
],
[
 44.704,
-114.265,
5,
2.6 
],
[
 -6.964,
129.763,
133.4,
4.5 
],
[
 60.274,
-152.6,
99.7,
2.5 
],
[
 44.587,
-114.336,
4.9,
3.2 
],
[
 44.644,
-114.251,
5,
4.9 
],
[
 -11.432,
162.533,
7,
5.1 
],
[
 59.136,
-152.535,
72.7,
3 
],
[
 -11.479,
162.503,
34.9,
4.9 
],
[
 36.857,
-97.827,
4.9,
3 
],
[
 -20.127,
-70.971,
20.6,
4.3 
],
[
 -11.549,
162.609,
35,
4.6 
],
[
 9.625,
125.334,
62.7,
4.9 
],
[
 -11.204,
162.121,
43.1,
5.1 
],
[
 -11.375,
162.569,
38.1,
4.6 
],
[
 -11.555,
162.721,
35,
5 
],
[
 49.379,
-120.465,
null,
2.5 
],
[
 -11.113,
161.884,
35.3,
4.7 
],
[
 63.443,
-148.348,
15.4,
2.8 
],
[
 -11.387,
162.536,
40.3,
4.9 
],
[
 -11.292,
162.18,
26.8,
5.9 
],
[
 -11.315,
162.211,
29.3,
7.6 
],
[
 40.299,
-124.515,
19.5,
2.8 
],
[
 36.449,
-97.063,
5,
2.9 
],
[
 -21.824,
-68.865,
160.6,
4.2 
],
[
 18.224,
-67.093,
85,
2.9 
],
[
 35.921,
-97.261,
5,
3.3 
],
[
 -7.191,
155.031,
6.7,
5.3 
],
[
 -7.141,
154.88,
22.6,
5 
],
[
 44.632,
-114.33,
5,
3.1 
],
[
 -7.1,
154.85,
43.4,
4.6 
],
[
 31.404,
-116.022,
16,
2.8 
],
[
 -6.965,
154.676,
47.2,
4.9 
],
[
 35.572,
-97.334,
5,
2.6 
],
[
 -20.572,
-70.793,
28.4,
4 
],
[
 36.287,
-97.255,
4.5,
3 
],
[
 -7.368,
155.345,
57.8,
4.6 
],
[
 53.46,
-163.418,
25.7,
2.7 
],
[
 12.026,
-87.445,
35,
4.3 
],
[
 19.059,
-67.751,
12,
2.8 
],
[
 65.363,
-151.321,
9.2,
2.8 
],
[
 -20.314,
-177.639,
515.6,
4.4 
],
[
 -6.731,
154.924,
89.9,
4.7 
],
[
 -7.153,
155.224,
41,
5.3 
],
[
 36.26,
-97.239,
2.8,
3.8 
],
[
 -7.015,
155.348,
35,
5.1 
],
[
 -7.116,
155.236,
35,
6.1 
],
[
 -7.678,
155.539,
58.9,
4.5 
],
[
 -6.923,
154.905,
75.1,
4.3 
],
[
 15.396,
-93.988,
46.3,
4 
],
[
 40.437,
-125.35,
24.7,
3.1 
],
[
 -6.801,
155.018,
50.2,
5.1 
],
[
 35.767,
-97.481,
5.3,
3 
],
[
 -15.218,
-179.576,
452.9,
4.1 
],
[
 35.768,
-97.481,
5.1,
2.5 
],
[
 -7.149,
155.253,
125.9,
4.4 
],
[
 -20.712,
-70.849,
8.4,
4.6 
],
[
 33.201,
-116.048,
8.7,
3.2 
],
[
 -22.916,
-66.586,
218.6,
4.6 
],
[
 36.514,
70.403,
203.8,
4.1 
],
[
 -6.762,
154.838,
71.8,
4.7 
],
[
 19.072,
-66.846,
13,
2.9 
],
[
 54.913,
-164.231,
157.7,
3 
],
[
 11.591,
-86.04,
135,
6.6 
],
[
 53.463,
-163.169,
36.1,
2.8 
],
[
 53.514,
-163.27,
34.9,
2.9 
],
[
 59.781,
-152.447,
100,
2.8 
],
[
 60.138,
-152.778,
100,
2.5 
],
[
 36.674,
-121.284,
8.6,
2.8 
],
[
 -6.958,
154.94,
11.1,
4.8 
],
[
 -6.839,
154.874,
12.8,
4.9 
],
[
 -6.835,
154.976,
15.8,
4.8 
],
[
 -20.151,
-70.916,
11.2,
3.9 
],
[
 65.139,
-148.467,
99.5,
2.5 
],
[
 -6.462,
155.325,
91.6,
4.7 
],
[
 12.117,
-86.509,
3.4,
4.4 
],
[
 -1.188,
149.811,
30.8,
4.9 
],
[
 -6.938,
155.022,
63.1,
4.7 
],
[
 -6.998,
155.055,
81.8,
4.9 
],
[
 -7.2,
154.87,
47.2,
4.9 
],
[
 -3.725,
119.27,
39.8,
4.5 
],
[
 41.05,
143.016,
45.5,
4.4 
],
[
 58.326,
-152.733,
5.8,
3.1 
],
[
 -6.713,
154.898,
21.3,
5.6 
],
[
 -56.954,
-24.52,
10,
5.1 
],
[
 44.654,
-114.359,
5,
2.5 
],
[
 53.501,
-163.242,
41.3,
2.5 
],
[
 53.493,
-163.224,
36.5,
2.6 
],
[
 18.774,
-65.046,
7,
2.5 
],
[
 -6.901,
154.949,
44.8,
5.5 
],
[
 -6.589,
155.06,
50.6,
4.6 
],
[
 -20.068,
-70.545,
22.3,
5.5 
],
[
 37.213,
-104.992,
7.6,
3.1 
],
[
 -6.763,
155.224,
79.7,
4.7 
],
[
 18.985,
-65.846,
15,
2.6 
],
[
 -6.887,
155.157,
35,
5.1 
],
[
 58.624,
-155.269,
100,
2.7 
],
[
 12.056,
-86.463,
21.6,
4.3 
],
[
 -6.858,
154.843,
65.7,
4.7 
],
[
 59.781,
-153.235,
100,
2.7 
],
[
 -19.976,
-70.933,
13.2,
4.9 
],
[
 52.684,
-174.382,
182.7,
2.5 
],
[
 -20.593,
-70.874,
27.6,
4.9 
],
[
 -6.727,
155.09,
44.3,
4.8 
],
[
 -6.879,
154.987,
52.6,
5.2 
],
[
 -6.852,
155.055,
45.9,
5.1 
],
[
 -6.855,
155.017,
39.4,
6.5 
],
[
 66.077,
-149.496,
20.5,
2.5 
],
[
 60.754,
-149.02,
13.1,
3 
],
[
 -6.625,
155.064,
50,
7.1 
],
[
 54.883,
-151.298,
10,
2.8 
],
[
 35.772,
-97.48,
6.2,
2.5 
],
[
 35.926,
-97.271,
4.3,
3 
],
[
 19.204,
-66.31,
40,
2.5 
],
[
 40.93,
-122.468,
18.6,
2.7 
],
[
 11.965,
-86.523,
10,
4.3 
],
[
 35.891,
-97.256,
3.1,
2.6 
],
[
 36.247,
-97.232,
5,
2.8 
],
[
 38.004,
-26.649,
10,
4.9 
],
[
 31.717,
103.337,
10,
4.6 
],
[
 19.096,
-66.484,
12,
2.8 
],
[
 -33.43,
-72.104,
25,
5.1 
],
[
 12.207,
93.148,
69.2,
4.9 
],
[
 35.896,
-97.278,
4.7,
2.6 
],
[
 59.926,
-153.111,
100,
3 
],
[
 -20.748,
-70.724,
17.5,
6 
],
[
 12.168,
-86.395,
10,
5.1 
],
[
 12.514,
-86.379,
13,
6.1 
],
[
 -19.856,
-177.297,
377.8,
4.5 
],
[
 -19.248,
-173.515,
13.9,
5.6 
],
[
 51.552,
-179.931,
211.8,
3 
],
[
 18.783,
-64.272,
41,
3.2 
],
[
 52.783,
-161.253,
25,
3.2 
],
[
 63.203,
-150.522,
121.1,
2.8 
],
[
 -3.92,
141.176,
73.3,
4.9 
],
[
 36.289,
-96.955,
8,
3.1 
],
[
 36.287,
-96.949,
8.6,
2.7 
],
[
 36.29,
-96.953,
8.1,
3.7 
],
[
 -20.035,
-70.963,
11.8,
5 
],
[
 -26.879,
-71.251,
19.8,
4.1 
],
[
 -20.054,
-71.049,
15.1,
4.3 
],
[
 36.291,
-96.948,
8,
3.1 
],
[
 59.842,
-153.137,
100,
2.8 
],
[
 -17.102,
-71.177,
96.8,
4.1 
],
[
 52.308,
179.578,
49.8,
2.8 
],
[
 52.999,
-162.148,
25,
3 
],
[
 35.784,
-97.503,
5,
2.8 
],
[
 44.635,
-114.293,
5,
4.1 
],
[
 62.675,
-149.858,
69.2,
3 
],
[
 -26.832,
-71.12,
26.4,
4.6 
],
[
 59.684,
-154.888,
100,
2.6 
],
[
 35.795,
-97.497,
7,
3.7 
],
[
 35.791,
-97.471,
3.4,
4.1 
],
[
 -20.156,
-178.323,
578.5,
4.4 
],
[
 36.282,
-97.266,
1.3,
2.6 
],
[
 51.318,
-174.717,
22.8,
2.5 
],
[
 36.277,
-97.246,
2.8,
2.6 
],
[
 36.403,
-97.148,
3.9,
3.3 
],
[
 36.275,
-97.268,
6.3,
2.7 
],
[
 35.664,
139.958,
79.6,
4.7 
],
[
 19.069,
-64.838,
51,
2.8 
],
[
 23.777,
123.141,
21.5,
4.8 
],
[
 32.107,
-115.142,
18.5,
2.9 
],
[
 19.126,
-64.797,
34,
3.2 
],
[
 -20.347,
-70.976,
11.3,
4.5 
],
[
 38.565,
55.595,
14.8,
4.4 
],
[
 14.345,
-90.403,
173.6,
4.9 
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
function drawChartGeoChartID68fee55a12e() {
var data = gvisDataGeoChartID68fee55a12e();
var options = {};
options["width"] =    556;
options["height"] =    347;
options["displayMode"] = "Markers";
options["colorAxis"] = {colors:['purple', 'red', 'orange', 'grey']};
options["region"] = "JP";
options["backgroundColor"] = "lightblue";

    var chart = new google.visualization.GeoChart(
    document.getElementById('GeoChartID68fee55a12e')
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
callbacks.push(drawChartGeoChartID68fee55a12e);
})();
function displayChartGeoChartID68fee55a12e() {
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
<script type="text/javascript" src="https://www.google.com/jsapi?callback=displayChartGeoChartID68fee55a12e"></script>
 
<!-- divChart -->
  
<div id="GeoChartID68fee55a12e"
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

<!-- Timeline generated in R 3.1.0 by googleVis 0.5.2 package -->
<!-- Wed Apr 16 22:13:09 2014 -->


<!-- jsHeader -->
<script type="text/javascript">
 
// jsData 
function gvisDataTimelineID68fe17c8da5c () {
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
function drawChartTimelineID68fe17c8da5c() {
var data = gvisDataTimelineID68fe17c8da5c();
var options = {};
options["width"] =    800;
options["height"] =    250;

    var chart = new google.visualization.Timeline(
    document.getElementById('TimelineID68fe17c8da5c')
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
callbacks.push(drawChartTimelineID68fe17c8da5c);
})();
function displayChartTimelineID68fe17c8da5c() {
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
<script type="text/javascript" src="https://www.google.com/jsapi?callback=displayChartTimelineID68fe17c8da5c"></script>
 
<!-- divChart -->
  
<div id="TimelineID68fe17c8da5c"
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

<!-- Sankey generated in R 3.1.0 by googleVis 0.5.2 package -->
<!-- Wed Apr 16 22:13:09 2014 -->


<!-- jsHeader -->
<script type="text/javascript">
 
// jsData 
function gvisDataSankeyID68fe377da37 () {
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
function drawChartSankeyID68fe377da37() {
var data = gvisDataSankeyID68fe377da37();
var options = {};
options["width"] =    400;
options["height"] =    250;

    var chart = new google.visualization.Sankey(
    document.getElementById('SankeyID68fe377da37')
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
callbacks.push(drawChartSankeyID68fe377da37);
})();
function displayChartSankeyID68fe377da37() {
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
<script type="text/javascript" src="https://www.google.com/jsapi?callback=displayChartSankeyID68fe377da37"></script>
 
<!-- divChart -->
  
<div id="SankeyID68fe377da37"
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

<!-- html table generated in R 3.1.0 by xtable 1.7-3 package -->
<!-- Wed Apr 16 22:13:09 2014 -->
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
## R version 3.1.0 (2014-04-10)
## Platform: x86_64-apple-darwin13.1.0 (64-bit)
## 
## locale:
## [1] en_GB.UTF-8/en_GB.UTF-8/en_GB.UTF-8/C/en_GB.UTF-8/en_GB.UTF-8
## 
## attached base packages:
## [1] stats     graphics  grDevices utils     datasets  methods   base     
## 
## other attached packages:
## [1] xtable_1.7-3    XML_3.98-1.1    RJSONIO_1.0-3   slidify_0.4    
## [5] googleVis_0.5.1
## 
## loaded via a namespace (and not attached):
## [1] digest_0.6.4   evaluate_0.5.3 formatR_0.10   knitr_1.5     
## [5] markdown_0.6.5 stringr_0.6.2  tools_3.1.0    whisker_0.3-2 
## [9] yaml_2.1.11
```

