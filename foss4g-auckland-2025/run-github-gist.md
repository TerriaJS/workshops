# Add a catalog to one of our hosted TerriaMaps

There are two options here

- You can drag and drop a catalog.json file onto one of our hosted TerriaMaps
- You can use GitHub Gist to create a catalog

**Note** these methods only allow you to change the catalog (`foss4g.json`) file, not the configuration (`config.json`) file.

If you want to change the configuration, you will need to setup a local TerriaMap.

## Drag and drop a catalog.json file onto one of our hosted TerriaMaps

### Guide

- Go to http://ci.terria.io/main/#clean
  - The `#clean` will clear the current catalog
- Drag your `foss4g.json` file onto the page
- You should see the catalog appear on the map
- **Note** to update your catalog, you will need to reload the page, and drag the file again

## Use GitHub Gist to create a catalog

If you can't follow the [Run pre-built TerriaMap locally](run-locally.md) guide, you can use GitHub Gist to create a catalog.

### Guide

- Go to https://gist.github.com/
- Create a new Gist

Paste in the following JSON

```json
{
  "homeCamera": {
    "north": -34,
    "east": 178,
    "south": -49,
    "west": 166
  },
  "catalog": [
    {
      "name": "FOSS4G Group",
      "type": "group"
    }
  ],
  "viewerMode": "3dSmooth",
  "baseMaps": {
    "defaultBaseMapId": "basemap-positron",
    "previewBaseMapId": "basemap-positron"
  }
}
```

- Create a Public Gist
- **Make sure the name ends with `.json`**
- Click the "Raw" button
- Copy URL
- Go to http://ci.terria.io/main/#clean&___PASTE_URL_HERE___
