---
# Feel free to add content and custom Front Matter to this file.
# To modify the layout, see https://jekyllrb.com/docs/themes/#overriding-theme-defaults

permalink: /installation/
layout: home
title: Installing TRIRIGA Indoor Maps
description: Steps for downloading, installing and configuring IBM TRIRIGA Indoor Maps for your IBM TRIRIGA solution.

sidebar:
  nav: "docs"
---

## Download Installation Files
Instructions to obtain the installation files will be provided with your email of entitlement to the software.

## Estimated time
This installation should take 1-2 hours to complete.

## Install Steps
#### A) Install Object Migration Package and modify out-of-the-box resources 
1. Install the OM package `TRI_Esri_Indoor_Connector_vx.x.x.zip` to your TRIRIGA instance. This will create a new perceptive app named `triLocateMap`.

1. Add new LocateMap app to Workplace Services UI:
   To use this new app instead of the default Locate app, you need to make the following change on WorkplaceServices webview files. Note that by completing these steps, you will redirect traffic when you click on the `Locate` link on workplace services, the app displayed will be the new LocateMap app installed with the OM Package capable of integrating with Esri Indoors.  

   1. Open `triview-workplace-services-dev.html` and change. ```<tricore-url hidden raw-url="/p/web/locate" bind-url="{{locateMainUrl}}"></tricore-url>``` to ```<tricore-url hidden raw-url="/p/web/locateMap" bind-url="{{locateMainUrl}}"></tricore-url>```  
   1. The files now must be vulcanized again. Follow the procedure described [here](https://www.ibm.com/support/knowledgecenter/SSHEB3_3.7/pdfs_wiki/How_to_vulcanize_your_UX_application.pdf)
   
   Note that if you like to revert to the original Locate App, just change the `workplace-services-dev.html` file back to the original and vulcanize the files again.   
   
1. Add properties to triBuilding form:
   1. Navigate to the Form Builder and Revise the triBuilding Form
   1. Add a new tab named triEsriMaps with a Tab Label of Esri Maps and click Apply
   1. On the new tab, add a new Section named triEsriMaps with a Tab Label of Esri Maps and click Apply
   1. On this new section, add a new field. Select data field triEsriMapIdTX and click Apply
   1. Select the new section again, and repeat step for the following fields:
	  - triEsriBuildingIdTX
	  - triEsriPortalUrl
	  - triEsriNetworkUrl
	  - triEsriZoomNU
	  - triEsriRotationNU
   1. After all changes are done, Publish the trBuilding Form.

1. Add properties to the triFloor form:
   1. On Form Builder, Revise the triFloor Form
   1. Add a new tab named triEsriMaps with a Tab Label of Esri Maps and click Apply
   1. On the new tab, add a new Section named triEsriMaps with a Tab Label of Esri Maps and click Apply
   1. On this new section, add a new field. Select data field triEsriFloorIdTX and click Apply
   1. Publish the triFloor Form.

1. TRIRIGA will need to be populated with data for each building and each floor that has indoor maps defined for them within Esri ArcGIS. On the record for buildings and floors there is a new section named `Esri Maps`.

#### B) Enabling Buildings

![alt]({{ site.url }}{{ site.baseurl }}/assets/images/installation/esri-install-1-buildings.png)

**Esri Map ID:** Which web map to load from the ArcGIS server. Obtain this ID from the ArcGIS Portal.

**Esri Building ID:** ID that identifies this building on ArcGIS. Obtain this ID from the ArcGIS Pro.

**Esri Building Default Zoom:** zoom level appropriate for the defined building. This value varies with the footprint of the building, but 20 is commonly sufficient for most buildings.

**Esri Building Default Rotation:** rotation appropriate for the defined building. This value defaults to 0, which corresponds to North at the top of the screen. However depending on the shape of the building you might want to rotate it for convenience. 

**Esri Portal URL:** URL of the ArcGIS Server. `https://{hostname}:{port}/{context_root}/portal`

**Esri Network URL:** the URL of the ArcGIS indoor navigation service for this facility. Obtain this ID from the ArcGIS Portal.

**Note**: If not defined yet, `GIS Latitude` and `GIS Longitude` will need to be set for the building on the building form found in TRIRIGA inside the `Primary Address` section.

#### C) Enabling Floors

![alt]({{ site.url }}{{ site.baseurl }}/assets/images/installation/esri-install-2-floors.png)

**Esri Floor ID:** ID that identifies this Floor on ArcGIS

This information is defined on your Esri server and can be retrieved from ArcGIS Pro.

An example on how to fill this info is displayed below

Building:

![alt]({{ site.url }}{{ site.baseurl }}/assets/images/installation/esri-install-3-floor-building-fill-ex.png)

Floor:

![alt]({{ site.url }}{{ site.baseurl }}/assets/images/installation/esri-install-4-floor-id.png)

#### D) Esri User Setup
Create a task username and password within Esri ArcGIS Portal to be used for authentication by TRIRIGA

for example:
```
username="tririga-maps"
password="tririga-maps-secret"
```

#### E) Configuring the Proxy

After installing the OM package for your TRIRIGA Maps integration, a new file named `proxy.config` will be created and needs to be populated with settings.

The file can be obtained from within TRIRIGA's dashboard by clicking `Tools > System Setup > ClassLoader > EsriIndoorMapsProxy > proxy.config` and clicking the download button.

An example of how this file should be configured is displayed below. In this example, the ESRI server (where the esri map is located) is defined as `https://your-mapping-server.ibm.com`. (please note that that if your server has an additional context root it must be included before `/portal` in the example below)

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

The username and password must be replaced with Esri Portal user created in step C.

The TRIRIGA server requires a secure connection [HTTPS] to the Esri ArcGIS installation. If a self-signed certificate has been used in the ArcGIS installation, or if it has been signed by the DigiCert Root Certificate Authority or a less common certificate authority then you will need to follow the instructions for WebSphere Liberty or WebSphere Application Server below to allow TRIRIGA to trust the connection:

**WebSphere Liberty**:

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

**WebSphere Application Server (WAS)**:

To add certs to the `cacerts` in the JRE please see the following [support documentation](https://www.ibm.com/support/pages/adding-digital-keys-and-certificates-received-third-party-jks-keystore-client-two-way-authentication).

To add certs to WAS refer to this [Knowledge Center Document](https://www.ibm.com/support/knowledgecenter/SSSHYH_6.1.0.2/com.ibm.netcoolimpact.doc_6.1.0.2/admin/imag_ewas_ssl.html)

## Install Verification
* Launch the new enhanced Locate application `https://{hostname}:{port}/{context_root}/p/web/locatemap`
* Select the building that has Esri Indoor Maps configured
* You should see the enhanced UI with the Esri map in the Locate App
