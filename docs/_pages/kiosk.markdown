---
# Feel free to add content and custom Front Matter to this file.
# To modify the layout, see https://jekyllrb.com/docs/themes/#overriding-theme-defaults

permalink: /kiosk/
layout: home
title: Configuring TRIRIGA Indoor Maps for kiosks
description: How to configure TRIRIGA Indoor Maps to be used via a kiosk.

sidebar:
  nav: "docs"
---

## Configuring TRIRIGA Indoor Maps for kiosks

#### A) Adding fields to the triEmployee form

Add `triEsriMaps` tab to the `triPeople` form:
   1. Go to Tools > Form Builder.
   1. Click the radio button for the `triPeople` module and the `triEmployee` form.
   1. Click the `Revise` link from the links at the top right.
   1. Click on the `triEsriMapsPeopleTab` link.
   1. Click `Copy Tab` link from the links at top right.
   1. Select `triPeople` as the Target Business Object and `triEmployee` as the Target form. Click `Apply`.
   1. Go back to the Form Builder and click on the radio button for the `triEmployee` form.
   1. Click the `Publish` link from the links at the top right.


#### B) Creating a TRIRIGA user account for a kiosk

Each kiosk needs to have a separate user account set up in TRIRIGA.  Create an employee account and complete the following fields in the `triEsriMaps` tab.

Field | Comment 
------- | ---------
Is this a Kiosk User? | Check to indicate the user account will have data for a kiosk to use during loading the Indoor Maps Locate app.
Allow People Search? | Check to indicate the users of the kiosk must be able to search for people.
Floor Kiosk is on | The level number representing the floor where the kiosk is located.
X Coordinate of Kiosk | The X coordinate where the "You are here" dot must be placed to indicate the location of the kiosk.
Y Coordinate of Kiosk | The Y coordinate where the "You are here" dot must be placed to indicate the location of the kiosk.

#### C) Setting up the kiosk for public use

To set up a kiosk with the Indoor Maps Locate app, either manually or scripted:
1. Log in to TRIRIGA using the username and password created specifically for the kiosk.
1. Navigate to the Locate app and select the building where the kiosk is located.