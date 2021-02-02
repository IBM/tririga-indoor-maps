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

## Obtaining Esri Map ID

1. Open a web browser.
1. Navigate to your Esri installations Portal e.g. `https://host.domain/portal`
1. Click the `Sign In` on the top right of the landing page.
![alt]({{ site.url }}{{ site.baseurl }}/assets/images/configuration/image1.png)
1. Log in as `admin` or any user that is able to see the organisation's content.
![alt]({{ site.url }}{{ site.baseurl }}/assets/images/configuration/image2.png)
1. Select `Content` from the navigation bar at the top of the page.
![alt]({{ site.url }}{{ site.baseurl }}/assets/images/configuration/image3.png)
1. Select `My Organisation` on the navigation sub-bar.
![alt]({{ site.url }}{{ site.baseurl }}/assets/images/configuration/image4.png)
1. Filter the content by clicking `Maps -> Web Maps` on the left hand side.
![alt]({{ site.url }}{{ site.baseurl }}/assets/images/configuration/image5.png)
1. Select the `Web Map` that you wish to configure in TRIRIGA - click on the title under the thumbnail (do not click the thumbnail itself or the map viewer will open instead).  Note assumes the content is displayed in Grid view below but the view  can be toggled at the top of the screen (List, Grid, Table).
![alt]({{ site.url }}{{ site.baseurl }}/assets/images/configuration/image6.png)
1. Look in the URL field of the web browser and note the `id` parameter value - this is the value that should be entered into the Esri Map ID in TRIRIGA.  In the example below it is 9a8068284e614be3bdcb1cd26f05499a.
![alt]({{ site.url }}{{ site.baseurl }}/assets/images/configuration/image7.png)

## Obtaining Esri Building ID & Esri Floor ID
1. Open a web browser.
1. Navigate to your Esri installations Portal e.g. `https://host.domain/portal`
1. Click the `Sign In` on the top right of the landing page.
![alt]({{ site.url }}{{ site.baseurl }}/assets/images/configuration/image1.png)
1. Log in as `admin` or any user that is able to see the organisation's content.
![alt]({{ site.url }}{{ site.baseurl }}/assets/images/configuration/image2.png)
1. Select `Content` from the navigation bar at the top of the page.
![alt]({{ site.url }}{{ site.baseurl }}/assets/images/configuration/image3.png)
1. Select `My Organisation` on the navigation sub-bar.
![alt]({{ site.url }}{{ site.baseurl }}/assets/images/configuration/image4.png)
1. Filter the content by clicking `Maps -> Web Maps` on the left hand side.
![alt]({{ site.url }}{{ site.baseurl }}/assets/images/configuration/image5.png)
1. Select the `Web Map` that you wish to configure in TRIRIGA - click on the title under the thumbnail (do not click the thumbnail itself or the map viewer will open instead).  Note assumes the content is displayed in Grid view below but the view  can be toggled at the top of the screen (List, Grid, Table).
![alt]({{ site.url }}{{ site.baseurl }}/assets/images/configuration/image6.png)
1. On the Web Map details screen, click on the link to the main layer in the `Layers` section - in the example below the link is called TRIRIGA_Demo_Web_Map_MIL1.
![alt]({{ site.url }}{{ site.baseurl }}/assets/images/configuration/image8.png)
1. A similar screen will open however note the change in title - this is the details screen for the Layer you clicked on above, not the Web Map.  On this screen, click on the link to the main layer in the `Layers` section - in the example below the link is called TRIRIGA_Demo_Web_Map_MIL1.
![alt]({{ site.url }}{{ site.baseurl }}/assets/images/configuration/image9.png)
1. This opens the REST services descriptor which describes technical information about the service.  Click on the `Levels` layer in the `Layers` section.  If this doesn't exist then no building levels have been published for this web map - see the administrator.
![alt]({{ site.url }}{{ site.baseurl }}/assets/images/configuration/image10.png)
1. This opens another REST services descriptor which describes technical information about the Levels layer.  Scroll to the bottom of this screen.
![alt]({{ site.url }}{{ site.baseurl }}/assets/images/configuration/image11.png)
1. In the Supported Operations section click the `Query` link.
![alt]({{ site.url }}{{ site.baseurl }}/assets/images/configuration/image12.png)
1. This opens a form that allows the layer to be queried.
![alt]({{ site.url }}{{ site.baseurl }}/assets/images/configuration/image13.png)
1. In the `Where` field add the value `1=1` as below.
![alt]({{ site.url }}{{ site.baseurl }}/assets/images/configuration/image14.png)
1. In the `Out Fields` field add the following value (do not omit the comma) `FACILITY_ID, LEVEL_ID`.
![alt]({{ site.url }}{{ site.baseurl }}/assets/images/configuration/image15.png)
1. All other fields should remain as default values.  Scroll to the bottom and click the `Query (GET)` button.
![alt]({{ site.url }}{{ site.baseurl }}/assets/images/configuration/image16.png)
1. The page will reload and scrolling to the bottom of the screen should show the records that matched - this is a list of each facility and each level.
![alt]({{ site.url }}{{ site.baseurl }}/assets/images/configuration/image17.png)
1. Choose whichever Facility and Levels you need for the configuration - if this it was a campus that was published, there may be more than one facility defined in this layer but TRIRIGA works on a building by building basis, so choose the details for your current building.  
1. The FACILITY_ID goes into the `Esri Building ID` field.
1. The LEVEL_ID goes into the `Esri Floor ID` field.

## Obtaining Esri Network URL
1. Open a web browser.
1. Navigate to your Esri installations Portal e.g. `https://host.domain/portal`.
1. Click the `Sign In` on the top right of the landing page.
![alt]({{ site.url }}{{ site.baseurl }}/assets/images/configuration/image1.png)
1. Log in as `admin` or any user that is able to see the organisation's content.
![alt]({{ site.url }}{{ site.baseurl }}/assets/images/configuration/image2.png)
1. Select `Content` from the navigation bar at the top of the page.
![alt]({{ site.url }}{{ site.baseurl }}/assets/images/configuration/image3.png)
1. Select `My Organisation` on the navigation sub-bar.
![alt]({{ site.url }}{{ site.baseurl }}/assets/images/configuration/image4.png)
1. Filter the content by clicking `Tools -> Network Analysis` on the left hand side.
![alt]({{ site.url }}{{ site.baseurl }}/assets/images/configuration/image18.png)
1. Select the Network Analysis Service for your map - in grid view click on the title under the thumbnail (do not click the thumbnail itself or the map viewer will open instead).  Note assumes the content is displayed in Grid view below but the view  can be toggled at the top of the screen (List, Grid, Table).
![alt]({{ site.url }}{{ site.baseurl }}/assets/images/configuration/image19.png)
1. On the details screen, click on the link to the navigation layer in the `Layers` section - in the example below the link is called TRIRIGA_Demo_Network.
![alt]({{ site.url }}{{ site.baseurl }}/assets/images/configuration/image20.png)
1. This opens a REST services descriptor which describes technical information about the navigation layer.  Click on the `Route link` in the `Route Layers` section.
![alt]({{ site.url }}{{ site.baseurl }}/assets/images/configuration/image21.png)
1. This opens another REST services descriptor which describes technical information about the route solver part of the navigation service.  `Get the full URL in the browser's URL field`.
![alt]({{ site.url }}{{ site.baseurl }}/assets/images/configuration/image22.png)
1. The URL captured above should be entered into the `Esri Navigation Url` field.