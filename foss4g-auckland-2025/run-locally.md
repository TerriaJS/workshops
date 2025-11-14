# Run pre-built TerriaMap locally

TerriaMap is a NodeJS package, that gets built to run in a web browser. This can be finicky, so we have pre-built the latest version of Terria for you!

This has some limitations, as it doesn't include the TerriaJS-Server component:

- The main limitation is the lack of Proxy server - so if you encounter CORS errors, you will not be able to fix them. We talk more about CORS in the [Setting up your catalog](catalogs-and-datasets.md#cross-origin-resource-sharing-cors) guide
- TerriaJS is identical, so if you transition to using your own version of TerriaMap, everything you learn will still apply!

## Guide

- Go to https://github.com/TerriaJS/terriamap-static
- Clone/download our repository
- Open Terminal in `terriamap-static` folder
- Make sure you have NodeJS installed
- Run `npx serve`
  - It will ask you to install `serve` if you don't have it installed - which is a simple NodeJS package to serve static files
  - Alternatively if you don't have NodeJS installed using python3 `python -m http.server 3000`
- Go to http://localhost:3000/
- Can you see a globe? Then you can move on to
  - [Setting up your catalog](catalogs-and-datasets.md)
  - [Theming (JSON based)](theming-json-based.md)
