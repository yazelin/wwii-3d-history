# WWII 3D History

第二次世界大戰互動式戰情室。這個 repository 同時保留兩個 GitHub Pages 預覽版本：

- 3D 地球版：https://yazelin.github.io/wwii-3d-history/
- 平面地圖版：https://yazelin.github.io/wwii-3d-history/flat/

## 內容

網站以單頁靜態 HTML 呈現二戰主要戰區與事件，包含：

- 1939-1945 年時間軸播放
- 歐洲、太平洋、北非等鏡頭預設
- 同盟國、軸心國、中立區域標示
- 戰役事件卡、戰力、將領、陣型、計策與天氣
- 軍隊、旗幟、航線、攻勢與爆炸/煙霧/天候等 Three.js 視覺效果

這是一個互動式歷史視覺化作品，地圖邊界、戰力數值與事件呈現偏向教學與敘事用途，不是嚴格的 GIS 或軍史資料庫。

## 檔案結構

```text
.
├── index.html       # 目前的 3D 地球版
├── flat/
│   └── index.html   # 6b00b40 版本延伸出的平面地圖版
├── LICENSE
└── README.md
```

## 本機預覽

這是純靜態網站，不需要安裝 npm 套件，也不需要 build。直接用瀏覽器開啟 HTML 檔即可：

- 3D 地球版：`index.html`
- 平面地圖版：`flat/index.html`

也可以使用 `file://` URL，例如：

- `file:///path/to/wwii-3d-history/index.html`
- `file:///path/to/wwii-3d-history/flat/index.html`

若瀏覽器或安全設定擋住 CDN module 載入，再改用本機 HTTP server 作為備用方式：

```bash
python3 -m http.server 4173
```

然後打開 `http://localhost:4173/` 或 `http://localhost:4173/flat/`。

## 部署

GitHub Pages 設定為從 `main` branch 的 repository root 部署。推送到 `main` 後，GitHub Pages 會自動重新 build 並發布。

## 維護注意

- 3D 版和平面版目前各自是完整 HTML 檔，沒有共用 build pipeline。
- 3D 版的球面底圖由 canvas 產生後貼到 `THREE.SphereGeometry`。`SphereGeometry` 的 UV 經度基準和 `geoToGlobe()` 的球面座標基準差 90 度，因此 `createGlobeTexture()` 裡有 `texture.offset.x = 0.25` 用來對齊底圖與城市/軍隊座標。
- 兩個版本都從 CDN 載入 Three.js：`https://unpkg.com/three@0.164.1/build/three.module.js`。
- 瀏覽器需要支援 WebGL；若畫面只看到 UI 沒有戰場，優先檢查 WebGL 是否可用與 CDN 是否載入成功。

## License

MIT License. See [LICENSE](LICENSE).
