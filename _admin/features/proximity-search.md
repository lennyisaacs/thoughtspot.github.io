---
title: [Proximity searches "near" and "farther than"]
keywords: within,near,"farther than",proximity,geo,search
last_updated: tbd
summary: "If your table contains Latitude and Longitude data, you can use proximity searches that find entities related to each other by location."
sidebar: mydoc_sidebar
permalink: /:collection/:path.html
---
Proximity keywords allow you to search search and then show on map (via search)
all instances of a measure near an attribute's associated lat/long coordinates
within _x_ miles/km/meters. Using proximity keywords causes ThoughtSpot to display a circle
that represents your set distance on the geo charts when you filter on a GeoType
column.

![]({{ site.baseurl }}/images/geospatial_search.png "Geospatial search on a geo area map")

The proximity keywords are.

-   `near`
-   `near…within n miles|km|meters`
-   `farther than n miles|km|meters from`

The distance is calculated as a straight-line distance (not road distance)
radius using miles, kilometers, or meters from the central point. If not
specified, the default is 10 km.

These keywords are limited to 33 latitude/longitude pairs. They work on
duplicate counties. Finally, you can filter on them. Some examples of valid
searches are:

`landings` _`latitude longitude city`_ `near tokyo`

`landings` _`latitude longitude city`_ `near tokyo within 50 miles`

 You can bracket your search only with actual values found in the data.  So
 "longitude between `-125.000000` and `-115.316670` worked for me, but not
 `longitude between -125 and -115`.

### Proximity search configuration requirements

All your data must be in the same set. The worksheet or one of the tables must
contain a column of type `longitude` and a column of type `latitude`. The
latitude and longitude data have to be on the same base tables for the feature
to work. You can't, for instance, have a dimension table with all your cities
and their associated geo coordinates and join to it from your fact table and
expect proximity search to work.

Also, your administrators must have configured these columns using the
appropriate GeoType.