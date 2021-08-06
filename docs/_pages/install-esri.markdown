---
# Feel free to add content and custom Front Matter to this file.
# To modify the layout, see https://jekyllrb.com/docs/themes/#overriding-theme-defaults

permalink: /install-esri/
layout: home
title: Setting up Esri
description: Steps for downloading, installing, and configuring Esri software to generated maps for TRIRIGA.

sidebar:
  nav: "docs"
---

## Overview

**Esri ArcGIS Indoors** is required to enable TRIRIGA Indoor Maps. It consists of **ArcGIS Pro**, which is the tool for generating and preparing your GIS maps; and **ArcGIS Enterprise**, which is the server that hosts the maps and wayfinding capabilities. You will need to obtain valid licenses for these Esri components and follow the Esri documentation to complete the installation. It is highly recommended to contact a qualified service provider to assist you with this process. Below is a summary of this process along with links, followed by the necessary configurations to enable TRIRIGA Indoor maps. 

### Steps

1. Gather your floorplans and review the [ArcGIS Indoors Information Model](https://pro.arcgis.com/en/pro-app/2.7/help/data/indoors/arcgis-indoors-information-model.htm) requirements to ensure that your data is in good condition.
1. Read the overview information of [ArcGIS Pro](https://www.esri.com/en-us/arcgis/products/arcgis-pro/overview) and [ArcGIS Enterprise](https://www.esri.com/en-us/arcgis/products/arcgis-enterprise/overview) to familiarize yourself with their capabilities.
1. Depending on your entitlement you may obtain the Esri software and license from IBM Passport Advantage, or directly from your myEsri portal
 See the IBM Passport Advantage parts list [here]({{ site.url }}{{ site.baseurl }}/assets/attachments/TRIRIGA%20Indoor%20Maps%20v11%20Parts%20List.pdf).
1. To enable TRIRIGA Indoor Maps you will require the following components. 
    - ArcGIS Enterprise ([quick start guide](https://links.esri.com/ArcGISPro/2.7/quick_start_guide))
    - ArcGIS Pro ([quick start guide](https://links.esri.com/ArcGISPro/2.7/quick_start_guide))
    - License Manager (comes with ArcGIS Enterprise)
    - TRIRIGA Connector for Esri ArcGIS Indoors ([quick start guide]({{ site.url }}{{ site.baseurl }}/install-tririga))
1. Once the installation is complete you may use Esri Tools to:
   * [Load](https://pro.arcgis.com/en/pro-app/2.7/help/data/indoors/data-creation-workflow.htm) CAD or BIM data into ArcGIS Pro to generate your GIS maps
   * [Create](https://pro.arcgis.com/en/pro-app/2.7/help/data/indoors/create-the-indoors-network.htm)  the Indoors routing network
   * [Generate](https://pro.arcgis.com/en/pro-app/2.7/help/data/indoors/load-points-of-interest.htm) points of interest on the maps
   * [Publish](https://doc.arcgis.com/en/indoors/viewer/share-a-web-map-or-scene-for-indoor-viewer.htm) maps to the Indoor Viewer on ArcGIS Enterprise
   
1. Finally you will want to [Install]({{ site.url }}{{ site.baseurl }}/install-tririga) TRIRIGA connector for Esri ArcGIS and configure it to authenticate into the ArcGIS server.


### References to Esri documentation

#### Overview
- [ArcGIS Indoors](https://www.esri.com/en-us/arcgis/products/arcgis-indoors/overview) 
- [ArcGIS Pro](https://www.esri.com/en-us/arcgis/products/arcgis-pro/overview)
- [ArcGIS Enterprise](https://www.esri.com/en-us/arcgis/products/arcgis-enterprise/overview)
 
#### Installation
- ArcGIS Enterprise Installation and Deployment
  <https://enterprise.arcgis.com/en/documentation/install/>
- ArcGIS Enterprise QuickStart Guide
  <https://www.esri.com/content/dam/esrisites/en-us/media/pdf/guides/quickstart-arcgis-enterprise.pdf>
- ArcGIS Enterprise Configure for ArcGIS Indoors
  <https://doc.arcgis.com/en/indoors/viewer/configure-your-indoors-portal.htm>
- How to Download and Install ArcGIS from myEsri
  <https://support.esri.com/en/technical-article/000018698>
- ArcGIS Pro Download, Install, and Authorize
  <https://pro.arcgis.com/en/pro-app/get-started/install-and-sign-in-to-arcgis-pro.htm>
  (use for SaaS deployment)
- ArcGIS Pro Install a Single User License
  <https://pro.arcgis.com/en/pro-app/get-started/authorize-and-start-arcgis-pro-with-a-single-use-license.htm>

#### Information Model 
 -  How to load data into ArcGIS Indoors <https://pro.arcgis.com/en/pro-app/2.7/help/data/indoors/arcgis-indoors-information-model.htm>
- Import untility from TRIRIGA to ArcGIS <https://hub.safe.com/publishers/safe-lab/templates/tririga-to-arcgis-indoors>

#### Routing
- Create the Indoors network <https://pro.arcgis.com/en/pro-app/2.7/help/data/indoors/create-the-indoors-network.htm>

#### Adding Points of Interest
- Add  points of interest to your indoor maps <https://pro.arcgis.com/en/pro-app/2.7/help/data/indoors/load-points-of-interest.htm>

#### Publishing
- Publish your indoor maps for web viewing and for use by IBM TRIRIGA <https://doc.arcgis.com/en/indoors/viewer/share-a-web-map-or-scene-for-indoor-viewer.htm>