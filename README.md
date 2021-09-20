# Leaflet_MultiPoint-Color-By-Speed

[Example](https://somnuekm.github.io/Leaflet_MultiPoint-Color-By-Speed/multiPointColorBySpeed.html)

![image](https://user-images.githubusercontent.com/58202287/133973903-a3995d23-4bc5-4ebc-ae7d-e60cf7b00eee.png)

![image](https://user-images.githubusercontent.com/58202287/133974079-1fe26a34-c4f4-4bb7-8739-dd670e038192.png)

## Code Example

```html
<script>
function getColor(speed) {
            return speed >= 100 ? '#FF0000' :
                speed >= 90 ? '#FFC000' :
                speed >= 80 ? '#FFFF00' :
                speed >= 70 ? '#80FF00' :
                '#00E000';
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

                    var firstdate = new Date(feature.properties.id);
                    var DateTime = ("0" + firstdate.getDate()).slice(-2) +
                        "/" + ("0" + (firstdate.getMonth() + 1)).slice(-2) +
                        "/" + firstdate.getFullYear() +
                        " " + ("0" + firstdate.getHours()).slice(-2) +
                        ":" + ("0" + firstdate.getMinutes()).slice(-2) + ":" + firstdate.getSeconds();;

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


