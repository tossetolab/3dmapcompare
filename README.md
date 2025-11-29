# 3D Web Map Viewer

- CesiumJS
  - Numazu City, Shizuoka Prefecture – 3D point cloud data (3D Tiles)
    https://tossetolab.github.io/3dmapcompare/index_1_1.html
  - Numazu City, Shizuoka Prefecture – building model (3D Tiles)
    https://tossetolab.github.io/3dmapcompare/index_1_2.html

- MapLibre GL JS, deck.gl, etc.
  - Numazu City, Shizuoka Prefecture – 3D point cloud data (3D Tiles)
    https://tossetolab.github.io/3dmapcompare/index_2_1.html
  - Numazu City, Shizuoka Prefecture – building model (3D Tiles)
    https://tossetolab.github.io/3dmapcompare/index_2_2.html
  - Numazu City, Shizuoka Prefecture – building model (MVT)
    https://tossetolab.github.io/3dmapcompare/index_2_3.html

For details on data conversion to 3D Tiles and MVT, see the following document:
- [3D Map Data Converter Documentation](3dmap-data-converter/3dmap-data-converter.md)

# Notes on Build Procedure

## Required environment

- Browser: Google Chrome or Microsoft Edge
- Development environment: Local server environment (Visual Studio Code (VSCode) extension: Live Server)
  - VSCode version: 1.96.2
- Internet connection: Required (to access GSI standard map tiles and 3D Tiles / MVT hosted on AWS S3)

## Libraries used

### [CesiumJS](https://github.com/CesiumGS/cesium)

- Version: 1.99
- High‑performance 3D map rendering and visualization library using WebGL that can display 3D Tiles and other formats
- Used for rendering 3D Tiles

### [MapLibre GL JS](https://github.com/maplibre/maplibre-gl-js)

- Version: 4.5.0
- Open‑source library for web map rendering

### [deck.gl](https://github.com/visgl/deck.gl)

- Version: 8.9.0
- WebGL‑based open‑source library that enables advanced data visualization
- Used for rendering 3D Tiles

### [loaders.gl](https://github.com/visgl/loaders.gl)

- Version: 2.3.0
- Toolkit for handling various data formats (including 3D Tiles)
- Used as a loader for 3D point cloud data (3D Tiles)

## Data used

This viewer uses the following 3D point cloud data and tiled datasets of 3D city model PLATEAU building models (second‑order or third‑order mesh) generated in the project “[Data conversion work for 3D web map visualization](3dmap-data-converter/)”.

- Note 1: The 3D Tiles version of the 3D point cloud data is 1.0, while the 3D Tiles version of the 3D city model PLATEAU building models is 1.1.
- Note 2: Although the 3D Tiles version of the 3D city model PLATEAU building models is 1.1, in order to make it loadable in deck.gl, the `"version": "1.0"` field in tileset.json has been changed to `"version": "0.0"`.

- 3D point cloud data, second‑order mesh 523856 (3D Tiles format)
  https://public-data.geolonia.com/komazawa-u-3dmap/3dtiles_pc_523856/tileset.json
- 3D point cloud data, third‑order mesh 52385628 (3D Tiles format)
  https://public-data.geolonia.com/komazawa-u-3dmap/3dtiles_pc_52385628/tileset.json
- 3D city model PLATEAU building model, second‑order mesh 523856 (3D Tiles format)
  https://public-data.geolonia.com/komazawa-u-3dmap/3dtiles_bldg_523856_2021/tileset.json
- 3D city model PLATEAU building model, third‑order mesh 52385628 (3D Tiles format)
  https://public-data.geolonia.com/komazawa-u-3dmap/3dtiles_bldg_52385628_2021/tileset.json
- 3D city model PLATEAU building model, second‑order mesh 523856 (MVT format)
  https://public-data.geolonia.com/komazawa-u-3dmap/mvt_bldg_523856_2021/{z}/{x}/{y}.pbf
- 3D city model PLATEAU building model, third‑order mesh 52385628 (MVT format)
  https://public-data.geolonia.com/komazawa-u-3dmap/mvt_bldg_52385628_2021/{z}/{x}/{y}.pbf

## Steps

### Preparing files

- Save the index.html file from the GitHub repository into any local directory.

### Starting a local server

- Use the VSCode extension “Live Server”.
- Open VSCode and open the directory that contains index.html.
- Install and enable the Live Server extension.

### Operation check

- Open index.html and click “Go Live” to start Live Server.
- Check that GSI standard map tiles, 3D Tiles, MVT, and other tile data are displayed correctly.

### Notes

#### Changing URLs for tile data (3D Tiles, MVT)

- By default, tile data for the third‑order mesh is loaded.
- Edit the tile data URLs in index.html as needed.
- CesiumJS / Numazu City, Shizuoka Prefecture – 3D point cloud data (3D Tiles)
