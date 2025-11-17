# Catalogs and Datasets

## Intro

TerriaJS uses a catalog to store all of the data that is displayed on the map. The catalog is defined in a JSON file, which is loaded by the application when it starts up.

By the end of this section of the workshop, you will have a better understanding of how catalogs and datasets work in TerriaJS. You will be able to create your own catalogs and add datasets to them. You will also be able to define the properties of each dataset, such as its name, description, and style.

**_nb: A lot of the information in this guide is taken directly from [TerriaJS documentation](https://docs.terria.io/guide/connecting-to-data/) This is the best resource for learning about TerriaJS, and we recommend that you refer to it if you get stuck._**

TerriaJS supports 70 data APIs and file formats, and has around 1000 different configuration properties, so it can get complicated. We recommend starting with simple data sources (like Web Map Service and GeoJSON) instead of data sources that require extensive configuration (like CKAN and CSW).

There are list of examples for different data types in the [TerriaJS documentation](https://docs.terria.io/guide/connecting-to-data/#getting-started).

We also have a [user guide](https://userguide.terria.io/) that explains how to use the TerriaJS application.

#### The image below shows the catalog for the NationalMap app.

![Alt text](assets/catalog.png)

### Cross-Origin Resource Sharing (CORS)

If you are trying to load data from a different domain than your TerriaJS application, you may run into issues with Cross-Origin Resource Sharing (CORS). TerriaJS provides a way to work around these issues using a proxy. For more information on how to set up a proxy, please refer to the [TerriaJS documentation on CORS](https://docs.terria.io/guide/connecting-to-data/cross-origin-resource-sharing/).

**Note** if you are using the "pre-built" TerriaMap, you are unable to use the TerriaJS proxy. You will need to setup the full developer environment. If you encounter CORS issues, please let us know and we can help you get setup, or we can find alternative data sources that don't require a proxy.

## Catalogs

A catalog is a hierarchical tree structure that defines the datasets (catalog items) that are displayed on the map. Each node in the tree represents a catalog item or a group of catalog items. The catalog is defined in a JSON file, which is loaded by the application when it starts up.

## Catalog Items

A catalog item is a collection of data that can be displayed on the map. In TerriaJS, catalog items can be of different types, such as GeoJSON, WMS, or CSV. Each catalog item has a set of properties that define how it is displayed on the map.

Please refer to the docs for more information on [catalog items](https://docs.terria.io/guide/connecting-to-data/catalog-items).

## Catalog basics

As mentioned the we configure the catalog in JSON. JSON is a data format that is used to store and exchange data. It is a text-based format that is easy to read and write. It is also easy for computers to parse and generate.

Each catalog file:

- must be valid JSON

  - `"` not `'`
  - no comments
  - all keys must be quoted `{ "key": "value" }`
  - case matters `"esri-mapServer-group"`

### Lets get started

A very minimal example - this defines

- a group called "FOSS4G Group" with no members
- a default basemap of "basemap-openstreetmap" - a nice simple OpenStreetMap basemap
- a home camera position framing beautiful Auckland
- the default viewer mode to `3dSmooth` - which is Cesium without Terrain (a smooth globe)

```json
{
  "homeCamera": {
    "east": 174.8,
    "west": 174.7,
    "north": -36.8,
    "south": -36.9
  },
  "catalog": [
    {
      "name": "FOSS4G Group",
      "type": "group"
    }
  ],
  "viewerMode": "3dSmooth",
  "baseMaps": {
    "defaultBaseMapId": "basemap-openstreetmap",
    "previewBaseMapId": "basemap-openstreetmap"
  }
}
```

Your catalog can be found in `init/foss4g.json`. You can edit this and then reload the page to see changes.

### Add a basemap

We can configure the basemap in the catalog. Update the `baseMaps` property in your catalog to get a Tasmanian LIST basemap.

```json
{
  ...
  "baseMaps": {
    "defaultBaseMapId": "list-basemap",
    "previewBaseMapId": "basemap-openstreetmap",
    "enabledBaseMaps": [
      "basemap-natural-earth-II",
      "basemap-black-marble",
      "basemap-openstreetmap",
      "basemap-darkmatter",
      "list-basemap"
    ],
    "items": [
      {
        "image": "public/img/tasmania-basemap-icon.png",
        "item": {
          "allowFeaturePicking": false,
          "id": "list-basemap",
          "name": "LIST Simple Basemap",
          "opacity": 1,
          "type": "esri-mapServer",
          "url": "https://services.thelist.tas.gov.au/arcgis/rest/services/Basemaps/SimpleBasemap/MapServer/0"
        }
      }
    ]
  }
}
```

### Add a new dataset!

Here we are going to add an ArcGis MapServer layer (ESRI's version of WMS) from Land Information System Tasmania (LIST). The layer contains the Tasmanian Heritage Register.

Add the "Tasmanian Heritage Register" LIST ArcGis MapServer layer to the catalog, as a member of our "FOSS4G group"

```json
{
  "name": "FOSS4G Group",
  "type": "group",
  "members": [
    {
      "type": "esri-mapServer",
      "name": "Tasmanian Heritage Register",
      "url": "https://services.thelist.tas.gov.au/arcgis/rest/services/HT/HT_Public/MapServer/0"
    }
  ]
}
```

### The catalog file with LIST basemap and Tasmanian Heritage Register

This is what your catalog should look like now

```json
{
  "homeCamera": {
    "east": 174.8,
    "west": 174.7,
    "north": -36.8,
    "south": -36.9
  },
  "catalog": [
    {
      "name": "FOSS4G Group",
      "type": "group",
      "members": [
        {
          "type": "esri-mapServer",
          "name": "Tasmanian Heritage Register",
          "url": "https://services.thelist.tas.gov.au/arcgis/rest/services/HT/HT_Public/MapServer/0"
        }
      ]
    }
  ],
  "viewerMode": "3dSmooth",
  "baseMaps": {
    "defaultBaseMapId": "list-basemap",
    "previewBaseMapId": "basemap-openstreetmap",
    "enabledBaseMaps": [
      "basemap-natural-earth-II",
      "basemap-black-marble",
      "basemap-openstreetmap",
      "basemap-darkmatter",
      "list-basemap"
    ],
    "items": [
      {
        "image": "public/img/tasmania-basemap-icon.png",
        "item": {
          "allowFeaturePicking": false,
          "id": "list-basemap",
          "name": "LIST Simple Basemap",
          "opacity": 1,
          "type": "esri-mapServer",
          "url": "https://services.thelist.tas.gov.au/arcgis/rest/services/Basemaps/SimpleBasemap/MapServer/0"
        }
      }
    ]
  }
}
```

---

### Let's add some of your own data!

Do you have access to some data your wish to load. Check the documentation and get some help from the Terria team and let's add it to your map.

You can get started with different data types [here](https://docs.terria.io/guide/connecting-to-data/)

If you see an interesting dataset on one of our Maps - like NationalMap - let us know and we can share the TerriaJS configuration!

### Intro to some data types

Go to the documentation to see the full list of data types [here](https://docs.terria.io/guide/connecting-to-data/).

These are some of the most common data types you might use:

- [Tabular - CSV](#tabular---csv)
- [Vector - GeoJSON](#vector---geojson)
- [Vector - Shapefile](#vector---shapefile)
- [Vector - Web Feature Service (WFS)](#vector---web-feature-service-wfs)
- [Vector - ArcGis FeatureServer](#vector---arcgis-featureserver)
- [Imagery - Web Map Service (WMS)](#imagery---web-map-service-wms)
- [Imagery - ArcGis MapServer](#imagery---arcgis-mapserver)
- [Imagery - ArcGis ImageServer](#imagery---arcgis-imageserver)
- [Raster - Cloud optimized GeoTIFF (COG)](#raster---cloud-optimized-geotiff-cog)
- [3D - Cesium 3D Tiles](#3d---cesium-3d-tiles)
- [3D - Cesium 3D Terrain](#3d---cesium-3d-terrain)
- [3D - ArcGis SceneServer](#3d---arcgis-sceneserver)

### Tabular - CSV

For what CSVs are supported - see [csv-geo-au](https://github.com/NICTA/nationalmap/wiki/csv-geo-au).

Tabular data in Terria is very customisable, and can be difficult to get working. We have an "Edit Style" tool to help with this - see [Style Editor in the user guide](https://userguide.terria.io/interactions-functionalities-and-workflows#style-editor) and [this discussion post](https://github.com/TerriaJS/terriajs/discussions/6422#discussioncomment-3176804) on how to use it.

[Documentation](https://docs.terria.io/guide/connecting-to-data/catalog-type-details/csv)

#### Example

```json
{
  "type": "csv",
  "url": "https://tiles.terria.io/static/auspost-locations.csv",
  "name": "Australia Post Locations",
  "id": "some unique ID"
}
```

### Vector - GeoJSON

[Documentation](https://docs.terria.io/guide/connecting-to-data/catalog-type-details/geojson)

Terria has support for a limited number of CRSs, but GeoJSON _should_ be WGS84 (EPSG:4326).

#### Example

```json
{
  "type": "geojson",
  "url": "https://tiles.terria.io/terriajs-examples/geojson/bike_racks.geojson",
  "name": "geojson example"
}
```

### Vector - Shapefile

[Documentation](https://docs.terria.io/guide/connecting-to-data/catalog-type-details/shp)

Shapefile must be zipped (can include `shp`, `dbf`, `prj`, and `cpg` properties)

```json
{
  "type": "shp",
  "name": "shp (shapefile) example",
  "url": "https://tiles.terria.io/terriajs-examples/shp/airports.zip"
}
```

### Vector - Web Feature Service (WFS)

[Documentation](https://docs.terria.io/guide/connecting-to-data/catalog-type-details/wfs)

**Note** there is a feature limit of 1000. This can be adjusted using the `maxFeatures` property.

```json
{
  "type": "wfs",
  "name": "wfs example",
  "url": "https://warehouse.ausseabed.gov.au/geoserver/ows",
  "typeNames": "ausseabed:AHO_Reference_Surface__Broome__2023_0_5m_L0_Coverage"
}
```

### Vector - ArcGis FeatureServer

[Documentation](https://docs.terria.io/guide/connecting-to-data/catalog-type-details/esri-featureServer)

**Note** there is a feature limit of 5000. This can be adjusted using the `maxFeatures` property.

```json
{
  "url": "https://services5.arcgis.com/OvOcYIrJnM97ABBA/ArcGIS/rest/services/Public_Hospitals_2021_22/FeatureServer/3",
  "type": "esri-featureServer",
  "name": "Australian Public Hospitals"
}
```

### Imagery - Web Map Service (WMS)

[Documentation](https://docs.terria.io/guide/connecting-to-data/catalog-type-details/wms)

**Note** Web Mercator (EPSG:3857) and WGS84 (EPSG:4326) image tiles are supported.

```json
{
  "type": "wms",
  "name": "Mangrove Cover",
  "url": "https://ows.services.dea.ga.gov.au",
  "layers": "ga_ls_mangrove_cover_cyear_3"
}
```

### Imagery - ArcGis MapServer

[Documentation](https://docs.terria.io/guide/connecting-to-data/catalog-type-details/esri-mapServer)

**Note** Web Mercator (EPSG:3857) and WGS84 (EPSG:4326) image tiles are supported.

```json
{
  "url": "https://services.ga.gov.au/gis/rest/services/GA_Surface_Geology/MapServer",
  "type": "esri-mapServer",
  "name": "Surface Geology"
}
```

### Imagery - ArcGis ImageServer

[Documentation](https://docs.terria.io/guide/connecting-to-data/catalog-type-details/esri-imageServer)

**Note** Web Mercator (EPSG:3857) and WGS84 (EPSG:4326) image tiles are supported.

```json
{
  "url": "https://sampleserver6.arcgisonline.com/arcgis/rest/services/CharlotteLAS/ImageServer",
  "type": "esri-imageServer",
  "name": "CharlotteLAS"
}
```

### Raster - Cloud optimized GeoTIFF (COG)

[Documentation](https://docs.terria.io/guide/connecting-to-data/catalog-type-details/cog)

**Note** Web Mercator (EPSG:3857) and WGS84 (EPSG:4326) rasters are supported, we have experimental support for reprojection, but expect issues!

```json
{
  "name": "COG Test Uluru",
  "type": "cog",
  "url": "https://sentinel-cogs.s3.us-west-2.amazonaws.com/sentinel-s2-l2a-cogs/52/J/FS/2023/5/S2A_52JFS_20230501_0_L2A/TCI.tif"
}
```

### 3D - Cesium 3D Tiles

[Documentation](https://docs.terria.io/guide/connecting-to-data/catalog-type-details/3d-tiles)

Cesium 3D Tiles can be a `url` to a 3d-tiles JSON file, or an `ionAssetId` to a Cesium Ion asset.

- Cesium Ion can be used to host and transform a variety of 3D formats - including 3D Models (OBJ, FBX, ...), Point Clouds (LAS, XYZ) and Terrain (GeoTIFF, ASCII Image)
- You can also set the `ionAccessToken` property to grant access to your Cesium Ion assets.

#### `ionAssetId`

Note, this requires a Cesium Ion access token to be set in the `ionAccessToken` property.

```json
{
  "type": "3d-tiles",
  "ionAssetId": 96188,
  "ionAccessToken": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJqdGkiOiJlM2MxODAwNC1mZmY3LTRkNzQtYmE4YS1hMGQzODhhNjQ3OTkiLCJpZCI6MjUyMzkzLCJpYXQiOjE3MzA1NDYxODl9.6ofnHtsKouZs8RU45MbtxuWLI38WcbIDK3sJHKDhwR0",
  "name": "Cesium OSM Buildings"
}
```

#### `url`

```json
{
  "type": "3d-tiles",
  "url": "https://tiles.terria.io/3d-tiles/photomesh/melbourne/tileset.json",
  "name": "CoM Melbourne 3D Photo Mesh"
}
```

### 3D - Cesium 3D Terrain

[Documentation](https://docs.terria.io/guide/connecting-to-data/catalog-type-details/cesium-terrain)

Cesium 3D Tiles can be a `url` to a directory of Cesium Terrain, or an `ionAssetId` to a Cesium Ion asset.

- You can also set the `ionAccessToken` property to grant access to your Cesium Ion assets.

#### `ionAssetId`

```json
{
  "type": "cesium-terrain",
  "ionAccessToken": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJqdGkiOiJlM2MxODAwNC1mZmY3LTRkNzQtYmE4YS1hMGQzODhhNjQ3OTkiLCJpZCI6MjUyMzkzLCJpYXQiOjE3MzA1NDYxODl9.6ofnHtsKouZs8RU45MbtxuWLI38WcbIDK3sJHKDhwR0",
  "ionAssetId": 1,
  "name": "Cesium World Terrain"
}
```

### 3D - ArcGis SceneServer (I3S)

The ESRI version of 3d-tiles

[Documentation](https://docs.terria.io/guide/connecting-to-data/catalog-type-details/i3s)

```json
{
  "type": "i3s",
  "name": "NYC Buildings",
  "url": "https://tiles.arcgis.com/tiles/z2tnIkrLQ2BRzr6P/arcgis/rest/services/NYC_Attributed_v17/SceneServer"
}
```

### Advanced options

TerriaJS catalogs have many other configuration options. You can find them in the [TerriaJS Init Source Documentation](...asdfasdf)

### Temporary Cesium Ion code

```json
eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJqdGkiOiJlM2MxODAwNC1mZmY3LTRkNzQtYmE4YS1hMGQzODhhNjQ3OTkiLCJpZCI6MjUyMzkzLCJpYXQiOjE3MzA1NDYxODl9.6ofnHtsKouZs8RU45MbtxuWLI38WcbIDK3sJHKDhwR0
```

#### Test catalog item

```json
{
  "type": "3d-tiles",
  "ionAssetId": 96188,
  "ionAccessToken": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJqdGkiOiJlM2MxODAwNC1mZmY3LTRkNzQtYmE4YS1hMGQzODhhNjQ3OTkiLCJpZCI6MjUyMzkzLCJpYXQiOjE3MzA1NDYxODl9.6ofnHtsKouZs8RU45MbtxuWLI38WcbIDK3sJHKDhwR0",
  "name": "Cesium OSM Buildings"
}
```

#### Get your Terrain working!

Edit `config.json` file - add to `parameters` object

```json
{
  "parameters": {
    ...,
    "cesiumIonAccessToken": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJqdGkiOiJlM2MxODAwNC1mZmY3LTRkNzQtYmE4YS1hMGQzODhhNjQ3OTkiLCJpZCI6MjUyMzkzLCJpYXQiOjE3MzA1NDYxODl9.6ofnHtsKouZs8RU45MbtxuWLI38WcbIDK3sJHKDhwR0",
```
