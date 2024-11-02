# Theming (JSON based)

This is the JSON based version - this will work for both pre-built and full TerriaMap developer environment

Also see

- [Theming (SASS based) - for TerriaMap developer environment](theming.md)

## Intro

Once you have your local development environment set up, the next step is to modify the look and feel of the map to suit you!

**_TIPS: Think of a good specific use case for your map._** Mine is for the 'Unknown Rangers', a ranger group working on managing the natural and cultural values of a remote area. Note here, that I have customised the colour scheme and have a title and a cool logo of a shark. The starting view of the map is also customised to be over an area of impressive terrain, and the map is set to initialise in 3D mode:

![Alt text](assets/themed_map_example1.png)

## Step 1: Edit the Colours

We want to change some of the elements to make it our own:

Add the `"theme"` property to `"parameters"` in your `config.json` file.

```json
"parameters": {
  ...,
  "theme": {
    "charcoalGrey": "#3f4854",
    "colorPrimary": "#519ac2",
    "colorSplitter": "#ff6f00",
    "compassWidth": "56",
    "dark": "#3f4854",
    "darkWithOverlay": "#667080",
    "frontComponentZIndex": "99",
    "grey": "#888888",
    "greyLighter": "#ddd",
    "greyLighter2": "#e6e6e6",
    "greyLightest": "#f2f2f2",
    "lg": "1300",
    "mapButtonColor": "#9ca1aa",
    "mapButtonTop": "18",
    "mapNavigationTop": "80",
    "md": "992",
    "mobile": "767",
    "modalBg": "#fff",
    "modalHighlight": "#519ac2",
    "modalText": "#000",
    "overlay": "rgba(255, 255, 255, 0.15)",
    "overlayInvert": "rgba(255, 255, 255, 0.85)",
    "radius40Button": "20",
    "radiusLarge": "4px",
    "radiusSmall": "2px",
    "ringWidth": "10",
    "sm": "768",
    "spacing": "5",
    "textBlack": "#000",
    "textDark": "#595b60",
    "textDarker": "#4d5766",
    "textLight": "#ffffff",
    "textLightDimmed": "#bbbbbb",
    "trainerHeight": "64",
    "workbenchWidth": "350"
  },
```

And here is a hint to the elements that they modify:

![image](https://github.com/TerriaJS/workshops/assets/6187649/bc2f467d-a32d-42ac-90e0-6274adb2cc73)

Save your changes and then refresh your browser at http://localhost:3000/

## Step 2: Change the Branding Bar

At the top left of the screen is the Branding Bar. This is defined as an html string in the `config.json` file of `TerriaMap`.

[Here is the parameter that we will modify](https://github.com/TerriaJS/TerriaMap/blob/14bf848b651a8403401f3c7a39f6a4075a0654c7/wwwroot/config.json#L47)

But first, we need to generate a logo.
You can do this with any image editor, [GIMP](https://www.gimp.org/downloads/) on your desktop, or https://www.photopea.com/ online if you dont want to install software:

<img src="assets/photopea_example.png" alt="Photopea Online Editor" width="600"/>

- Make a new canvas 320px by 52px.
- Add some text and an image.
- I prefer to make a transparent PNG with white text...
- Then save the image to your copy of the TerriaMap repo at `TerriaMap/wwwroot/images/branding-bar.png`

Now modify the code for
["brandBarElements"here](https://github.com/TerriaJS/TerriaMap/blob/14bf848b651a8403401f3c7a39f6a4075a0654c7/wwwroot/config.json#L47) to point to your image at `image/branding-bar.png`.

## Step 3: Other Tidy Up

Some more properties in `config.json` you may want to change:

```
["parameters"]["appName"]
["parameters"]["supportEmail"]
["parameters"]["languageConfiguration"]["languages"]
["initializationUrls"]
```

TerriaJS has many other configuration options available - you can see them all in the [TerriaJS Config Documentation](https://docs.terria.io/configuration....)
