We INSERT GOVERNMENT AGENCY may have the opportunity to talk briefly with the 
INSERT PROMISING CONTRACT VEHICLE responsible for providing PostgreSQL as part 
of our INSERT PLAN OF THE MONTH. 

"I’ve already got the use of the PostGIS extension on the list of features that 
our team would want. Are there any other features or configurations that you 
think should be included with a PostgreSQL installation?"




## PostGIS

### Motivation 

Duh.  See the intro, just putting this at the top as a reminder.

### Considerations

* See section 2.2 [of the docs](https://postgis.net/docs/postgis_installation.html#install_short_version) 
"Install Requirements"





## PostgreSQL OGR Foreign Data Wrapper 

### Motivation 

A PostgreSQL database with PostGIS and the OGR Foreign Data Wrapper makes 
the PostgreSQL database interoperable with almost all vector spatial data formats.
It exposes vector GIS formats (shapefiles, Oracle sdo_geometry, etc) as tables
in PostgreSQL. 

This would streamline the transition from legacy data sinks like Oracle
and ESRI-focused shops to open and cloud-friendly environments.  From a marketing 
perspective we might engage in a little big of puffery and suggest that a PostGIS 
database with the OGR_FDW wrapper is a fully open source Database + [FME Server](https://www.safe.com/fme/fme-server/) bundle.

For a fun use case check out the lovable galaxy brains on the Oracle 
Spatial user forum suggesting using OGR_FDW to leverage exciting new PostGIS 
functions like Voronoi Polygon generators to read and write data in their stodgy 
old Oracle databases.  https://community.oracle.com/thread/4166457

### Background/Reminders 

* Link: https://github.com/pramsey/pgsql-ogr-fdw

* Foreign Data Wrappers: https://wiki.postgresql.org/wiki/Foreign_data_wrappers

* OGR = (O)pen(G)IS Simple Features (R)eference Implementation 

* OGR = abstract data model for reading and writing vector geospatial formats 

### Considerations

* Requires the PostGIS extension to use

* In order to build the extension you must have GDAL libraries, GDAL development 
packages, and the PostgreSQL development packages.




## PostGIS Topology

### Motivation 

"The PostGIS Topology types and functions are used to manage topological objects 
such as faces, edges and nodes."  It's common for government agencies 
responsible for maintaining street networks, tax lots, and so on to use a topology 
to enforce topological rules like "tax lots do not overlap." 

Topologies are also useful when performing geometric simplification.  By 
simplifying the topological primitives we can reduce the complexity (amount)
of spatial data without changing the spatial relationships between higher-level
spatial features.

For a fun example of topology run amok check out this [ProPublica article](https://www.propublica.org/article/trump-inc-podcast-one-trump-tax-cut-meant-to-help-the-poor-a-billionaire-ended-up-winning-big) 
describing the use over tiny overlaps in spatial data to leverage tax benefits.
(Skip to "Bank Error in Your Favor")

### Background/Reminders 

* Docs: https://postgis.net/docs/Topology.html

### Considerations

* postgis_topology is included with the postgis installation

* "CREATE EXTENSION postgis_topology;" to enable

* See https://postgis.net/docs/postgis_installation.html




## PostGIS Raster

### Motivation 

There are limited cases where raster processing in a database is sensible. Typically 
this means avoiding nonsensical plans like storing gobs of binary data in 
a database but instead doing sensible work like vectorizing raster data or performing 
analyses that involve both raster and vector data.

### Considerations

* In the current PostGIS releases raster functions are included in the extension

* As of PostGIS 3.0 raster functionality is no longer bundled with the postgis extension

* Like the topology extension above, in 3.0+ raster is included with the postgis 
build but must be enabled with "CREATE EXTENSION postgis_raster;"

* https://postgis.net/2019/05/26/postgis-3.0.0alpha1/