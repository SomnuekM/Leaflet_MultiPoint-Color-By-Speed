# Leaflet MultiPoint Color By Speed

[Example 1](https://somnuekm.github.io/Leaflet_MultiPoint-Color-By-Speed/multiPointColorBySpeed.html)
![image](https://user-images.githubusercontent.com/58202287/133973903-a3995d23-4bc5-4ebc-ae7d-e60cf7b00eee.png)
![image](https://user-images.githubusercontent.com/58202287/133974079-1fe26a34-c4f4-4bb7-8739-dd670e038192.png)

[Example 2](https://somnuekm.github.io/Leaflet_MultiPoint-Color-By-Speed/MultiPointColorBySpeedInput.html)
![image](https://user-images.githubusercontent.com/58202287/134484140-c76500e4-1d1f-4e07-ba4d-adaedf89106c.png)

[Example 3](https://somnuekm.github.io/Leaflet_MultiPoint-Color-By-Speed/MultiPointColorBySpeed_CalculateSpeed.html)
![image](https://user-images.githubusercontent.com/58202287/135198974-19194360-358e-4b06-bbfe-f0af0bc18f5c.png)

[Highcharts StockChart](https://somnuekm.github.io/Leaflet_MultiPoint-Color-By-Speed/speedChart.html)
![image](https://user-images.githubusercontent.com/58202287/134884807-e7350f4e-b1c5-45f3-8ecc-0260c5dcec5a.png)


## Code Example

```html
<script>
function getColor(speed) {
             return speed > 100 ? '#FF0000' :
                        speed > 90 ? '#FFC000' :
                        speed > 80 ? '#FFFF00' :
                        speed > 70 ? '#80FF00' :
                        speed > 0 ? '#00E000' :
                        '#669999';
 };

let urlJson = 'https://raw.githubusercontent.com/SomnuekM/Leaflet_MultiPoint-Color-By-Speed/main/dataJson/demo.json';
 $.getJSON(urlJson, function(data) {

            point = L.geoJson(data, {
                pointToLayer: function(feature, latlng) {
                    return L.circleMarker(latlng, {
                        radius: 5.5,
                        opacity: .5,
                        color: getColor(feature.properties.speed),
                        fillColor: getColor(feature.properties.speed),
                        fillOpacity: 0.8
                    })
                },
                onEachFeature: function(feature, layer) {
                    layer._leaflet_id = feature.properties.id;

                    var d = new Date(feature.properties.id);
                    var DateTime = ("0" + d.getDate()).slice(-2) +
                        "/" + ("0" + (d.getMonth() + 1)).slice(-2) +
                        "/" + d.getFullYear() +
                        " " + ("0" + d.getHours()).slice(-2) +
                        ":" + ("0" + d.getMinutes()).slice(-2) + 
                        ":" + ("0" + d.getSeconds()).slice(-2);

                    var popupContent = "<p><b>" + DateTime + "</b> </br>" +
                        "<b>speed : </b>" + feature.properties.speed + "</br>";
                    if (feature.properties && feature.properties.popupContent) {
                        popupContent += feature.properties.popupContent;
                    }
                    layer.bindPopup(popupContent);

                }
            });

            // zoom the map to the polyline
            map.fitBounds(point.getBounds());
            //Add selected points back into map as green circles.
            map.addLayer(point);

  })
</script>
```

## JSON Data Example 
```json
[
  {
    "type": "Feature",
    "properties": {
      "id": 1631487601000,
      "speed": 53
    },
    "geometry": {
      "type": "Point",
      "coordinates": [
        100.50063,
        13.86313
      ]
    }
  },
  {
    "type": "Feature",
    "properties": {
      "id": 1631487603000,
      "speed": 56
    },
    "geometry": {
      "type": "Point",
      "coordinates": [
        100.500895,
        13.8630333
      ]
    }
  },
  {
    "type": "Feature",
    "properties": {
      "id": 1631487605000,
      "speed": 57
    },
    "geometry": {
      "type": "Point",
      "coordinates": [
        100.50117,
        13.8629333
      ]
    }
  },
  {
    "type": "Feature",
    "properties": {
      "id": 1631487608000,
      "speed": 58
    },
    "geometry": {
      "type": "Point",
      "coordinates": [
        100.5014516,
        13.8628333
      ]
    }
  }
 ]
```

