# How to display Texas House District 134 using Mapbox on your webpage

* Sign-up for a free Mapbox account [here](https://www.mapbox.com/signup/?plan=starter).
This will give you an access token to generate maps using Mapbox. You can find your access token from [here](https://www.mapbox.com/studio/account/tokens/).

* Include the CSS and Javascript libraries into the page that will display the map: 
```
<link rel="stylesheet" href="https://unpkg.com/leaflet@1.0.3/dist/leaflet.css" />
<script src="https://unpkg.com/leaflet@1.0.3/dist/leaflet.js"></script>
<script src='https://api.mapbox.com/mapbox.js/plugins/leaflet-fullscreen/v1.0.1/Leaflet.fullscreen.min.js'></script>
<link href='https://api.mapbox.com/mapbox.js/plugins/leaflet-fullscreen/v1.0.1/leaflet.fullscreen.css' rel='stylesheet' />
```
* Upload the TX-134 map file `tx134.js` to your server and include it's location:
```
<script src="/js/tx134.js"></script>
```
* Put a div element with a certain id where you want your map to be displayed:

```
<div id="mapid" style="height: 600px;"></div>
```
You can adjust the height of the map to your liking with `style="height: 600px;`

* Now add the javascript that creates the map:
```javascript
<script type="text/javascript">
var geojson;

var map = L.map('mapid').setView([29.74, -95.435],12);
L.tileLayer('https://api.tiles.mapbox.com/v4/{id}/{z}/{x}/{y}.png?access_token={accessToken}', {
    attribution: 'Map data &copy; <a href="http://openstreetmap.org">OpenStreetMap</a> contributors, <a href="http://creativecommons.org/licenses/by-sa/2.0/">CC-BY-SA</a>, Imagery © <a href="http://mapbox.com">Mapbox</a>',
    maxZoom: 18,
    id: 'mapbox.streets',
    accessToken: 'your_access_token'
}).addTo(map);

L.control.fullscreen().addTo(map);

function style(feature) {
  return {
    fillColor: '#4292c6',
    fillOpacity: 0.7,
    opacity: 0.7,
    color: '#4292c6',
    weight: 3
  };
}

geojson = L.geoJSON( tx134Data, {style: style} ).addTo(map);
</script>
```
* Copy that really long string of digits and numbers, [your access token](https://www.mapbox.com/studio/account/tokens/), into the accessToken setting: 

```javascript
    accessToken: 'copy your access token here'
```
You can change the settings of the map using the style function:
```javascript
    fillColor: '#4292c6',
    fillOpacity: 0.7,
    opacity: 0.7,
    color: '#4292c6',
    weight: 3
```

Find the style options available [here](http://leafletjs.com/reference-1.0.3.html#path)
