---
# Feel free to add content and custom Front Matter to this file.
# To modify the layout, see https://jekyllrb.com/docs/themes/#overriding-theme-defaults

permalink: /troubleshooting/
layout: home
title: Troubleshooting
description: Get help diagnosing issues and details on how to fix more frequently encountered issues with TRIRIGA Indoor Maps.

sidebar:
  nav: "docs"
---

## Debugging Esri Server Connection Problems

1. Test that you can ping Esri server from TRIRIGA server.
Log into your VM or computer running TRIRIGA, and use the curl command to determine if the Esri server is reachable.

2. Test that the proxy can access your Esri server.
Using your web browser, browse to `https://YOUR-TRIRIGA-SERVER/html/en/default/rest/EsriIndoorMapsProxy?https://YOUR-ESRI-SERVER/portal/sharing/rest/portals/self?f=json&culture=en-us`.  This is successful if a JSON blob is returned that doesn't look like an error.

3. Turn on logging by using `com.tririga.custom.EsriIndoorMapsProxy` as the class name through the TRIRIGA Admin UI.

## Common Problems

1. For certificate chaining errors seen in the logging output, you must add the certificates for the Esri server to the key stores.
The certificates can be exported using a web browser. They can be added to the cacerts file (in jre/lib/security directory) using commands as, example:
`mv cacerts cacerts.orig`
`export PATH=$PATH:/opt/IBM/WebSphere/AppServer/java/8.0/jre/bin`
`keytool -import -trustcacerts -alias WHATEVER-YOU-WANT -file SOME-EXPORTED-CERT.cer -keystore cacerts`
If using Websphere Application Server, you must add the certificate in the CellDefaultTrustStore (SSL certificate and key management > Key stores and certificates > CellDefaultTrustStore > Signer certificates).

2. If you get "Failed to load portal item" message while using the Locate app, check the building information in TRIRIGA, specifically the `Esri Map ID` at the bottom of the form.  Check the Esri server for the ID for your building.

3. If you get "Unable to load..." message while using the Locate app, check that the URL in `Esri Portal URL` on the building is correct.

4. If you get "Failed to fetch" message while using the Locate app, check that the URL in `Esri Network URL` on the building is correct.

5. If you get "User does not have permissions to access..." message while using the Locate app, check that the path in `Esri Network URL` on the building is correct.

6. If the floorplan doesn't appear on the screen, check that the `Esri Building ID` on the building and `Esri Floor ID` on the floor are correct.

7. If the map appears and is focused somewhere other than where the building is located, check that the `GIS Latitude` and `GIS Longitude` are correct.

8. If the building rotation or zoom isn't ideal, then change the Zoom and Rotation properties on the building.  A zoom level of around 20 is typically good.

9. If you find issues while selecting a room (real name doesn't appear, room description isn't correct, etc.), then check the ID of the space. The ID property is used to look up the space in Esri.

## Overview of Esri Components

* [ArcGIS Indoors](https://www.esri.com/en-us/arcgis/products/arcgis-indoors/overview "ArcGIS Indoors Overview")

* [ArcGIS Pro](https://www.esri.com/en-us/arcgis/products/arcgis-pro/overview)

* [ArcGIS Enterprise](https://www.esri.com/en-us/arcgis/products/arcgis-enterprise/overview)

* [ArcGIS Online](https://www.esri.com/en-us/arcgis/products/arcgis-online/overview)

 

 

## Installation of Esri components

* [ArcGIS Enterprise Installation and Deployment](https://enterprise.arcgis.com/en/documentation/install/)

* [ArcGIS Enterprise QuickStart Guide](https://www.esri.com/content/dam/esrisites/en-us/media/pdf/guides/quickstart-arcgis-enterprise.pdf)

* [ArcGIS Enterprise Configure for ArcGIS Indoors](https://doc.arcgis.com/en/indoors/viewer/configure-your-indoors-portal.htm)

* [ArcGIS Online  Configure for ArcGIS Indoors](https://doc.arcgis.com/en/indoors/viewer/configure-your-organization-for-indoors.htm)
