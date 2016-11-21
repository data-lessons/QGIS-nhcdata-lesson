---
layout: page
title: Setup
permalink: /setup/
---
### Dataset
iDigBio search parameters and resulting [dataset.](http://s.idigbio.org/idigbio-downloads/a69d1541-4726-465d-84ad-50c7ed556eee.zip)

	{"core_type": "records", "record_fields": null, "rq": {"stateprovince": "california", "geopoint": {"type": "exists"}, "data": {"type": "fulltext", "value": "carabidae"}}, "form": "dwca-csv", "mq": null, "core_source": "indexterms", "mediarecord_fields": null}

Move your downloaded data (the iDigBio dataset and auxiliary layers) into a workspace (such as a folder on desktop). This will serve as your working directory where you will also store your project file. Unzip the iDigBio zipped file in your directory. You can leave the auxiliary data (shapefiles, rasters) as zipped.

### Set a working folder
Move your downloaded data (the iDigBio dataset and auxiliary layers) into a workspace (such as a folder on desktop). This will serve as your working directory where you will also store your project file. Unzip the iDigBio zipped file in your directory. You can leave the auxiliary data (shapefiles, rasters) as zipped.

### Launch QGIS
The community updates the version of QGIS every year. The version I am using is 2.4.0-Chugiak, but newer versions are available. There may be slight differences in versions. You can check your version using QGIS > About QGIS. The following plugins will have to be enabled in order to use them.

### Check QGIS Plugins
Under Plugins in the dropdown menus, navigate to Manage and Install Plugins. Under Installed, ensure that the box next to each plugin is checked. You can install and update supported plugins via this panel: 

* [Clipper](https://plugins.qgis.org/plugins/clipper/) (clip intersecting vector features)
* [Coordinate Capture](https://docs.qgis.org/2.2/en/docs/user_manual/plugins/plugins_coordinate_capture.html?highlight=coordinate) (find coordinates in various coordinate reference systems)
* [GPS Tools](http://docs.qgis.org/2.0/en/docs/user_manual/working_with_gps/plugins_gps.html?highlight=GPS) (loading and importing GPS data)
* [Heatmap](http://documentation.qgis.org/2.0/en/docs/user_manual/plugins/plugins_heatmap.html?highlight=heatmap) (generate a heatmap raster given input vector points)
* [Interpolation](http://documentation.qgis.org/2.0/en/docs/user_manual/plugins/plugins_interpolation.html?highlight=interpolation) (interpolation techniques given vertices of a vector layer)
* [OpenLayers](http://documentation.qgis.org/2.0/en/docs/training_manual/qgis_plugins/plugin_examples.html?highlight=openlayers) (load basemaps from OpenStreetMap, Google, etc.)
* [TimeManager](https://plugins.qgis.org/plugins/timemanager/?highlight=time) (event-visualization animation for vector features)
* [Gazetteer Search](https://github.com/AstunTechnology/QGIS-Gazetteer-Plugin#Installation) (finding named places from multiple gazetteers via a text search bar)
* [Lifemapper](http://plugins.qgis.org/plugins/lifemapperTools/) (a custom georeferencing tool developed by domain experts)
* Processing (spatial data processing framework)
