---
name: CesiumJS Viewer / Jekyll Integration
tags: [gis, cesiumjs, o3de, 3D, cloud-native]
image: http://www.geosolutionsgroup.com/wp-content/uploads/2023/06/cesium-certified-dev-logo-sm.png?x31768
description: Seeing if I can Embed the Viewer in a Static Page embedded on GitHub
---

First test for the cesium viewer on a static page! 

<script src="https://cesium.com/downloads/cesiumjs/releases/1.70/Build/Cesium/Cesium.js"></script>
<link href="https://cesium.com/downloads/cesiumjs/releases/1.70/Build/Cesium/Widgets/widgets.css" rel="stylesheet">

<div id="cesiumContainer" style="width: 900px; height:600px; border-radius:1em"></div>
<script>

    var viewer = new Cesium.Viewer("cesiumContainer", {
        terrainProvider: Cesium.createWorldTerrain(),
    });

    var tileset = new Cesium.Cesium3DTileset({
        url: 'https://s3.us-east-2.amazon.com/construkted-assets/0gy35muf8i/tileset.json'
    });

  tileset.modelMatrix = Cesium.Transforms.eastNorthUpToFixedFrame(Cesium.Cartesian3.fromDegrees(5, 6, 25));
    viewer.scene.primitives.add(tileset);
    viewer.zoomTo(tileset);
</script>
