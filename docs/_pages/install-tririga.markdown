---
# Feel free to add content and custom Front Matter to this file.
# To modify the layout, see https://jekyllrb.com/docs/themes/#overriding-theme-defaults

permalink: /install-tririga/
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

   1. Open `triview-workplace-services-dev.html` and replace the line 
   {% raw %}```<tricore-url hidden raw-url="/p/web/locate" bind-url="{{locateMainUrl}}"></tricore-url>``` to ```<tricore-url hidden raw-url="/p/web/locate" bind-url="{{locateMainUrl}}"></tricore-url>```{% endraw %} 
   with 
   {% raw %}```<tricore-url hidden raw-url="/p/web/locate" bind-url="{{locateMainUrl}}"></tricore-url>``` to ```<tricore-url hidden raw-url="/p/web/locateMap" bind-url="{{locateMainUrl}}"></tricore-url>```{% endraw %} 
   1. The Workplace Services production file will have to be vulcanized again. If you wish to do this now, follow the procedure described [here](https://www.ibm.com/support/knowledgecenter/SSHEB3_3.7/pdfs_wiki/How_to_vulcanize_your_UX_application.pdf).  Vulcanization can be difficult on your first time, so if you don't want to do that just now, you can set the Production Filename to be the same as the Development Filename (i.e. set Production Filename to `triview-workplace-services-dev`) and carry on with the instructions below.
   
1. Add `triEsriMaps` tab to the `triBuilding` form:
   1. Navigate to the Form Builder (Tools > Form Builder).
   1. Click the radio button for the `Location` module.
   1. Click the radio button for the `triBuilding` form.
   1. Click the `Revise` link from the links at the top right.
   1. Click on the `triEsriMapsBuildingTab` link.
   1. Click on `Copy Tab` link from the links at top right.
   1. Select `triBuilding` as the Target Business Object.
   1. Select `triBuilding` as the Target Form.
   1. Click `Apply`.
   1. Go back to the Form Builder and click on the radio button for the `triBuilding` form.
   1. Click the `Publish` link from the links at the top right.

1. Add `triEsriMaps` tab to the `triFloor` form:
   1. Still in the Form Builder with `Location` module selected...
   1. Click the radio button for the `triFloor` form.
   1. Click the `Revise` link from the links at the top right.
   1. Click on the `triEsriMapsFloorTab` link.
   1. Click on `Copy Tab` link from the links at top right.
   1. Select `triFloor` as the Target Business Object.
   1. Select `triFloor` as the Target Form.
   1. Click `Apply`.
   1. Go back to the Form Builder and click on the radio button for the `triFloor` form.
   1. Click the `Publish` link from the links at the top right.

1. In order to link the existing Locate app with the new LocateMap app, you must first add a data source to the existing triLocate model.
   1. Navigate to the Model Designer (Tools > Model Designer).
   1. Search for `triLocate`.
   1. Add a new Data Source with the following values:
      1. Name: `Building Lookup`
      1. Exposed Name: `buildingLookup`
      1. Data Source Type: `Query`
      1. Multiple Records: `TRUE`
      1. Module: `Location`
      1. Business Object: `triBuilding`
      1. Query Name: `triBuilding - UX - LocateMap - Building`
   1. On this data source, add a field:
      1. Name: `Building Record ID`
      1. Exposed Name: `buildingRecordId`
      1. Field Name: `Building Record ID`
   1. Also on this data source, add another field:
      1. Name: `Esri Map ID`
      1. Exposed Name: `esriMapId`
      1. Field Name: `Esri Map ID`

1. Modify existing Locate UX app's location context component to open new LocateMap UX app.
   1. Navigate to the Web View Designer (Tools > Web View Designer).
   1. Click on `triapp-location-context-v3`.
   1. Click on `tricomp-location-context.js`.
   1. Click on the `Download View File` icon.
   1. Edit the `tricomp-location-contextjs` file downloaded.
   1. Search for this line of code `this.fire("select-building", {building: finalBuilding});`.
   1. Add this line of code below it `this.fire("refresh-building", {newBuildingId: newBuilding._id});`.
   1. Click on the `Upload View File` icon and choose the file you just edited.
   1. Click `Save & Close` link from the links at the top right.

1. Modify existing Locate UX app to open new LocateMap UX app.
   1. Navigate to the Web View Designer (Tools > Web View Designer).
   1. Click on `triLocate`.
   1. Click on `trimain-locate.js`.
   1. Click on the `Download View File` icon.
   1. Edit the `trimain-locatejs` file downloaded.
   1. Search for `</style>`.
   1. Add the following lines of code AFTER the `</style>` line:
      ```
      <triplat-ds id="buildingLookup" name="buildingLookup" filtered-data="{{_buildingLookup}}">
         <triplat-query>
            <triplat-query-filter name="buildingRecordId" operator="equals" value="[[overrideBuildingId]]" ignore-if-blank>
            </triplat-query-filter>
         </triplat-query>
      </triplat-ds>
      ```
   1. Search for this line of code `listeners:`.
   1. BEFORE the listeners section, add this line of code:
      ```
      observers: [ "_checkEsriStatus(_buildingLookup)", ],
      ```
   1. INSIDE the listeners section, add this line of code:
      ```
      'refresh-building': '_refreshBuilding',
      ```
      (Note, a comma has been added to the end of the above line, so add in the middle of the listeners.)
   1. AFTER the listeners section, add this block of code:
      ```
      _checkEsriStatus: function(e) { 
         if (this.overrideBuildingId != "" && this._buildingLookup[0] && this._buildingLookup[0].esriMapId) {
            this._isEsriMapAvailable = false;
            var currentUrl = window.location.href;
            var newUrl = currentUrl.substring(0,currentUrl.indexOf("overrideBuildingId=") + 19) + this._buildingLookup[0].buildingRecordId;
            newUrl = newUrl.replace("locate", "locateMap");
            window.location.href = newUrl;
         } else {
            this._isEsriMapAvailable = false;
         }
      },

      _refreshBuilding: function(e) {
         this.overrideBuildingId = e.detail.newBuildingId;
         this._checkEsriStatus(e);
      },
      ```
   1. Click on the `Upload View File` icon and choose the file you just edited.
   1. Click `Save & Close` link from the links at the top right.

1. Bundle up the triLocate app by performing the following steps:  (You'll need NodeJS installed.  See https://nodejs.org for instructions.)
   1. Download and install the @tririga/tri-bundler tool using `npm install @tririga/tri-bundler -g`.
   1. Download and install the tri-pull NodeJS tool using `npm install @tririga/tri-pull -g`.
   1. Download and install the tri-deploy NodeJS tool using `npm install @tririga/tri-deploy -g`.
   1. Pull all the files for triview-locate from your TRIRIGA instance using following command:
      ```
      tri-pull -t URL-for-your-TRIRIGA-instance -u your-userID -p your-password -v triview-locate -d triLocate`
      ```
   1. Bundle the files for triview-locate using the following command:
      ```
      tri-bundler --url URL-for-your-TRIRIGA-instance -u your-userID -p your-password -v triview-locate --component triview-locate-dev.js --output triLocate/triview-locate.js`
      ```
   1. Deploy the bundled file using the following command:
      ```
      tri-deploy -t URL-for-your-TRIRIGA-instance -u your-userID -p your-password -v triview-locate -d triLocate --files triview-locate.js
      ```
   1. If you have difficulties with the above tools, more information about them can be found at https://www.npmjs.com/package/@tririga/tri-pull, https://www.npmjs.com/package/@tririga/tri-bundler, and https://www.npmjs.com/package/@tririga/tri-deploy.  



#### B) Enabling Buildings

TRIRIGA will need to be populated with data for each building and each floor that has indoor maps defined for them within Esri ArcGIS. On the record for buildings and floors there is a new tab named `triEsriMaps`.

See [configuration page]({{ site.url }}{{ site.baseurl }}/configuring) for more details on the following.

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

After installing the OM package for your TRIRIGA Maps integration, a new file named `tokenfetcher.config` will be created and needs to be populated with settings.

The file can be obtained from within TRIRIGA's dashboard by clicking `Tools > System Setup > System > Class Loader > EsriIndoorMapsTokenFetcher > tokenfetcher.config` and clicking the download button.

An example of how this file should be configured is displayed below. In this example, the ESRI server (where the esri map is located) is defined as `https://your-mapping-server.ibm.com/portal`. (please note that that if your server has an additional context root it must be included before `/portal` in the example below)

```
<?xml version="1.0" encoding="utf-8" ?>
<ProxyConfig allowedReferers="*"
                logFile="proxy_log.log"
                logLevel="INFO"
                mustMatch="true">
  <serverUrls>
        <serverUrl url="https://your-mapping-server.ibm.com/portal"
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

You will likely have to add the root and intermediate certs of your Esri server to the TRIRIGA server. This command can be used to get the certificates.

`echo q | openssl s_client -showcerts -connect your-mapping-server.com:443 > your-mapping-server.com.cer`

Use the following steps as a guide on how to add the certificates to the trusted store and restart the TRIRIGA server.

1. Go to "cd c:\tririga\wlp\bin"
1. Find out which JRE/JDK is being used by "type run.bat" and look for the JAVA_HOME variable
1. Go to "cd c:\program files\java<jre/jdk>\jre\lib\security".
1. Add the certificates obtained from the openssl command above to the trusted certificate authorities file (default password is changeit)
`keytool -import -alias esri-certs -file your-mapping-server.com.cer -keystore cacerts`
1. Check that the certificates were successfully installed in the trusted certificate authorities file (default password is changeit) - keytool -list -keystore cacerts
1. Go to "cd c:\tririga\wlp\bin"
1. Stop the server "shutdown.bat"
1. Start the server "run.bat"

**WebSphere Application Server (WAS)**:

To add certs to the `cacerts` in the JRE please see the following [support documentation](https://www.ibm.com/support/pages/adding-digital-keys-and-certificates-received-third-party-jks-keystore-client-two-way-authentication).

To add certs to WAS refer to this [Knowledge Center Document](https://www.ibm.com/support/knowledgecenter/SSSHYH_6.1.0.2/com.ibm.netcoolimpact.doc_6.1.0.2/admin/imag_ewas_ssl.html)

#### F) Adding model to security group
The OM package imported contains a new model for the UX app.  Non-admin users need to be given proper access to this model.  To accomplish this, you can either create a new security group or modify an existing.  The steps below modify the `TRIRIGA Request Central - Fundamentals` security group to allow users, that have this group, to read, update, create and delete the `triLocateMap` model.
1.  From the TRIRIGA Main UI, go to `Tools > Adminstration > Security Manager`.
2.  Click on the `TRIRIGA Request Central - Fundamentals` security group.
3.  In the window appears, click on the `Access` tab.
4.  Scroll down and expand the `Models` root and select `triLocateMap`.
5.  In the "Model Access" panel on the right, select `Read,Update,Create and Delete`.
6.  Click Save & Close.

## Install Verification
* Launch the new enhanced Locate application `https://{hostname}:{port}/{context_root}/p/web/locatemap`
* Select the building that has Esri Indoor Maps configured
* You should see the enhanced UI with the Esri map in the Locate App
