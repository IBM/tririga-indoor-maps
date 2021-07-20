---
# Feel free to add content and custom Front Matter to this file.
# To modify the layout, see https://jekyllrb.com/docs/themes/#overriding-theme-defaults

permalink: /installation/
layout: home
title: Installing Overview
description: Overview of the steps involved to enable users to interact with Esri indoor maps in TRIRIGA

sidebar:
  nav: "docs"
---

<<<<<<< Updated upstream
## Install Steps

### Install and configure Esri software

Follow these instructions to [install and configure Esri software]({{ site.url }}{{ site.baseurl }}/install-tririga) to generate and serve indoor maps from CAD data.

### Install and configure TRIRIGA software
=======
## Download Installation Files
Instructions to obtain the installation files will be provided with your email of entitlement to the software.

## Estimated time
The installation may take 1-2 hours to complete.

## Steps
#### A) Installing Object Migration (OM) package and modifying out-of-the-box resources
1. Install the OM package `TRI_Esri_Indoor_Connector_vx.x.x.zip` to your TRIRIGA instance. This will create a new perceptive app named `triLocateMap`.

2. Add new LocateMap app to Workplace Services UI. To use this new app instead of the default Locate app, you need to make the following change on WorkplaceServices webview files. 
**Note**: By completing these steps, you will redirect traffic when you click on the `Locate` link on workplace services, the app displayed will be the new LocateMap app installed with the OM Package capable of integrating with Esri Indoors.  

   1. Open `triview-workplace-services-dev.html` and change.{% raw %}```<tricore-url hidden raw-url="/p/web/locate" bind-url="{{locateMainUrl}}"></tricore-url>``` to ```<tricore-url hidden raw-url="/p/web/locateMap" bind-url="{{locateMainUrl}}"></tricore-url>```{% endraw %}.  
   2. The files now must be vulcanized again. Follow the procedure described [here](https://www.ibm.com/support/knowledgecenter/SSHEB3_3.7/pdfs_wiki/How_to_vulcanize_your_UX_application.pdf) 
   
   Note that, if you like to revert to the original Locate App, just change the `workplace-services-dev.html` file back to the original and vulcanize the files again.   
   
3. Add properties to triBuilding form.
   1. Navigate to the Form Builder and Revise the triBuilding form.
   2. Add a new tab named triEsriMaps with a Tab label of Esri Maps and click Apply.
   3. On the new tab, add a new Section named triEsriMaps with a Tab label of Esri Maps and click Apply.
   4. On this new section, add a new field. Select data field triEsriMapIdTX and click Apply.
   5. Select the new section again, and repeat step for the following fields:
	  - triEsriBuildingIdTX
	  - triEsriPortalUrl
	  - triEsriNetworkUrl
	  - triEsriZoomNU
	  - triEsriRotationNU
   6. After all changes are done, publish the trBuilding form.

4. Add properties to the triFloor form:
   1. On Form Builder, Revise the triFloor form
   1. Add a new tab named triEsriMaps with a Tab label of Esri Maps and click Apply
   1. On the new tab, add a new Section named triEsriMaps with a Tab label of Esri Maps and click Apply
   1. On this new section, add a new field. Select data field triEsriFloorIdTX and click Apply
   1. Publish the triFloor form.

5. TRIRIGA will need to be populated with data for each building and each floor that has indoor maps defined for them within Esri ArcGIS. On the record for buildings and floors there is a new section named `Esri Maps`.

#### B) Enabling buildings

Following is a description of the details that must be filled in the form.

For more information, see [configuration page]({{ site.url }}{{ site.baseurl }}/configuring). 

![alt]({{ site.url }}{{ site.baseurl }}/assets/images/installation/esri-install-1-buildings.png)

**Esri Map ID:** Which web map to load from the ArcGIS server. Obtain this ID from the ArcGIS Portal.

**Esri Building ID:** ID that identifies this building on ArcGIS. Obtain this ID from the ArcGIS Pro.

**Esri Building Default Zoom:** zoom level appropriate for the defined building. This value varies with the footprint of the building, but 20 is commonly sufficient for most buildings.

**Esri Building Default Rotation:** rotation appropriate for the defined building. This value defaults to 0, which corresponds to North at the top of the screen. However depending on the shape of the building you might want to rotate it for convenience. 

**Esri Portal URL:** URL of the ArcGIS Server. `https://{hostname}:{port}/{context_root}/portal`

**Esri Network URL:** the URL of the ArcGIS indoor navigation service for this facility. Obtain this ID from the ArcGIS Portal.

**Note**: If not defined yet, `GIS Latitude` and `GIS Longitude` must be set for the building on the building form found in TRIRIGA, inside the `Primary Address` section.

#### C) Enabling floors

![alt]({{ site.url }}{{ site.baseurl }}/assets/images/installation/esri-install-2-floors.png)

**Esri Floor ID**: ID that identifies this Floor on ArcGIS.

**Note**: This information is defined on your Esri server and can be retrieved from ArcGIS Pro.

An example on how to fill this information is displayed below:

Building:

![alt]({{ site.url }}{{ site.baseurl }}/assets/images/installation/esri-install-3-floor-building-fill-ex.png)

Floor:

![alt]({{ site.url }}{{ site.baseurl }}/assets/images/installation/esri-install-4-floor-id.png)

#### D) Setting up Esri User
Create a task username and password within Esri ArcGIS Portal to be used for authentication by TRIRIGA.

for example:
```
username="tririga-maps"
password="tririga-maps-secret"
```

#### E) Configuring the Proxy

1. After installing the OM package for your TRIRIGA Maps integration, a new file named `proxy.config` will be created that must be populated with settings.

2. To obtain the file from within TRIRIGA's dashboard, click `Tools > System Setup > ClassLoader > EsriIndoorMapsProxy > proxy.config` and click the download button.

An example of configuring this file is displayed below. In this example, the ESRI server (where the esri map is located) is defined as `https://your-mapping-server.ibm.com`. 
**Note**: If your server has an additional context root, it must be included before `/portal` in the example below.

```
<?xml version="1.0" encoding="utf-8" ?>
<ProxyConfig allowedReferers="*"
                logFile="proxy_log.log"
                logLevel="INFO"
                mustMatch="true">
  <serverUrls>
        <serverUrl url="https://your-mapping-server.ibm.com"
            username="$REPLACE_THIS_USERNAME"
            password="$REPLACE_THIS_PASSWORD"
            tokenServiceUri="https://your-mapping-server.ibm.com/portal/sharing/rest/generateToken"
            rateLimit="600"
            rateLimitPeriod="60"
            matchAll="true">
        </serverUrl>
  </serverUrls>
</ProxyConfig>
```

3. You must replace the username and password with Esri Portal user created in step C.

The TRIRIGA server requires a secure connection [HTTPS] to the Esri ArcGIS installation. If a self-signed certificate is used in the ArcGIS installation, or if it is signed by the DigiCert Root Certificate Authority or a less common certificate authority, then you must follow the instructions for WebSphere Liberty or WebSphere Application Server provided below, to allow TRIRIGA to trust the connection.

**WebSphere Liberty**

For each required cert in the chain, perform the following:

```
echo q | openssl s_client -showcerts -connect your-mapping-server.ibm.com:443 > your-mapping-server.ibm.com.cer
keytool -import -alias your-mapping-server -file ./your-mapping-server.ibm.com.cer -keystore key.p12 -storetype PKCS12 
password: $REPLACE_THIS
```

An example start of the `server.xml` file that with HTTPS enabled on Liberty:

```
<server description="IBM TRIRIGA Application Platform">
	<!-- Enable features -->
	<featureManager>
		<feature>jsp-2.2</feature>
		<feature>jaxrs-1.1</feature>
		<feature>localConnector-1.0</feature>
		<feature>servlet-3.0</feature>
		<feature>jndi-1.0</feature>
        <feature>ejbLite-3.1</feature>
        <feature>jdbc-4.0</feature>
	<feature>transportSecurity-1.0</feature>
	</featureManager>
	<keyStore id="defaultKeyStore" password="tririga" />
```

**WebSphere Application Server (WAS)**

To add certs to the `cacerts` in the JRE, see the following [support documentation](https://www.ibm.com/support/pages/adding-digital-keys-and-certificates-received-third-party-jks-keystore-client-two-way-authentication).

To add certs to WAS, refer to [Knowledge Center Document](https://www.ibm.com/support/knowledgecenter/SSSHYH_6.1.0.2/com.ibm.netcoolimpact.doc_6.1.0.2/admin/imag_ewas_ssl.html).

#### F) Adding model to security group
The OM package that is imported, contains a new model for the UX app. Non-admin users must be given proper access to this model. To accomplish this, you must either create a new security group or modify an existing. The following steps modify the `TRIRIGA Request Central - Fundamentals` security group to allow users, that have this group, to read, update, create, and delete the `triLocateMap` model.
1.  From the TRIRIGA Main UI, go to `Tools > Adminstration > Security Manager`.
2.  Click `TRIRIGA Request Central - Fundamentals` security group.
3.  In the window that appears, click `Access`.
4.  Scroll down and expand the `Models` root, and select `triLocateMap`.
5.  In the "Model Access" panel on the right, select `Read,Update,Create and Delete`.
6.  Click Save & Close.
>>>>>>> Stashed changes

Follow these instructions to [install and configure TRIRIGA software]({{ site.url }}{{ site.baseurl }}/install-tririga) to enable TRIRIGA users to use Esri indoor maps.