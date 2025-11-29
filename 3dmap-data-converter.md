# Document describing conversion tools and procedures

## Execution environment for conversion tools

- OS: Windows 11 Pro (24H2)
- CPU: AMD Ryzen 7 5700X 8‑Core Processor 3.40 GHz
- Memory: 64.0 GB
- SSD: 4 TB

## Data used

### VIRTUAL SHIZUOKA point cloud data (LP data, original data in LAS format)

- Obtain the VIRTUAL SHIZUOKA point cloud data (LP data, original data in LAS format) from the G Spatial Information Center.
  [VIRTUAL SHIZUOKA point cloud data](https://www.geospatial.jp/ckan/dataset?q=+VIRTUAL+SHIZUOKA+%E7%82%B9%E7%BE%A4&sort=metadata_modified+desc)

### 3D City Model (Project PLATEAU) Numazu City (FY2021) CityGML (v2)

- Obtain the 3D city model (Project PLATEAU) building model (CityGML format) from the G Spatial Information Center.
  [3D City Model (Project PLATEAU) Numazu City (FY2021)](https://www.geospatial.jp/ckan/dataset/plateau-22203-numazu-shi-2021)
- Although data for Numazu City for FY2023 is also published, the conversion process with the converter does not work properly, so the FY2021 data is used.

## Target area

- Numazu City, Shizuoka Prefecture
  - Second‑order mesh (10 km square): 523856
  - Third‑order mesh (1 km square): 52385628

![alt text](対象範囲.png)

## Conversion of 3D point cloud data to 3D Tiles

### Conversion tools

- QGIS 3.34.12 (bundled PDAL)
  - pdal 2.8.1
  - https://pdal.io/en/2.8.1/

- py3dtiles 9.0.0
  - https://py3dtiles.org/v9.0.0/

### Installing conversion tools

- pdal
  - Installing QGIS 3.34.12 also installs OSGeo4W Shell and PDAL.
  - Start OSGeo4W Shell and run the pdal command.
  - Check the pdal version.

    ```
    C:\Program Files\QGIS 3.34.12>pdal --version
    --------------------------------------------------------------------------------
    pdal 2.8.1 (git-version: a06325)
    --------------------------------------------------------------------------------
    ```

- py3dtiles
  - Start Command Prompt and install py3dtiles by running the following command.

    ```
    pip install py3dtiles
    ```

  - Check the py3dtiles version.

    ```
    C:\Users\yshiw>pip show py3dtiles
    Name: py3dtiles
    Version: 9.0.0
    Summary: Python module for 3D tiles format
    Home-page: https://py3dtiles.org
    Author:
    Author-email: The Py3DTiles team <contact@oslandia.com>
    License: Apache-2.0
    Location: C:\Users\yshiw\AppData\Local\Programs\Python\Python312\Lib\site-packages
    Requires: cython, earcut, lz4, numba, numpy, psutil, pygltflib, pyproj, pyzmq
    Required-by:
    ```

  - Install laspy[laszip] so that LAZ can be handled.

    ```
    pip install laspy[laszip]
    ```

### Merging LAS files

- The 3D point cloud data is divided according to the “National Base Map grid (map information level 500, 300 m × 400 m)”, so LAS files are merged by second‑order mesh (10 km square) and third‑order mesh (1 km square).
- PDAL pipelines are used for merging.
- Prepare pipeline-merge-2ji.json and pipeline-merge-3ji.json.
- In "bounds", specify the lower‑left Y, upper‑right Y, lower‑left X, and upper‑right X coordinates of the target second‑order or third‑order mesh.
  Note: Since the 3D point cloud data uses Japan Plane Rectangular CS Zone 8, X and Y coordinates should be specified in that CRS.
- The following shows examples of merging for second‑order mesh code 523856 and third‑order mesh code 52385628.

- pipeline-merge-2ji.json
