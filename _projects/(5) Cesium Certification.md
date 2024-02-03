---
name: Cesium Developer Certification Progress
tools: [machine learning, big data, cloud native]
image: http://www.geosolutionsgroup.com/wp-content/uploads/2023/06/cesium-certified-dev-logo-sm.png?x31768
description: Resources for my GEOG-639 class...
---

# Cesium Developer Certification Progress

I'm in the process of finishing certification for becoming a cesium developer. As this is now an OGC standard, it will a useful GIS technology to know. Here are the basic pieces of it...

# Foundations I
https://cesium.com/learn/cesium-foundations/

Lessions 1-4:
- 


---
# Lesson 1: The Ceisum Platform

![b9f748130cd3b02ba0a227591eceab9e.png](resources/b9f748130cd3b02ba0a227591eceab9e.png)

- Cesium OpenSource / Proprietary Business Model
- Overview:
	- List itemCesiumJS was created in 2011 by an Analytical Graphics Inc.  (aerospace visualizations), and Cesium spun out as its own company in 2019.
	- Cesium Ion is the commerical wing of that.

## Knowledge Check:
- How did Cesium Start?
	- In 2011 as a company for aerospace visualizations. 
	- Patrick Cozzi, is the CEO
- What runtimes does Cesium Support:
	- O3DE, Unity, Omniverse, Unreal, CesiumJS, and 
- What open standard did cesium create:
	- [OGC 3D Tiles](https://www.ogc.org/standard/3dtiles/) 

* * *
# Lession 2: 3D Tiles
![8867ec3553ca41ea4e05e81525baab9a.png](resources/8867ec3553ca41ea4e05e81525baab9a.png)

## 2.1) Why was the 3D Tiles specification first created?

- To stream 3D models from sources such as Point Clouds, photogrammetry meshes, 3D buildings, vector data. 
- The exisiting tech didn't exist, so they created the tech & spec in 2015, and the OGC adopted it in 2019
	
## 2.2) What are the ten core features of 3D Tiles?

- **Open**, follows an OGC [specification](https://github.com/CesiumGS/3d-tiles)

- **Optimized for streaming and rendering**
	- Can show high-level abstractions, or zoom in for details (i.e. Optimzed for Hierarchical Level of Detail (*HLOD*))
		- ![95b6e184ca76fd9c818d0911118dcb92.png](resources/95b6e184ca76fd9c818d0911118dcb92.png)
		- ![4243ac9b32c7da9bc8650d11c0d049c0.png](resources/4243ac9b32c7da9bc8650d11c0d049c0.png)
		- ![20c7454c903ee272cf4023882e65fa01.png](resources/20c7454c903ee272cf4023882e65fa01.png)
		- ![3ea37963f079ad3947f651cfd89d777f.png](resources/3ea37963f079ad3947f651cfd89d777f.png)
	
- **Designed for 3D**
	- Not built in 2.5D, meaning you can have a 3D camera float around everywhere. 
	- Its *ontology* does not rely on constructs like "zoom levels", instead it uses a geometric rendering model, that uses "**tunable pixel error**", and "*geometric error* for Level-Of-Detail (LOD) *selection*" (e.g. for a given LOD, what is acceptable in terms of geometric error?). 
	- Bounding volumes are 3D extents, not 2D cartolography which is based on Web Mercator, which has its *poles bound to infinity*, making 3D calculations impractical
	- Also bc the US **DoD**, and the ***National System for Geospatial Intellegence***, says it is not a good idea. They have a [paper](https://nsgreg.nga.mil/doc/view?i=4478) on it.
	 
- **Interactive**
	- Support user interactions like mouseover!
		- ![d5043ca52cc1e6eeb3fb3ec7f9c554f0.png](resources/d5043ca52cc1e6eeb3fb3ec7f9c554f0.png)

- **Styleable**
	- Metadata for individual models, allow shading alteration at runtime without altering the code!
	- Height dependent styling !
		- ![c6dc3edc25513cac104f8e534f749156.png](resources/c6dc3edc25513cac104f8e534f749156.png)

- **Adaptable**
	- Can work with multiple subdivision strategies for 3D: Traditional 3D is quadtree, but that is unecessarily costly. 
		- ![b5b917a67f906eeb5f2a1742537ba914.png](resources/b5b917a67f906eeb5f2a1742537ba914.png)
		
- **Flexible**
	- Avoids unecessary data loads:
		- "**refinement**" = increasing the resolution
			- "**replacement *refinement***": 2D, when a user zooms in, and the visual map tiles are replaced with a higher-resolution one. 
			- "**Additive *refinement***": 3D, when you progressively add more data. 
				- ![3e0f5ff1adc36ba7515e12a8fbc3c6ef.png](resources/3e0f5ff1adc36ba7515e12a8fbc3c6ef.png)
				- Zoomed in, more details... ![dab5a9738e3ae873d690864d3986d741.png](resources/dab5a9738e3ae873d690864d3986d741.png)

	3D Data allows both types!

- **Heterogeneous**
	- 3D Tiles are heterogeneous because there is no one-size-fits-all for 3D datasets. 
		- **Batched models** (e.g., buildings) need a different representation from **instanced models** (e.g., trees), which need a different representation from **point clouds**, and so on.

	The heterogeneous nature of 3D Tiles allows discrete levels of detail combined with HLOD. 
	- EXAMPLE: a 3D building could be a billboard and label at one LOD, an extruded footprint at a higher LOD, a 3D model at the next LOD, and a textured 3D model at the highest LOD.

- **Precise**
	- Has full precision geometry, with roots in  rocket science. 

- **Temporal**
	- Designed for time-dynamic visualizations so you can see snow cover change over time. 


### 2.3) Why is metadata such a critical feature in the 3D Tiles 1.1 (aka "Next") specification?
- Metadata = semantics
- Because it allows the model to be rendered as one big block BUT have its individual features identified at runtime, which results in per-tile runtime processing and low CPU overhead during rendering
	- **[Specification Doc](https://github.com/CesiumGS/3d-tiles/tree/main/specification/Metadata)**
	- ![84eece563eabcc333d8b231c78de66a6.png](resources/84eece563eabcc333d8b231c78de66a6.png)
- The new 1.1 version allows metadata to be rendered in lookup tables that are aggregated
	- ![fc8d7f8b3e52fa8019eb8fc4ae958c3c.png](resources/fc8d7f8b3e52fa8019eb8fc4ae958c3c.png)
	- Left: per-texel colors showing the feature classification, e.g., roof, sky roof, windows, window frames, and AC units . Right: classification is used to determine rendering material properties, e.g., make the windows translucent.
	- ![3b5b0d22fe69d4951ee783413565817f.png](resources/3b5b0d22fe69d4951ee783413565817f.png)

### 2.4) What is Implicit vs Explicit Tiling Schemes?

#### Partial Updates!
- Implicit means that support for well-known **spatial indexes** without the need to explicitly define them.
- This enables random access capability at any time (aka, partial updates to a tile!)

#### Via Digital Twin Simulations
This partial update capability means that simulations streaming agents of a digital twin can be smooth AF!
- Implicit tiling supports massive simulations such as a crowd of people in a city. Spatial indexes enable efficient queries for nearby objects.
	- ![81f5242c2353658ef194c0bbe5c116f2.png](resources/81f5242c2353658ef194c0bbe5c116f2.png)

#### 2D Cartography integration
This means that implicit tiling can represent WMTS, TMS, and CDB data in the 3D space! Interoperability!

#### S2 Subdivision (Google spatial index)
Version 1.1 also includes S3: a [global subdivision](https://cesium.com/blog/2021/11/10/introducing-3d-tiles-next/#s2-subdivision), where each tile is equal area, and minimal distortion at the pole. 
- ![62a7512ef23cd469d9960fce63129826.png](resources/62a7512ef23cd469d9960fce63129826.png) The S2 Hilbert curve on the WGS84 ellipsoid.

#### Next Tile Spec (3.1)

Developer resources including the 3D Tiles Next Reference Card, sample data, and the upcoming 3D Tiles Next Tech blog series.
	- https://github.com/CesiumGS/3d-tiles/blob/main/next/3d-tiles-next-reference-card.pdf
	- https://github.com/CesiumGS/3d-tiles-samples

---
# Lesson 3: Cesium ion
https://cesium.com/learn/cesium-foundations/#lesson-3-cesium-ion







![preview](https://www.sketchappsources.com/resources/source-image/we-were-soldiers-landing-page-dbruggisser.jpg)

## Search Movies

![search](https://www.sketchappsources.com/resources/source-image/microsoft-windows-10-virtual-keyboard-diogo-sousa.png)

<p class="text-center">
{% include elements/button.html link="https://github.com/YoussefRaafatNasry/portfolYOU" text="Learn More" %}
</p>