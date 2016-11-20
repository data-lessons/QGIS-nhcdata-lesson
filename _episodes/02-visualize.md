---
title: "Next"
teaching: 0
exercises: 0
questions:
- "Key question"
objectives:
- "First objective."
keypoints:
- "First key point."
---
To get started, open the processing toolbox. You will use the search feature to find the tools we’re running in this section of the tutorial. This tutorial only uses native QGIS algorithms but other analysis packages, such as GRASS and SAGA, offer additional tools you can install and explore (which require dependencies). Many of these algorithms can take up to several minutes to run on this dataset. 

**We are emphasizing exploration by date; place; and taxon**

### Assessing the subset
Now that we have created a subset of the occurrences within Santa Barbara County, these data have the EPA Ecoregions appended to the attribute table. Open the attribute table for SB_Eco_join. Scrolling to the far right, you will see that each point now has bioregion attributes. Take some time to explore the occurrences and query by ecoregion. **Do the types of occurrences make sense for the given biomes?**

### Symbolize by collection, collector, class
In the Properties of SB_Eco_join, we can change the symbology to reflect the distribution of occurrences by collection. In Style, change from Single Symbol to Categorized. The column to visualize is dwc_collec or dcterms_1 for collection and dwc_iden_6 for collector or dwc_class for Class. **Do you notice any clusters by collection? By collector? By class? By any other attribute?**

### Popups for localities 
In the Properties for SB_Eco_join, go to Display and select dwc_locali as the Field for Map Tips. This will enable you to preview the locality description of occurrences. You can choose another attribute to preview in this way as well. Also, click the Map Tips button to enable the Map Tips. **Check the locality descriptions against the Gazetteer, the OSM Basemap, the Ecoregions; does it make sense?**

### Aggregation
**How many observations occurred in each county? Do any counties have a disproportionate amount?**

* Goal: find biases in collection as a first pass
* Tool: Count Points In a Polygon, (Join By Location, Select/Extract by Attribute/Location)
* Output: Shapefile with attribute table

To open the toolbox panel, go to Processing > Toolbox. Search for the count points in a polygon tool. This tool summarizes the number of points that intersect each polygon in the feature of interest and writes a new shapefile of counties that contains the sum of points as an attribute in the attribute table. Below, that field is “Numpoints.” 

Open attribute table and navigate to the “Numpoints” field. Sort by value by clicking on the header name to find the counties with the greatest and fewest number of observations. 

Move layer beneath the points to visualize which points correspond to which county. Changing the order of the layers in the left panel orders the way they are drawn on the canvas. You toggle them on and off by checking or unchecking the layers as well. 

### Symbology
**Which counties have the greatest number of observations? Which points have the greatest coordinate uncertainty in meters?**

* Goal: visualize systematic biases or errors
* Tool: Style (Single Symbol, Categorized, Graduated, Proportional Circles)
* Output: same layer with updated properties

Now that the counties contain information for aggregated point counts, we can change the layer symbology to reflect the information. Right click on “occurrence_raw.csv” to select “Properties”.

In the style tab, change from Single Symbol to Graduated. This allows you to pick a number of classes to style your data. Experiment with different numbers of breaks (7+/- 2 for legibility), color ramps (continuous), and distribution modes (natural breaks - jenks). This allows you to easily visualize which counties have the greatest and fewest observation points. We can use this in combination with the Identify tool to explore the number of observations in each county.

Next, try changing the symbology of the occurrences_raw.csv points to find which have the highest coordinate uncertainty to create a proportional symbol map that scales the radius of the point based on the uncertainty. The symbology options may vary between QGIS versions. This will highlight points with low positional precision. 

Select features of interest in the attribute table and highlight them on the map. You can for instance filter your data by removing records below a given threshold of precision. You can also use the Identify tool to click on specific points and see their attributes displayed in the left panel. 

### Intersection, Subsetting
**Which observations occurred in Santa Barbara County? Around particular state or federal parks?**

* Goal: subset data 
* Tool: Extract By Attribute, Intersection, Select By Location - make a selection, save out, table edit
* Output: same layer with updated properties

As we found in the previous step of aggregation, there are 662 observations in Santa Barbara County.  Create a subset of data of just the points that occur in Santa Barbara County on which we can perform additional analysis. Find the Extract by attribute tool in the Processing toolbox. You will extract Santa Barbara County from the set of counties in CA counties. Save the new output selection as a layer named “Santa Barbara County” that you can use to clip and subset occurrence_raw points.

Next, open the Intersection tool. Select the “occurrences_raw” as the input layer and “Santa Barbara  County” as the intersect layer. This will write the intersection of the layers to a new file.

We also select Santa Barbara County by building a query from the attribute table.

### Time Animation
**Are there biases in the collection by collector or errors with dates or transcriptions? Which points were collected by the same collector or have low data quality scores? (For all records before 1940, what institutions? - by institution code), bias based on institutional protocols - build a query**

* Goal: visually assess data quality or outliers
* Tool: TimeManager (requires installation of Plugin; go to Manage and Install Plugins and search) - warning: this dataset is very large, so running TimeManager can be somewhat slow
* Output: same layer with time enabled symbology for attribute of interest

Toggle on TimeManager Plugin from the menu; this will open the interactive panel. 

Choose a time field (i.e. dwc:dcterms_mo, dwc:eventDate, dwc:year) from the “occurrences_raw.csv” to use as a timestamp. You can choose a start time of interest and see which observations correspond to this start date. This is another means of revealing patterns in your symbolized data.

### Centroids
**Are the observations georeferenced to a county or state level?**

* Goal: find points that are not descriptively georeferenced
* Tool: Polygon centroids; (Dissolve)
* Output: a new shapefile with points that describe the geometric center of each polygon

Open the Polygon centroids tool from the processing toolbox. Use the CA Counties layer as your input and save out the centroids to a new shapefile in your same folder directory.

### Buffer
**What is the acceptable distance from the centroid as a proxy measure of granularity?**

* Goal: find points that are within an acceptable threshold distance from the centroid of the counties
* Tool: Buffer(s)
* Output: a new shapefile of polygons with areas of a given search radius around each centroid

Open the Fixed Distance Buffer tool from the processing toolbox. You are prompted to select a Buffer distance. To find out the project properties and units, navigate to Project > Project Properties > General. You will see that CRS transformation is enabled (your layers are projected on the fly) and your canvas map units are in Meters. Your projection is Pseudo Mercator, so your map units are in Decimal Degrees.

As a first pass, generate a 0.08 degree buffer (approximately 5.5 miles) around each centroid. Since this is a proxy measure for granularity, you can choose any buffer radius that makes sense.

### Intersect
**Do any observation points Intersect the buffer? If so, is the precision of these observations suspect?**

* Goal: find points that intersect the threshold distance
* Tool: Intersect
* Output: a selection of points (highlighted in the attribute table) that intersect the search radius

Find the Select by Location tool in the Processing Toolbox. Specify the occurrences_raw.csv points as the layer to select from and the Buffer as the intersection layer.

We can now review the 1939/21518 subset of occurrences that are geocoded to within a 5 mile radius of the county centroid. Filter in the attribute table to sort “Show Selected Features”. At the top of the table, the number of selected features is reported. Review the Longitude and Latitude of the coordinates and note the precision. Is it spurious? What is the date of the record?

### Bin by Uncertainty
**How many points are over an acceptable threshold of uncertainty? (by taxa, genus, collector, year…) Cluster around… distribution of genus separately and evaluate for outliers - data cleaning**

* Goal: find categories of points to manually evaluate
* Tool: Field Calculator, Basic Statistics for Numeric Field
* Output: an html file with statistics for the selection

Open Field Calculator. In order to perform any numeric analysis on our occurrences_raw.csv points, they need to be interpreted as numbers rather than as strings. We can convert the field without overwriting it by creating a new column in our attribute table. Know that you can also apply functions to existing columns using the Field Calculator. 

Open Basic Statistics for Numeric Field. Choose a field of interest, such as coordinate uncertainty in meters on which to perform the analysis.

### Heatmap
**Are there any clusters or hotspots of observations?**

* Goal: find categories of points to manually evaluate
* Tool: Field Calculator, Summary Statistics - attribute table
* Output: an html file with statistics for the selection

Heatmaps are used to identify clusters or hotspots. In the Heatmap Plugin dialog, enter 50,000 meters as the Radius. Radius is the area around each point that will be used to calculate the ‘heat’ a pixel received.

Change the symbology to a pseudocolor ramp and classify to make the heatmap more legible.

You can experiment with different search radii or pixel sizes by enabling advanced features.

## Next Steps
Now that you can select and subset the records, let’s see how we can edit the data and save it back out to a CSV file. 

### Editor
**How to make edits to the CSV and save out (back to table)?**

Using the editor tool

## Additional QGIS resources
Mango Maps [videos](http://qgis-tutorials.mangomap.com/)
- <i>A series of videos that explain basic QGIS operations</i>

Stack Overflow for [GIS](http://qgis-tutorials.mangomap.com/)
- <i>A helpful community forum for posting GIS questions</i>
