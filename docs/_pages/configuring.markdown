---
# Feel free to add content and custom Front Matter to this file.
# To modify the layout, see https://jekyllrb.com/docs/themes/#overriding-theme-defaults

permalink: /configuring/
layout: home
title: Configuring TRIRIGA Indoor Maps
description: How to configure TRIRIGA Indoor Maps for your IBM TRIRIGA solution.

sidebar:
  nav: "docs"
---
## Building and Floor fields to Esri ArcGIS values reference table

BO | Field | Comment 
------- | --------- | -------- 
triBuilding | GIS Latitude (triGisLatitudeNU) | This is an existing field.  It can be easily obtained by googling the address and looking in the URL. You may have to tweak the link to get to the preferred position.
triBuilding | GIS Longitude (triGisLongitudeNU) | This is an existing field.  It can be easily obtained by googling the address and looking in the URL. You may have to tweak the link to get to the preferred position.
triBuilding | Esri Map ID (triEsriMapIdTX) | This is a new field. For adding, refer to the installation instructions. See the following instructions for configuring. (Ex. 403b6012276b4339af152e9c3319a4b1)
triBuilding | Esri Portal URL (triEsriPortalUrl) | This is a new field. For adding, refer to the installation instructions. The URL is determined during Esri installation. (Ex. https://host.domain/portal)
triBuilding | Esri Network URL (triEsriNetworkUrl) | This is a new field. For adding, refer to the installation instructions. See the following instructions for configuring. 
triBuilding | Esri Building ID (triEsriBuildingID) | This is a new field. For adding, refer to the installation instructions.  See the following instructions for configuring. (Ex. NC_CHARLOTTE_ONE)
triFloor | Esri Floor ID (triEsriFloorID) | This is a new field. For adding, refer to the installation instructions.  See the following instructions for configuring. (Ex. NC_CHARLOTTE_ONE.1)
triBuilding | Esri Building Default Zoom (triEsriZoomNU) | This is a new field. For adding, refer to the installation instructions.  Depends on the footprint of the building, 20 is probably fine for most buildings, however, needs to be experimented with.
triBuilding | Esri Building Default Rotation (triEsriRotationNU) | This is a new field. For adding, refer to the installation instructions.  Depends on the shape of the building and the most common screen format that people will view it in.  If the building is wider East to West, it probably makes sense to rotate it 90 degrees.  Experiment with it to find the best value for the most common medium.



## Obtaining Esri Map ID

1. Navigate to your Esri installation's portal, e.g. `https://host.domain/portal`.
1. Click `Sign In` on top right of the landing page.
![alt]({{ site.url }}{{ site.baseurl }}/assets/images/configuration/image1.png)
1. Log in as an `admin` or any user that is able to see the organization's content.
![alt]({{ site.url }}{{ site.baseurl }}/assets/images/configuration/image2.png)
1. Click `Content` on the navigation bar at the top of the page.
![alt]({{ site.url }}{{ site.baseurl }}/assets/images/configuration/image3.png)
1. Click `My Organisation` on the navigation sub-bar.
![alt]({{ site.url }}{{ site.baseurl }}/assets/images/configuration/image4.png)
1. Filter the content by clicking `Maps -> Web Maps` on the left side.
![alt]({{ site.url }}{{ site.baseurl }}/assets/images/configuration/image5.png)
1. Select the `Web Map` that you wish to configure in TRIRIGA. Click on the title under the thumbnail (do not click the thumbnail itself or the map viewer will open instead).  In the following screenshot, the content is displayed in Grid view, but the view can be toggled at the top of the screen (List, Grid, Table).
![alt]({{ site.url }}{{ site.baseurl }}/assets/images/configuration/image6.png)
1. From the URL of the web browser, note the `id` parameter value. This is the value that must be entered in the Esri Map ID in TRIRIGA.  In the following example, it is 9a8068284e614be3bdcb1cd26f05499a.
![alt]({{ site.url }}{{ site.baseurl }}/assets/images/configuration/image7.png)

## Obtaining Esri Building ID and Esri Floor ID

1. Follow the steps from 1 to 8 given in the section Obtaining Esri Map ID.
1. On the Web Map details screen, click on the link to the main layer under `Layers`. In the following example, the link is called TRIRIGA_Demo_Web_Map_MIL1.
![alt]({{ site.url }}{{ site.baseurl }}/assets/images/configuration/image8.png)
1. A similar screen is displayed, however, note the change in title. This is the details screen for the Layer you clicked on in step-2, not the Web Map.  On this screen, click on the link to the main layer under the `Layers` section. In the following example, the link is called TRIRIGA_Demo_Web_Map_MIL1.
![alt]({{ site.url }}{{ site.baseurl }}/assets/images/configuration/image9.png)
1. This opens the REST services descriptor which describes the technical information about the service.  Click `Levels` under the `Layers` section.
**Note**: If this doesn't exist, then no building levels have been published for this web map, you must consult the administrator.
![alt]({{ site.url }}{{ site.baseurl }}/assets/images/configuration/image10.png)
1. This opens another REST services descriptor which describes technical information about the Levels layer.  Scroll to the bottom of this screen.
![alt]({{ site.url }}{{ site.baseurl }}/assets/images/configuration/image11.png)
1. In the Supported Operations section, click `Query`.
![alt]({{ site.url }}{{ site.baseurl }}/assets/images/configuration/image12.png)
1. This opens a form that allows the layer to be queried. Fill the details as:
  * In the Where field, add the value 1=1
  * In the Out Fields field, add the value FACILITY_ID, LEVEL_ID (do not omit the comma)
![alt]({{ site.url }}{{ site.baseurl }}/assets/images/configuration/image13.png)
1. In the `Where` field add the value `1=1` as shown below.
![alt]({{ site.url }}{{ site.baseurl }}/assets/images/configuration/image14.png)
1. In the `Out Fields` field add the value `FACILITY_ID, LEVEL_ID` (do not omit the comma) .
![alt]({{ site.url }}{{ site.baseurl }}/assets/images/configuration/image15.png)
1. All other fields must be left as default values.  Scroll to the bottom and click `Query (GET)`.
![alt]({{ site.url }}{{ site.baseurl }}/assets/images/configuration/image16.png)
1. The page will reload. Scroll to the bottom of the screen to see the records that matched. This is a list of each facility and level.
![alt]({{ site.url }}{{ site.baseurl }}/assets/images/configuration/image17.png)
1. Choose whichever facility and level you need for the configuration. If this was a campus that was published, there may be more than one facility defined in this layer, but TRIRIGA works on a building by building basis, so choose the details for your current building.  
1. Enter the FACILITY_ID in the `Esri Building ID` field and the LEVEL_ID in the `Esri Floor ID` field.

## Obtaining Esri Network URL

1. Follow the steps from 1 to 5 given in the section Obtaining Esri Map ID.
1. Filter the content by clicking `Tools -> Network Analysis` on the left side.
![alt]({{ site.url }}{{ site.baseurl }}/assets/images/configuration/image18.png)
1. Select the Network Analysis Service for your map. In the grid view, click on the title under the thumbnail (do not click the thumbnail itself or the map viewer will open instead).  In the following screenshot,the content is displayed in Grid view, but the view can be toggled at the top of the screen (List, Grid, Table).
![alt]({{ site.url }}{{ site.baseurl }}/assets/images/configuration/image19.png)
1. On the details screen, click on the link to the navigation layer under the `Layers`. In the following example, the link is called TRIRIGA_Demo_Network.
![alt]({{ site.url }}{{ site.baseurl }}/assets/images/configuration/image20.png)
1. This opens a REST services descriptor which describes technical information about the navigation layer.  Click `Route link` under `Route Layers` section.
![alt]({{ site.url }}{{ site.baseurl }}/assets/images/configuration/image21.png)
1. This opens another REST services descriptor which describes technical information about the route solver part of the navigation service. Note full URL from the browser's URL field.
![alt]({{ site.url }}{{ site.baseurl }}/assets/images/configuration/image22.png)
1. The URL captured in step-7 must be entered in the `Esri Navigation Url` field.