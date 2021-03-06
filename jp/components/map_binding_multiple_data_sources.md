---
title: マップ | データ可視化ツール | Ignite UI for Angular | 複数シリーズ | Infragistics
_description: マップを使用すると、ビュー モデルからの地理的位置を含むデータ、またはシェープ ファイルから地理的画像マップにロードされた地理空間データを表示できます。
_keywords: map, Ignite UI for Angular, infragistics
_language: ja
---

## 複数データ ソースのバインド

`XamGeographicMap` では、カスタムデータソースを地理空間データとオーバーレイするために複数の地理的シリーズオブジェクトを追加できます。たとえば、空港の地理的位置をプロットするための `GeographicSymbolSeries`、空港間のフライトをプロットするための `GeographicPolylineSeries`、主要な地理座標のグリッド線をプロットするための 2nd `GeographicPolylineSeries` などです。

### デモ

<div class="sample-container" style="height: 400px">
    <iframe id="geo-map-binding-multiple-sources-iframe" src='{environment:demosBaseUrl}/maps/geo-map-binding-multiple-sources' width="100%" height="100%" seamless frameBorder="0" onload="onSampleIframeContentLoaded(this);"></iframe>
</div>
<div>
    <button data-localize="stackblitz" disabled class="stackblitz-btn"   data-iframe-id="geo-map-binding-multiple-sources-iframe" data-demos-base-url="{environment:demosBaseUrl}">StackBlitz で表示
    </button>
</div>

<div class="divider--half"></div>

このトピックでは、次の地理空間データをプロットする複数の地理的シリーズを表示するための手順を説明します。

`GeographicSymbolSeries` – 主要空港の場所を表示します。
`GeographicPolylineSeries` – 空港間のフライトを表示します。
`GeographicPolylineSeries` – 主座標のグリッド線を表示します。

希望のデータをプロットするために、これまたは他の組み合わせで地理的シリーズを使用できます。

### データ ソースの作成

`XamGeographicMap` に表示するすべての地理的シリーズのデータ​​ソースを作成します。たとえば、[WorldConnections](map_resources_world_connections.md) スクリプトを使用できます。

### フライトのオーバーレイ

主要空港間のフライト接続を含む最初の `GeographicPolylineSeries` オブジェクトを作成し、それを `XamGeographicMap` の `IgxSeriesComponent` コレクションに追加します。

### グリッド線のオーバーレイ

地理グリッド線を使用して2番目の `GeographicPolylineSeries` オブジェクトを作成し、それを XamGeographicMap の Series コレクションに追加します。

地理的なグリッド線を使用して `GeographicSymbolSeries` オブジェクトを作成し、それを地理的な `XamGeographicMap` の `IgxSeriesComponent` コレクションに追加します。
