# geoportail-leaflet

## Description

Exemple minimal d'intégration des couches géoportail dans leafet : [minimal.html](minimal.html).

## Principe

* Générer une URL fonctionnellement équivalente à une URL TMS (ex : `https://{s}.tile.openstreetmap.fr/osmfr/{z}/{x}/{y}.png`) :

```js
/**
 * Renvoie l'URL de la couche geoportail
 */
function getGeoportalURL(layerName) {
    var url = "https://wxs.ign.fr/";
    url += GEOPORTAL_API_KEY;
    url += "/geoportail/wmts?SERVICE=WMTS&VERSION=1.0.0&REQUEST=GetTile";
    url += "&LAYER=" + layerName;
    url += "&STYLE=normal&FORMAT=image/png";
    url += "&TILEMATRIXSET=PM&TILEMATRIX={z}&TILEROW={y}&TILECOL={x}";
    return url;
}
```

* S'appuyer sur cette méthode pour créer des couches leaflet :

```js
var layerPlanIgn = L.tileLayer(
    getGeoportalURL("GEOGRAPHICALGRIDSYSTEMS.PLANIGNV2"),
    {
        attribution: '&copy; <a href="https://www.ign.fr/">IGN</a>',
        maxZoom: 19
    }
);
layerPlanIgn.addTo(map);
```

## Voir aussi

* [IGNF/geoportal-extensions](https://github.com/IGNF/geoportal-extensions#extensions-g%C3%A9oportail)

