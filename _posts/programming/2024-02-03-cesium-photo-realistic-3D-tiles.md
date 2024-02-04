---
name: CesiumJS Viewer / Jekyll Integration
tags: [gis, cesiumjs, o3de, 3D, cloud-native]
image: http://www.geosolutionsgroup.com/wp-content/uploads/2023/06/cesium-certified-dev-logo-sm.png?x31768
description: Seeing if I can Embed the Viewer in a Static Page embedded on GitHub
---

Nothing fancy here, just re-creating the cesium sandbox example on my github page to see if I could do it. Very cool that it is working.

See this link for details: https://developers.google.com/maps/documentation/tile/3d-tiles


<!-- Include the CesiumJS JavaScript and CSS files 
      @ https://developers.google.com/maps/documentation/tile/3d-tiles
-->
<script src="https://ajax.googleapis.com/ajax/libs/cesiumjs/1.105/Build/Cesium/Cesium.js"></script>
<link href="https://ajax.googleapis.com/ajax/libs/cesiumjs/1.105/Build/Cesium/Widgets/widgets.css" rel="stylesheet">

<div id="cesiumContainer"></div>
<script>

    window.onunhandledrejection = event => {
      console.warn(`UNHANDLED PROMISE REJECTION: ${event.reason}`);
    };

    window.onerror = function(message, source, lineNumber, colno, error) {
      console.warn(`UNHANDLED ERROR: ${error.stack}`);
    };

    const viewer = new Cesium.Viewer('cesiumContainer', {
      imageryProvider: false,
      baseLayerPicker: false,
      requestRenderMode: true,
    });

    const tileset = viewer.scene.primitives.add(new Cesium.Cesium3DTileset({
      url: "https://tile.googleapis.com/v1/3dtiles/root.json?key=AIzaSyA26OxLFQuImt9-8Vpm7gK400FmhqiNubA",
      showCreditsOnScreen: true,
    }));

    viewer.scene.globe.show = false;


    // Point the camera at the Googleplex
    viewer.scene.camera.setView({
      destination: new Cesium.Cartesian3(
        -2693797.551060477,
        -4297135.517094725,
        3854700.7470414364
      ),
      orientation: new Cesium.HeadingPitchRoll(
        4.6550106925119925,
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


