---
name: CesiumJS Viewer / Jekyll Integration
tags: [gis, cesiumjs, o3de, 3D, cloud-native]
image: http://www.geosolutionsgroup.com/wp-content/uploads/2023/06/cesium-certified-dev-logo-sm.png?x31768
description: Seeing if I can Embed the Viewer in a Static Page embedded on GitHub
---

## This is disabled (but the code can work)!
Though the code works, I've disabled it by not including the API key: you need a serverless environment that can do more than host static-pages like github otherwise you can't secure your secret keys.  

## Purpose: 

Create an experiment to integrate CesiumJS Viewer using Google 3D tiles into a serverless environment via Jeykyll on github, and point the viewer via 3D coordinates / heading to Calgary, Canada.

It was an interesting experiment because generally, when you push things into a public repository you cannot hide important aspects like `secrets` such as the API key for an endpoint. Instead I had to dig into the documentation a bit and figure out how to do it only to discover you need a serverless environment with more security than Github pages. 

## Related links

See these links for details: 
- Consuming Google 3D photorealistic tiles: https://developers.google.com/maps/documentation/tile/3d-tiles
- Securing secrets on github: https://www.youtube.com/watch?v=IuT0Ua7V4xA
- Offline server for homemade 3D tiles: https://github.com/CesiumGS/cesium/tree/main/Documentation/OfflineGuide

<!-- Include the CesiumJS JavaScript and CSS files 
      @ https://developers.google.com/maps/documentation/tile/3d-tiles
-->
<script src="https://ajax.googleapis.com/ajax/libs/cesiumjs/1.105/Build/Cesium/Cesium.js"></script>
<link href="https://ajax.googleapis.com/ajax/libs/cesiumjs/1.105/Build/Cesium/Widgets/widgets.css" rel="stylesheet">

<div id="cesiumContainer"></div>
<script>

    // Set the Cesium Ion token to `null` to avoid warnings
    Cesium.Ion.defaultAccessToken = null;

    // Go to your google API console to get this value
    GOOGLE_API_KEY = "your-google-maps-api-key"

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

    const GOOGLE_URL = "https://tile.googleapis.com/v1/3dtiles/root.json?key=" + GOOGLE_API_KEY, 
      tileset = viewer.scene.primitives.add(new Cesium.Cesium3DTileset({
      url: GOOGLE_URL,
      showCreditsOnScreen: true,
    }));

    viewer.scene.globe.show = false;


    // Point the camera at the Googleplex
    viewer.scene.camera.setView({
      destination: new Cesium.Cartesian3(
        
        // google's building from example
        //  -2693797.551060477,
        //  -4297135.517094725,
        //  3854700.7470414364
    
        //-1638505.031170999,
        //-3670575.300085036, 
        // 5005447.782384179

         //-1641906.9002619397, 
         //-3665664.7493907656, 
         // 5004000.782384179

         //-1536205.7653611891, 
         //-3766031.6151890275, 
         // 4899541.872834316

          
          -1642000.8304259968, 
          -3666000.9879576718,
           4940000.0

        ),
        orientation: new Cesium.HeadingPitchRoll(
          -2.455010,
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


