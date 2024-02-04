---
name: CesiumJS Viewer / Jekyll Integration
tags: [gis, cesiumjs, o3de, 3D, cloud-native]
image: http://www.geosolutionsgroup.com/wp-content/uploads/2023/06/cesium-certified-dev-logo-sm.png?x31768
description: Seeing if I can Embed the Viewer in a Static Page embedded on GitHub
---

First test for the cesium viewer on a static page! 


<!-- Include the CesiumJS JavaScript and CSS files 
      @ https://developers.google.com/maps/documentation/tile/3d-tiles
-->
<script src="https://ajax.googleapis.com/ajax/libs/cesiumjs/1.105/Build/Cesium/Cesium.js"></script>
<link href="https://ajax.googleapis.com/ajax/libs/cesiumjs/1.105/Build/Cesium/Widgets/widgets.css" rel="stylesheet">

<div id="cesiumContainer"></div>
<script>
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


</script>


