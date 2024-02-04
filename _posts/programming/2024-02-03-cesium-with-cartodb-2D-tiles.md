---
name: CesiumJS Viewer / Jekyll Integration
tags: [gis, cesiumjs, o3de, 3D, cloud-native]
image: http://www.geosolutionsgroup.com/wp-content/uploads/2023/06/cesium-certified-dev-logo-sm.png?x31768
description: Seeing if I can Embed the Viewer in a Static Page embedded on GitHub
---

First test for the cesium viewer on a static page! 


<!-- Include the CesiumJS JavaScript and CSS files -->
<script src="https://cesium.com/downloads/cesiumjs/releases/1.87.1/Build/Cesium/Cesium.js"></script>
<link href="https://cesium.com/downloads/cesiumjs/releases/1.87.1/Build/Cesium/Widgets/widgets.css" rel="stylesheet">


<style>
  .app .data .map {
      position: relative;
  }
  html, body, #cesiumContainer, .leaflet-container {
      position: absolute;
      width: 100%;
      height: 100%;
      margin: 0;
      padding: 0;
  }
</style>

<div id="cesiumContainer" style="width: 900px; height:600px; border-radius:1em"></div>
<script>
  // Set the Cesium Ion token to `null` to avoid warnings
  Cesium.Ion.defaultAccessToken = null;

  /* Per Carto's website regarding basemap attribution: https://carto.com/help/working-with-data/attribution/#basemaps */
  let CartoAttribution = 'Map tiles by <a href="https://carto.com">Carto</a>, under CC BY 3.0. Data by <a href="https://www.openstreetmap.org/">OpenStreetMap</a>, under ODbL.'

  // Create ProviderViewModel based on different imagery sources
  // - these can be used without Cesium Ion
  var imageryViewModels = [];

  imageryViewModels.push(new Cesium.ProviderViewModel({
    name: 'OpenStreetMap',
    iconUrl: Cesium.buildModuleUrl('Widgets/Images/ImageryProviders/openStreetMap.png'),
    tooltip: 'OpenStreetMap (OSM) is a collaborative project to create a free editable \
  map of the world.\nhttp://www.openstreetmap.org',
    creationFunction: function() {
      return new Cesium.UrlTemplateImageryProvider({
        url: 'https://{s}.tile.openstreetmap.org/{z}/{x}/{y}.png',
        subdomains: 'abc',
        minimumLevel: 0,
        maximumLevel: 19
      });
    }
  }));
  imageryViewModels.push(new Cesium.ProviderViewModel({
    name: 'Positron',
    tooltip: 'CartoDB Positron basemap',
    iconUrl: 'http://a.basemaps.cartocdn.com/light_all/5/15/12.png',
    creationFunction: function() {
      return new Cesium.UrlTemplateImageryProvider({
        url: 'http://{s}.basemaps.cartocdn.com/light_all/{z}/{x}/{y}.png',
        credit: CartoAttribution,
        minimumLevel: 0,
        maximumLevel: 18
      });
    }
  }));
  imageryViewModels.push(new Cesium.ProviderViewModel({
    name: 'Positron without labels',
    tooltip: 'CartoDB Positron without labels basemap',
    iconUrl: 'http://a.basemaps.cartocdn.com/rastertiles/light_nolabels/5/15/12.png',
    creationFunction: function() {
      return new Cesium.UrlTemplateImageryProvider({
        url: 'https://{s}.basemaps.cartocdn.com/rastertiles/light_nolabels/{z}/{x}/{y}.png',
        credit: CartoAttribution,
        minimumLevel: 0,
        maximumLevel: 18
      });
    }
  }));
  imageryViewModels.push(new Cesium.ProviderViewModel({
    name: 'Dark Matter',
    tooltip: 'CartoDB Dark Matter basemap',
    iconUrl: 'http://a.basemaps.cartocdn.com/rastertiles/dark_all/5/15/12.png',
    creationFunction: function() {
      return new Cesium.UrlTemplateImageryProvider({
        url: 'https://{s}.basemaps.cartocdn.com/rastertiles/dark_all/{z}/{x}/{y}.png',
        credit: CartoAttribution,
        minimumLevel: 0,
        maximumLevel: 18
      });
    }
  }));
  imageryViewModels.push(new Cesium.ProviderViewModel({
    name: 'Dark Matter without labels',
    tooltip: 'CartoDB Dark Matter without labels basemap',
    iconUrl: 'http://a.basemaps.cartocdn.com/rastertiles/dark_nolabels/5/15/12.png',
    creationFunction: function() {
      return new Cesium.UrlTemplateImageryProvider({
        url: 'https://{s}.basemaps.cartocdn.com/rastertiles/dark_nolabels/{z}/{x}/{y}.png',
        credit: CartoAttribution,
        minimumLevel: 0,
        maximumLevel: 18
      });
    }
  }));
  imageryViewModels.push(new Cesium.ProviderViewModel({
    name: 'Voyager',
    tooltip: 'CartoDB Voyager basemap',
    iconUrl: 'http://a.basemaps.cartocdn.com/rastertiles/voyager_labels_under/5/15/12.png',
    creationFunction: function() {
      return new Cesium.UrlTemplateImageryProvider({
        url: 'https://{s}.basemaps.cartocdn.com/rastertiles/voyager_labels_under/{z}/{x}/{y}.png',
        credit: CartoAttribution,
        minimumLevel: 0,
        maximumLevel: 18
      });
    }
  }));
  imageryViewModels.push(new Cesium.ProviderViewModel({
    name: 'Voyager without labels',
    tooltip: 'CartoDB Voyager without labels basemap',
    iconUrl: 'http://a.basemaps.cartocdn.com/rastertiles/voyager_nolabels/5/15/12.png',
    creationFunction: function() {
      return new Cesium.UrlTemplateImageryProvider({
        url: 'https://{s}.basemaps.cartocdn.com/rastertiles/voyager_nolabels/{z}/{x}/{y}.png',
        credit: CartoAttribution,
        minimumLevel: 0,
        maximumLevel: 18
      });
    }
  }));
  imageryViewModels.push(new Cesium.ProviderViewModel({
    name: 'National Map Satellite',
    iconUrl: 'https://basemap.nationalmap.gov/arcgis/rest/services/USGSImageryOnly/MapServer/tile/4/6/4',
    creationFunction: function() {
      return new Cesium.UrlTemplateImageryProvider({
        url: 'https://basemap.nationalmap.gov/arcgis/rest/services/USGSImageryOnly/MapServer/tile/{z}/{y}/{x}',
        credit: 'Tile data from <a href="https://basemap.nationalmap.gov/">USGS</a>',
        minimumLevel: 0,
        maximumLevel: 16
      });
    }
  }));

  // Initialize the viewer - this works without a token!
  viewer = new Cesium.Viewer('cesiumContainer', {
    imageryProviderViewModels: imageryViewModels,
    selectedImageryProviderViewModel: imageryViewModels[1],
    animation: false,
    timeline: false,
    infoBox: false,
    homeButton: false,
    fullscreenButton: false,
    selectionIndicator: false,
  });
  // Remove the Terrain section of the baseLayerPicker
  viewer.baseLayerPicker.viewModel.terrainProviderViewModels.removeAll()

   // Point the camera at the Googleplex
    viewer.scene.camera.setView({
      destination: new Cesium.Cartesian3(
        
        // google's building from example
        //  -2693797.551060477,
        //  -4297135.517094725,
        //  3854700.7470414364

         //-1637851.0756622232, 
         //-3640187.5318698585, 
         // 4962000.809236132

          -1639351.1093918397, 
          -3666172.594959622, 
           4938700.0

        ),
        orientation: new Cesium.HeadingPitchRoll(
          -3.455010,
          -0.2863894863138836,
          1.3561760425773173e-7
        ),
    }); 

    viewer.canvas.addEventListener('click',
      function(e){
        var mousePosition = new Cesium.Cartesian2(e.clientX, e.clientY);
        var ellipsoid = viewer.scene.globe.ellipsoid;
        var cartesian = viewer.camera.pickEllipsoid(mousePosition, ellipsoid);

        if (cartesian) {
          var cartographic = ellipsoid.cartesianToCartographic(cartesian);
          
          var longitudeString = Cesium.Math.toDegrees(cartographic.longitude).toFixed(2);
          var latitudeString = Cesium.Math.toDegrees(cartographic.latitude).toFixed(2);
          var heightString = Cesium.Math.toDegrees(cartographic.height).toFixed(2);

          console.log('longitude: ' + longitudeString + ', latitude: ' + latitudeString + ', height:' + heightString);

          console.log('cartesian', cartesian);
        } else {
          console.log('Globe was not picked');
        }

      }, false);

</script>
</div>
