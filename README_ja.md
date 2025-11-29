# 3Dウェブ地図表示ツール
- CesuimJS
  - 静岡県沼津市 3次元点群データ（3D Tiles）  
https://tossetolab.github.io/3dmapcompare/index_1_1.html
  - 静岡県沼津市 建築物モデル（3D Tiles）  
https://tossetolab.github.io/3dmapcompare/index_1_2.html

- MapLibre GL JS、deck.gl等
  - 静岡県沼津市 3次元点群データ（3D Tiles）  
https://tossetolab.github.io/3dmapcompare/index_2_1.html
  - 静岡県沼津市 建築物モデル（3D Tiles）  
https://tossetolab.github.io/3dmapcompare/index_2_2.html
  - 静岡県沼津市 建築物モデル（MVT）  
https://tossetolab.github.io/3dmapcompare/index_2_3.html

# 構築の手順メモ
## 必要な環境
- ブラウザ: Google Chrome または Microsoft Edge
- 開発環境: ローカルサーバー環境（Visual Studio Code(以下、VSCode) 拡張機能:Live Server）※VSCodeのバージョン1.96.2
- インターネット接続: 必須（地理院タイル（標準地図）やAWS S3にホスティングされた3D TilesやMVTへのアクセスが必要なため）

## 使用ライブラリ
### [CesiumJS](https://github.com/CesiumGS/cesium)
- バージョン: 1.99
- 高性能な3D地図表示・視覚化ライブラリでWebGLを利用して3D Tiles等を表示可能。
- 3D Tilesの描画に使用

### [MapLibre GL JS](https://github.com/maplibre/maplibre-gl-js)
- バージョン: 4.5.0
- Web地図表示用のオープンソースライブラリ

### [deck.gl](https://github.com/visgl/deck.gl)
- バージョン: 8.9.0
- 高度なデータ視覚化を可能にするWebGLベースのオープンソースライブラリ
- 3D Tilesの描画に使用

### [loaders.gl](https://github.com/visgl/loaders.gl)
- バージョン: 2.3.0
- 各種データフォーマット（3D Tilesなど）を扱うためのツールセット
- 3次元点群データ（3D Tiles）のローダーとして使用

## 使用データ
[3次元ウェブ地図表示のためのデータ変換](https://tossetolab.github.io/3dmapcompare/3dmap-data-converter/)にて作成した、以下の3次元点群データおよび3D都市モデルPLATEAU建築物モデル（2次メッシュまたは3次メッシュ）のタイルデータを使用します。  
- ※注意事項1:3次元点群データの3D Tilesのバージョンは1.0、3D都市モデルPLATEAU建築物モデルの3D Tilesのバージョンは1.1となっています。  
- ※注意事項2:3D都市モデルPLATEAU建築物モデルの3D Tilesのバージョンは1.1ですが、deck.glでの読み込みに対応させるため、tileset.jsonの"version": "1.0"を"version": "0.0"に変更しています。
- 3次元点群データ2次メッシュ523856(3D Tiles形式)  
https://public-data.geolonia.com/komazawa-u-3dmap/3dtiles_pc_523856/tileset.json
- 3次元点群データ3次メッシュ52385628(3D Tiles形式)  
https://public-data.geolonia.com/komazawa-u-3dmap/3dtiles_pc_52385628/tileset.json
- 3D都市モデルPLATEAU建築物モデル2次メッシュ523856(3D Tiles形式)  
https://public-data.geolonia.com/komazawa-u-3dmap/3dtiles_bldg_523856_2021/tileset.json
- 3D都市モデルPLATEAU建築物モデル3次メッシュ52385628(3D Tiles形式)  
https://public-data.geolonia.com/komazawa-u-3dmap/3dtiles_bldg_52385628_2021/tileset.json
- 3D都市モデルPLATEAU建築物モデル2次メッシュ523856(MVT形式)  
https://public-data.geolonia.com/komazawa-u-3dmap/mvt_bldg_523856_2021/{z}/{x}/{y}.pbf
- 3D都市モデルPLATEAU建築物モデル3次メッシュ52385628(MVT形式)  
https://public-data.geolonia.com/komazawa-u-3dmap/mvt_bldg_52385628_2021/{z}/{x}/{y}.pbf


## 手順
### ファイルの準備
- GitHubレポジトリの index.html ファイルを任意のローカルディレクトリに保存します。

### ローカルサーバーの起動
- VSCode の 拡張機能:Live Server を使用します。
- VSCode を開き、index.html のあるディレクトリを開きます。
- 拡張機能:Live Server をインストールして有効化します。

### 動作確認
- index.htmlを開き、Go LiveをクリックするとLive Serverが起動します。
- 地理院タイル（標準地図）や3D Tiles、MVT等のタイルデータが表示されることを確認してください。

### 注意事項
#### タイルデータ（3D Tiles、MVT）のURLの変更
- デフォルトでは、3次メッシュのタイルデータを読み込むようにしています。
- 必要に応じて index.html 内のタイルデータのURLを編集します。
- CesuimJS / 静岡県沼津市 3次元点群データ（3D Tiles）の該当箇所
```javaScript
    // 3次元点群データ（3D Tiles）
    var pc_3dtiles = viewer.scene.primitives.add(new Cesium.Cesium3DTileset({
      // url: 'https://public-data.geolonia.com/komazawa-u-3dmap/3dtiles_pc_523856/tileset.json' // 2次メッシュ
      url: 'https://public-data.geolonia.com/komazawa-u-3dmap/3dtiles_pc_52385628/tileset.json' // 3次メッシュ
    }));
```
  
- CesuimJS / 静岡県沼津市 建築物モデル（3D Tiles）の該当箇所
```javaScript
    // 建築物モデル（3D Tiles）
    var bldg_3dtiles = viewer.scene.primitives.add(new Cesium.Cesium3DTileset({
      // url: 'https://public-data.geolonia.com/komazawa-u-3dmap/3dtiles_bldg_523856_2021/tileset.json' // 2次メッシュ
      url: 'https://public-data.geolonia.com/komazawa-u-3dmap/3dtiles_bldg_52385628_2021/tileset.json' // 3次メッシュ
    }));
```
- MapLibre GL JS、deck.gl等 / 静岡県沼津市 3次元点群データ（3D Tiles）
```javaScript
      // 3次元点群データ（3D Tiles）
      const tile3dLayer = new deck.MapboxLayer({
        id: "numazushi-pc",
        type: deck.Tile3DLayer,
        pointSize: 1,
        // data: 'https://public-data.geolonia.com/komazawa-u-3dmap/3dtiles_pc_523856/tileset.json', // 2次メッシュ
        data: 'https://public-data.geolonia.com/komazawa-u-3dmap/3dtiles_pc_52385628/tileset.json', // 3次メッシュ
        loader: Tiles3DLoader
      });
```
- MapLibre GL JS、deck.gl等 / 静岡県沼津市 建築物モデル（3D Tiles）
```javaScript
      // MapboxOverlayを使ったインターリーブ
      const overlay = new deck.MapboxOverlay({
        interleaved: true,
        layers: [
          // 建築物モデル（3D Tiles）
          new deck.Tile3DLayer({
            id: 'numazushi-bldg',
            // data: 'https://public-data.geolonia.com/komazawa-u-3dmap/3dtiles_bldg_523856_2021/tileset.json', // 2次メッシュ
            data: 'https://public-data.geolonia.com/komazawa-u-3dmap/3dtiles_bldg_52385628_2021/tileset.json', // 3次メッシュ
            opacity: 1,
            pointCloud: false,
            onTileLoad: d => {
              const { content } = d;
              content.cartographicOrigin.z -= 40.4420 + 8.5;
            }
          })
        ]
      });
```
- MapLibre GL JS / 静岡県沼津市 建築物モデル（MVT）
```javaScript
      // 建築物モデル（MVT）ソース
      map.addSource("numazushi-bldg", {
        type: 'vector',
        // tiles: ['https://public-data.geolonia.com/komazawa-u-3dmap/mvt_bldg_523856_2021/{z}/{x}/{y}.pbf'], // 2次メッシュ
        tiles: ['https://public-data.geolonia.com/komazawa-u-3dmap/mvt_bldg_52385628_2021/{z}/{x}/{y}.pbf'], // 3次メッシュ
        minzoom: 13,
        maxzoom: 17,
        attribution: '<a href="https://www.geospatial.jp/ckan/dataset/plateau-22203-numazu-shi-2021" target="_blank">3D都市モデル（Project PLATEAU）沼津市（2021年度）</a>'
      });
```
