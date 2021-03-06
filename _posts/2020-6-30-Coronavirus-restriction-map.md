---
layout: single
title: "Map of postcodes with Stage Three restrictions"
categories: [maps]
tags: 
search: true
excerpt: 
excerpt_separator: <!--more-->
published: true
header:
  og_image: "/images/2020-06/map-og.png"
---
    
<style>
    .mapid { 
      position: relative;
      padding-bottom: 75%; // This is the aspect ratio
      height: 0;
      overflow: hidden;
    }
</style>

#### Update: Restrictions have been extended to the whole of metropolitan Melbourne, plus Mitchell Shire. [Read more](https://www.premier.vic.gov.au/statement-from-the-premier-49/).
    
<link rel="stylesheet" href="https://unpkg.com/leaflet@1.6.0/dist/leaflet.css" integrity="sha512-xwE/Az9zrjBIphAcBb3F6JVqxf46+CDLwfLMHloNu6KEQCAWi6HcDUbeOfBIptF7tcCzusKFjFw2yuvEpDL9wQ==" crossorigin=""/>

<script src="https://unpkg.com/leaflet@1.6.0/dist/leaflet.js" integrity="sha512-gZwIG9x3wUXg2hdXF6+rVkLF/0Vi9U8D2Ntg4Ga5I5BZpVkVxlJWbSQtXPSiUTtC0TjtGOmxa1AJPuV0CPthew==" crossorigin=""></script>
   
<script src="/images/2020-06/user_polygon/VMADMIN/leaflet_ajax.js"></script>
   
<div class="mapid" id ="mapid"></div>

<script>
    function style(feature) {
        if (feature.properties.Stage3 == 'N/A') {
            return {
                fillColor: 'green',
                color: 'green',
                weight: 1,
                opacity: 1,
                fillOpacity: 0.1
                };
            }
        else {
            return {
                fillColor: 'red',
                color: 'red',
                weight: 1,
                opacity: 1,
                fillOpacity: 0.2
                };
            }
    }
//    function zoomToFeature(e) {
//        mymap.fitBounds(e.target.getBounds());
//    }

    function onEachFeature(feature, layer) {
		layer.bindPopup("<p>Postcode: " + feature.properties.POSTCODE + "<br>Stage Three start date: " + feature.properties.Stage3 + "</p>");
//        layer.on({
//            click: zoomToFeature
//        });
    }
    var mymap = L.map('mapid').setView([-37.8174, 144.9564], 11);
    L.tileLayer('https://api.mapbox.com/styles/v1/{id}/tiles/{z}/{x}/{y}?access_token={accessToken}', {
        attribution: 'Map data &copy; <a href="http://openstreetmap.org">OpenStreetMap</a> contributors | Postcodes from <a href="https://discover.data.vic.gov.au/dataset/postcode-boundaries-polygon-vicmap-admin">DELWP</a> under CC BY 4.0 | Imagery © <a href="https://www.mapbox.com/">Mapbox</a>',
        maxZoom: 18,
        id: 'mapbox/dark-v10',
        tileSize: 512,
        zoomOffset: -1,
        accessToken: 'pk.eyJ1IjoiZGl2YWRvIiwiYSI6ImNrYzIyeHgwdjF6eXYzNG54Yjk4Zzh6dWUifQ.p_uNs4ap_9MxrbVGuFWWiA'
    }).addTo(mymap);
    var geojsonLayer = new L.GeoJSON.AJAX("/images/2020-06/user_polygon/VMADMIN/postcode.json" ,{style: style, onEachFeature: onEachFeature});
    geojsonLayer.addTo(mymap);
    // add GeoJSON layer to the map once the file is loaded
//    var datalayer = L.geoJson(geojsonLayer ,{
//    onEachFeature: function(feature, featureLayer) {
//    featureLayer.bindPopup(feature.properties.POSTCODE);
//    }
//    }).addTo(mymap);
//    mymap.fitBounds(datalayer.getBounds());
//    });
</script>

#### Postcode list:

  * 3012: Brooklyn, Kingsville, Maidstone, Tottenham, West Footscray
  * 3021: Albanvale, Kealba, Kings Park, St Albans
  * 3032: Ascot Vale, Highpoint City, Maribyrnong, Travancore
  * 3038: Keilor Downs, Keilor Lodge, Taylors Lakes, Watergardens
  * 3042: Airport West, Keilor Park, Niddrie
  * 3046: Glenroy, Hadfield, Oak Park
  * 3047: Broadmeadows, Dallas, Jacana
  * 3055: Brunswick South, Brunswick West, Moonee Vale, Moreland West
  * 3060: Fawkner
  * 3064: Craigieburn, Donnybrook, Mickleham, Roxburgh Park and Kalkallo
  
*Source: [ABC](https://www.abc.net.au/news/2020-07-01/victorian-premier-warns-all-suburbs-could-lockdown-if-cases-rise/12409000)*
               
Read more: [Press release from the Victorian Premier](https://www.premier.vic.gov.au/statement-from-the-premier-47/)
               
#### Update 04/07/2020:

These postcodes will be under Stage Three restrictions from 11.59pm 4 July 2020:
  * 3031: Kensington, Flemington
  * 3051: North Melbourne
               
Read more: [Press release from the Victorian Premier](https://www.premier.vic.gov.au/statement-from-the-premier-48/)