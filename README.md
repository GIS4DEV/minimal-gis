# MiMiGIS (Middlebury Minimal GIS)
[download](https://github.com/GIS4DEV/MiMiGIS/archive/main.zip)

This QGIS plugin, designed for use in introductory GIS courses, contains a Group By tool and a Direction and Distance tool, as well as installation of a set of Mapbox Maki icons and National Park Service (NPS) icons. We plan to [expand the functionality](development_agenda.md) of this plugin over time with more tools and resources. For more information about the project, check out our blog posts [here](https://majacannavo.github.io/jterm21main) and [here](https://www.josephholler.com/a-minimal-gis-plugin-for-qgis/).

The `Group By` and `Distance and Direction` algorithms were written by Maja Cannavo and Joseph Holler, and the plugin was built by Maja Cannavo using [Plugin Builder](https://github.com/g-sherman/Qgis-Plugin-Builder).
The Maki icons were downloaded [here](https://labs.mapbox.com/maki-icons/) from Mapbox, and the NPS icons were downloaded [here](https://www.nps.gov/carto/app/#!/maps/symbols) from NPS. Both sets of icons were then edited by Joseph Holler to allow for color customization in QGIS.

Authors: [Maja Cannavo](mailto:mcannavo@middlebury.edu) and [Joseph Holler](mailto:josephh@middlebury.edu), Middlebury College, Middlebury, VT

Plugin/algorithm icons--all under CC0 license from [SVG Repo](https://www.svgrepo.com/):
[M icon](https://www.svgrepo.com/svg/5274/medium-size), [sigma icon](https://www.svgrepo.com/svg/175093/sigma-maths), [compass rose icon](https://www.svgrepo.com/svg/253234/wind-rose-compass)

This plugin was developed and tested using QGIS 3.10.9; compatibility with other versions is not guaranteed.

## Group By:
Group features with common values in the group field(s). Optionally, dissolve geometries and calculate summary statistics for numeric fields. All outputs will have a "featCount" field with the number of features in each group.

### Example: Grouping parcels in Central Falls, RI, by zone (NE, NW, SE, or SW) and calculating feature count and average for number of bedrooms and total value.
Example Input | Example Output
--- | ---
![](markdown_visuals/images/parcels_notdissolved_jpg.jpg) | ![](markdown_visuals/images/parcels_dissolved.jpg)
![](markdown_visuals/tables/before_table.png) | ![](markdown_visuals/tables/after_table.png)

### Algorithm Parameters:
Parameter | Description | Data Type | Python Identifier
--- | --- | --- | ---
Input layer | Input layer with features to be dissolved. | Vector | 'INPUT'
Group Fields (optional) | In which field(s) do you want to search for values with which to form the new groups? A new group will be formed for each combination of values in the group field(s). If you do not select any group fields, the output will be a single feature. | Field(s) | 'GROUPFIELDS'
Summary Fields (optional) | Which numerical field(s) do you want to calculate summary statistics for? | Numerical field(s) | 'SUMMARYFIELDS'
Dissolve Geometry | Do you want to dissolve the geometries (geographic data) associated with the features? Disjoint geometries are still dissolved into multi-part features. If this option is unchecked, the output will be a table with no geographic data. | Boolean | 'DISSOLVEGEOMETRY'
Average | Calculate the average or mean of your summary field(s)? | Boolean | 'AVERAGE'
Count Values | Count non-null values in your summary field(s)? | Boolean | 'COUNTVALUES'
Sum | Calculate the sum of your summary field(s)? | Boolean | 'SUM'
Maximum | Calculate the maximum of your summary field(s)? | Boolean | 'MAXIMUM'
Minimum | Calculate the minimum of your summary field(s)? | Boolean | 'MINIMUM'
Grouped Output | Grouped output. If you are not dissolving geometries, then save the output as a .csv, .xlsx, or database table. | Feature Sink | 'OUTPUT'    


## Direction and Distance:
Calculates the distance (in meters) and direction (in degrees) from an origin to a set of input features. Distance calculation is ellipsoidal, using the WGS 1984 geographic coordinate system (EPSG:4326). Direction calculation uses the World Mercator projected coordinate system (EPSG:3395).

### Example: Calculating direction and distance from Chicago's central business district to each of the city's census tracts.
Example Direction Result | Example Distance Result
--- | ---
![](markdown_visuals/images/tracts_dir_jpg.jpg) | ![](markdown_visuals/images/tracts_dist_jpg.jpg)
Example Input Attribute Table | Example Output Attribute Table
![](markdown_visuals/tables/before_table_2.png) | ![](markdown_visuals/tables/after_table_2.png)

### Algorithm Parameters:
Parameter | Description | Data Type | Python Identifier
--- | --- | --- | ---
Input Layer | Layer of features for which to calculate direction and distance from the origin. | Vector | 'INPUT'
Origin | Origin feature from which to calculate direction and distance. | Vector | 'ORIGIN'
Prefix | The algorithm creates two new fields, one with suffix 'Dist' for Distance and one with suffix 'Dir' for Direction. Enter a prefix to use for the field names, such that you will not create duplicate fields in your output. | String | 'PREFIX'
Dir/Dist Output | New layer with direction and distance fields. | Feature Sink | 'OUTPUT'

## Maki/NPS Icons:
MiMiGIS.zip contains folders with the Maki and NPS icons. The plugin automatically adds the paths to these directories to the list of SVG paths in your QGIS preferences. For reference, the Maki icons are located at MiMiGIS/SVG/maki_icons, and the NPS icons at MiMiGIS/SVG/NPS_icons.
