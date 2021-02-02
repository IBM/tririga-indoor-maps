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

1. Open a web browser
1. Navigate to your Esri installations Portal e.g. https://host.domain/portal
1. Click the Sign In on the top right of the landing page
![alt]({{ site.url }}{{ site.baseurl }}/assets/images/configuration/image1.png)
1. Log in as admin or any user that is able to see the organisation's content
![alt]({{ site.url }}{{ site.baseurl }}/assets/images/configuration/image2.png)
1. Select Content from the navigation bar at the top of the page
![alt]({{ site.url }}{{ site.baseurl }}/assets/images/configuration/image3.png)
1. Select My Organisation on the navigation sub-bar
![alt]({{ site.url }}{{ site.baseurl }}/assets/images/configuration/image4.png)
1. Filter the content by clicking Maps -> Web Maps on the left hand side
![alt]({{ site.url }}{{ site.baseurl }}/assets/images/configuration/image5.png)
1. Select the Web Map that you wish to configure in TRIRIGA - click on the title under the thumbnail (do not click the thumbnail itself or the map viewer will open instead).  Note assumes the content is displayed in Grid view below but the view  can be toggled at the top of the screen (List, Grid, Table).
![alt]({{ site.url }}{{ site.baseurl }}/assets/images/configuration/image6.png)
1. Look in the URL field of the web browser and note the id parameter value - this is the value that should be entered into the Esri Map ID in TRIRIGA.  In the example below it is 9a8068284e614be3bdcb1cd26f05499a
![alt]({{ site.url }}{{ site.baseurl }}/assets/images/configuration/image7.png)