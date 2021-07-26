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

The steps to set up Esri software to generate maps for TRIRIGA is an involved process that is documented by Esri documentation.  This document is a summary of the process required to create maps for TRIRIGA to use.

### Steps

1. Evaluate the CAD data that the customer has and determine if it is ready for import or requires more work ( same criteria as importing CAD data into TRIRIGA).
1. Install Esri ArcGIS Indoors components that come with the Esri OEM on premise - must work with customer's IT department.
1. Use Esri Tools to:
   * Load CAD data or import directly from TRIRIGA using ETL tool
   * Run automation to convert CAD data to GIS maps
   * Generate routing paths and validate them
   * Generate points of interest on the maps requires input from customer
   * Publish maps to the ArcGIS server and validate
1. Install TRIRIGA connector for Esri ArcGIS and configure it to authenticate into the ArcGIS server.


### Links to Esri documentation

#### Overviews
- ArcGIS Indoors
  <https://www.esri.com/en-us/arcgis/products/arcgis-indoors/overview>
- ArcGIS Pro
  <https://www.esri.com/en-us/arcgis/products/arcgis-pro/overview>
- ArcGIS Enterprise
  <https://www.esri.com/en-us/arcgis/products/arcgis-enterprise/overview>
- ArcGIS Online
  <https://www.esri.com/en-us/arcgis/products/arcgis-online/overview>
 
#### Installation
- ArcGIS Enterprise Installation and Deployment
  <https://enterprise.arcgis.com/en/documentation/install/>
- ArcGIS Enterprise QuickStart Guide
  <https://www.esri.com/content/dam/esrisites/en-us/media/pdf/guides/quickstart-arcgis-enterprise.pdf>
- ArcGIS Enterprise Configure for ArcGIS Indoors
  <https://doc.arcgis.com/en/indoors/viewer/configure-your-indoors-portal.htm>
- ArcGIS Online Configure for ArcGIS Indoors
  <https://doc.arcgis.com/en/indoors/viewer/configure-your-organization-for-indoors.htm>
- How to Download and Install ArcGIS from myEsri
  <https://support.esri.com/en/technical-article/000018698>
- ArcGIS Pro Download, Install, and Authorize
  <https://pro.arcgis.com/en/pro-app/get-started/install-and-sign-in-to-arcgis-pro.htm>
  (use for SaaS deployment)
- ArcGIS Pro Install a Single User License
  <https://pro.arcgis.com/en/pro-app/get-started/authorize-and-start-arcgis-pro-with-a-single-use-license.htm>