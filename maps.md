# My first Leaflet maps
by MicheleVNG  
Saturday, 18 March 2017  

This is my personal version of the week 2 assignment for the [Developing Data 
Products](https://www.coursera.org/learn/data-products/) course on Coursera.

There you go:


```r
library(leaflet)
library(readr)
library(dplyr)

cities <- read_csv("comuni.csv") %>% 
	arrange(desc(`POP-Totale`)) %>% 
	select(Comune, Latitudine, Longitudine, `POP-Totale`) %>% 
	rename(lat = Latitudine,
	       lng = Longitudine,
	       pop = `POP-Totale`)
```

### Top 20 italian cities by population


```r
cities[1:20, ] %>% 
	leaflet() %>% 
	addTiles() %>% 
	addMarkers()
```

<!--html_preserve--><div id="htmlwidget-af2747b5fdb3a4fb71dd" style="width:672px;height:480px;" class="leaflet html-widget"></div>
<script type="application/json" data-for="htmlwidget-af2747b5fdb3a4fb71dd">{"x":{"options":{"crs":{"crsClass":"L.CRS.EPSG3857","code":null,"proj4def":null,"projectedBounds":null,"options":{}}},"calls":[{"method":"addTiles","args":["//{s}.tile.openstreetmap.org/{z}/{x}/{y}.png",null,null,{"minZoom":0,"maxZoom":18,"maxNativeZoom":null,"tileSize":256,"subdomains":"abc","errorTileUrl":"","tms":false,"continuousWorld":false,"noWrap":false,"zoomOffset":0,"zoomReverse":false,"opacity":1,"zIndex":null,"unloadInvisibleTiles":null,"updateWhenIdle":null,"detectRetina":false,"reuseTiles":false,"attribution":"&copy; <a href=\"http://openstreetmap.org\">OpenStreetMap\u003c/a> contributors, <a href=\"http://creativecommons.org/licenses/by-sa/2.0/\">CC-BY-SA\u003c/a>"}]},{"method":"addMarkers","args":[[41.9015,45.4655,40.8518,45.0629,38.1157,44.4057,44.4949,43.771,41.1171,37.508,45.4408,45.4384,38.1938,45.4064,45.6495,40.4658,45.5412,43.8777,38.1113,44.6488],[12.4608,9.18652,14.2681,7.67849,13.3613,8.94626,11.3426,11.248,16.8719,15.0829,12.3155,10.9917,15.554,11.8768,13.778,17.2478,10.2194,11.1022,15.6473,10.9201],null,null,null,{"clickable":true,"draggable":false,"keyboard":true,"title":"","alt":"","zIndexOffset":0,"opacity":1,"riseOnHover":false,"riseOffset":250},null,null,null,null,null,null,null]}],"limits":{"lat":[37.508,45.6495],"lng":[7.67849,17.2478]}},"evals":[],"jsHooks":[]}</script><!--/html_preserve-->

### Top 30 italian cities by population (with radius)


```r
cities[1:30, ] %>% 
	leaflet() %>% 
	addTiles() %>% 
	addCircles(weight = 1, radius = sqrt(cities[1:30,]$pop) * 60,
		   popup = paste("Population:", cities[1:30,]$pop))
```

<!--html_preserve--><div id="htmlwidget-ab4fab34315de07d1b07" style="width:672px;height:480px;" class="leaflet html-widget"></div>
<script type="application/json" data-for="htmlwidget-ab4fab34315de07d1b07">{"x":{"options":{"crs":{"crsClass":"L.CRS.EPSG3857","code":null,"proj4def":null,"projectedBounds":null,"options":{}}},"calls":[{"method":"addTiles","args":["//{s}.tile.openstreetmap.org/{z}/{x}/{y}.png",null,null,{"minZoom":0,"maxZoom":18,"maxNativeZoom":null,"tileSize":256,"subdomains":"abc","errorTileUrl":"","tms":false,"continuousWorld":false,"noWrap":false,"zoomOffset":0,"zoomReverse":false,"opacity":1,"zIndex":null,"unloadInvisibleTiles":null,"updateWhenIdle":null,"detectRetina":false,"reuseTiles":false,"attribution":"&copy; <a href=\"http://openstreetmap.org\">OpenStreetMap\u003c/a> contributors, <a href=\"http://creativecommons.org/licenses/by-sa/2.0/\">CC-BY-SA\u003c/a>"}]},{"method":"addCircles","args":[[41.9015,45.4655,40.8518,45.0629,38.1157,44.4057,44.4949,43.771,41.1171,37.508,45.4408,45.4384,38.1938,45.4064,45.6495,40.4658,45.5412,43.8777,38.1113,44.6488,44.7993,43.1107,44.699,43.5485,44.4184,39.2238,41.4622,44.0571,40.6824,44.8376],[12.4608,9.18652,14.2681,7.67849,13.3613,8.94626,11.3426,11.248,16.8719,15.0829,12.3155,10.9917,15.554,11.8768,13.778,17.2478,10.2194,11.1022,15.6473,10.9201,10.3382,12.3908,10.6297,10.3106,12.2035,9.12166,15.5446,12.5646,14.7681,11.6117],[97066.1114910863,66870.3432023494,58849.0509694082,56040.353317944,48654.0810210202,45937.4357142407,36562.4561538199,35903.8215236206,33724.7505550449,32527.6374795342,30674.1454648699,30150.8208843474,29592.9586219425,27245.0215635811,26974.8549579048,26843.1443761717,26146.6479687168,25838.7615802306,25513.5493414774,25395.5980437555,25163.9027179808,24182.9774841726,24155.64530291,23777.872066272,23525.8156075406,23228.8355282825,23007.1641016445,22417.9303237386,21849.2288193428,21844.038088229],null,null,{"lineCap":null,"lineJoin":null,"clickable":true,"pointerEvents":null,"className":"","stroke":true,"color":"#03F","weight":1,"opacity":0.5,"fill":true,"fillColor":"#03F","fillOpacity":0.2,"dashArray":null},["Population: 2617175","Population: 1242123","Population: 962003","Population: 872367","Population: 657561","Population: 586180","Population: 371337","Population: 358079","Population: 315933","Population: 293902","Population: 261362","Population: 252520","Population: 243262","Population: 206192","Population: 202123","Population: 200154","Population: 189902","Population: 185456","Population: 180817","Population: 179149","Population: 175895","Population: 162449","Population: 162082","Population: 157052","Population: 153740","Population: 149883","Population: 147036","Population: 139601","Population: 132608","Population: 132545"],null,null,null,null,null]}],"limits":{"lat":[37.508,45.6495],"lng":[7.67849,17.2478]}},"evals":[],"jsHooks":[]}</script><!--/html_preserve-->
