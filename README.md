# Data-Representation-and-Querying-Project-2015

# Recyleing Locations
## Data Representation and Querying Project 2015
### Pauric Boyle

##Introduction

This project is Based on designing an app for [Apps4gaps](http://apps4gaps.ie/) using one of their datasets. 

The app I intend on designing is an app used to locate where your nearest loacation for recyling. The app will start out being used for galway city and will gradually grow until it can cover the whole of ireland. 

There will also be an admin side to the app so that an administrator can update the app and add new locations for the app.



##Dataset
The dataset I am going to use for this app is [Galway City Recycling Bring Bank Locations](https://data.gov.ie/dataset/galway-city-recycling-bring-bank-locations). 

The dataset is only a small dataset for starting out but will gradually increase in size.

####[Galway City Recycling Bring Bank Locations Dataset

Heading | Description  
---------|-----------
"X " |X Cordinates. 
"Y " | Y Cordinates.
"OBJECTID" | An incrementing id to keep track of each record
"RECYCLABLE " | Recycleable types.
"LAT " | Latitude.
"LONG " | longitude.

##Additional Data
I plan on adding in more columns with more data to make the app more in dept. One of the columns i plan on adding is a full column were the data will simple be yes for full and no for still room so that when you're looking at the app it will show you weather or not the closest recyling banks are empty or full. The next column that I'll add will be emptied date which will just take in a date type as its data. This column will be used for indicating when the banks have last been emptied.

##Google Maps Intergration
In my app I plan on integrating the Google maps api. By using Google maps the user will be able to go on the app and once they click on a link the longitude and the latitude will be sent to the javascript funchtiion which will then will open up the location on a map window.

The GET method will be used for recieving the data. The following url will get longitude and the latitude from the data with object number 1. 
URL: http://RecyleingLocations.com/OBJECTID/1.

The json response for this would be.

```json
 {
        "X": "-9.104600012589737",
        "Y": "53.262472165778256",
        "OBJECTID": "1",
        "LOCATION": "Joyces Knocknacarra",
        "RECYCLABLE": "Glass",
        "Lat": "53.263",
        "Long": "-9.105",
        "EastITM": "526265.906",
        "NorthITM": "724165.855",
        "EastIG": "126299.228",
        "NorthIG": "224136.428"
    }
```
This would be the javascript used to locate the Recycling banks at object id1.

```javascript
function initMap() {
  // Create a map object and specify the DOM element for display.
  var map = new google.maps.Map(document.getElementById('map'), {
    center: {lat: -9.105, lng: 53.263},
    scrollwheel: false,
    zoom: 8
  });
}
```

##Updating the data
There will be an admin page for updating the data. A field I plan on adding into the dataset will be Eptied Date. when the admin logs onto the app he can update the app with the date it has been updated. 

To do this we use the PUT method to update the field. To make sure we are updateing the proper data we use the the object id which is quinque to each object in the dataset.

URL: http://RecyleingLocations.com/OBJECTID/10/emptieddate.

The updated json would look like this. 


```json
{
        "X": "-9.014816641260293",
        "Y": "53.275349456250957",
        "OBJECTID": "10",
        "LOCATION": "Renmore, beside Kingfisher Club",
        "RECYCLABLE": "Glass & Textiles",
        "Lat": "53.276",
        "Long": "-9.015",
        "EastITM": "532275.269",
        "NorthITM": "725509.672",
        "EastIG": "132309.883",
        "NorthIG": "225480.569"
        "EMPTIEDDATE": "13/11/15"
    }
  
```

##Closest Recycling plants to your location
To find the closest recycling plants to your location we take the users longitude and latitude and use the POST with the following URL. 

URL: http://RecyleingLocations.com/location/closest.
