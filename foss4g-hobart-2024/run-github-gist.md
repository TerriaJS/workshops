# Use GitHub Gist to create a catalog

If you can't follow the [Run pre-built TerriaMap locally](run-locally.md) guide, you can use GitHub Gist to create a catalog.

## Guide

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
- Click the "Raw" button
- Copy URL
- Go to https://ci.terria.io/main/#clean&___PASTE_URL_HERE___
