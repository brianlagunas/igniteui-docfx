---
title: Banner コンポーネント
_description: Ignite UI for Angular Banner コンポーネントは、簡単に非侵入型メッセージをオプション操作と統合できます。
_keywords: Ignite UI for Angular, UI コントロール, Angular ウィジェット, web ウィジェット, UI ウィジェット, Angular, Native Angular コンポーネント スイート, Native Angular コントロール, Native Angular コンポーネント Library, Angular Banner コンポーネント, Angular Banner コントロール
_language: ja
---
## Banner

<p class="highlight">
Ignite UI for Angular Banner コンポーネントは、スナックバーより長い時間の表示でダイアログより控えめのメッセージを簡単に表示できます。Banner にカスタム アクション ボタンやアイコンの表示を設定できます。</p>
<div class="divider"></div>

### Banner デモ

<div class="sample-container loading" style="height: 400px">
    <iframe id="banner-sample-iframe" frameborder="0" seamless width="100%" height="100%" src="{environment:demosBaseUrl}/notifications/banner-sample-4" onload="onSampleIframeContentLoaded(this);"></iframe>
</div>
<div>
    <button data-localize="stackblitz" disabled class="stackblitz-btn" data-iframe-id="banner-sample-iframe" data-demos-base-url="{environment:demosBaseUrl}">stackblitz で表示</button>
</div>
<div class="divider--half"></div>

> [!NOTE]
> Ignite UI for Angular コンポーネントをプロジェクトに追加する前に、必要なすべての依存関係を構成し、プロジェクトのセットアップが正しく完了したことを確認してください。[インストール](https://jp.infragistics.com/products/ignite-ui-angular/getting-started#installation)のトピックで手順をご確認ください。

## 使用方法

Ignite UI for Angular Banner の使用は、はじめに **app.module.ts** ファイルに `IgxBannerModule` をインポートします。

```typescript
// app.module.ts

...
import { IgxBannerModule } from 'igniteui-angular';

@NgModule({
    ...
    imports: [..., IgxBannerModule],
    ...
})
export class AppModule {}
```
### ベーシック Banner

Banner コンポーネントを表示するには、[`open()`]({environment:angularApiUrl}/classes/igxbannercomponent.html#open) メソッドを呼び出してボタンクリックで呼び出します。Banner メッセージを構成するには、Banner コンテンツ内のテキストを渡します。指定した Banner 領域にテキストが表示され、表示時にBannerはデフォルト テンプレートを使用します。

```html
<!--banner.component.html-->

<igx-banner #connectionBanner>
    You are currently offline.
</igx-banner>
...
<button igxButton="raised" (click)="connectionBanner.toggle()">Toggle Banner</button>
```

Bannerは、要素がページ テンプレートに挿入された場所にその他すべてのコンテンツを移動して表示されます。Bannerは、閉じるための最小限のユーザー操作 (1-2 クリックなど) を要求する非侵入型コンテンツ表示します。

#### ベーシック Banner デモ

<div class="sample-container loading" style="height: 530px">
    <iframe id="banner-sample-1-iframe" frameborder="0" seamless="" width="100%" height="100%" data-src="{environment:demosBaseUrl}/notifications/banner-sample-1" class="lazyload"></iframe>
</div>
<div>
    <button data-localize="stackblitz" disabled class="stackblitz-btn" data-iframe-id="banner-sample-1-iframe" data-demos-base-url="{environment:demosBaseUrl}">view on stackblitz</button>
</div>

### Banner のテンプレート化

[`IgxBannerComponent`]({environment:angularApiUrl}/classes/igxbannercomponent.html) は、マテリアル デザイン Banner ガイドラインにできるかぎり準拠しながら簡単にコンテンツをテンプレート化します。

#### Banner メッセージの変更

`igx-banner` タグに渡されるコンテンツを変更してBannerに表示されるメッセージを変更できます。以下は、’Connection' Bannerのコンテンツを変更してより多くの情報を提供します。

```html
    <!--banner.component.html-->
    <igx-banner #connectionBanner>
        You have lost connection to the internet. This app is offline.
    </igx-banner>
    ...
    <button igxButton="raised" (click)="connectionBanner.toggle()">Toggle Banner</button>
```

#### アイコンの追加

Banner コンテンツに [`igx-icon`](icon.md) を渡すことができ、常に Banner メッセージの最初に配置されます。

> [!NOTE]
> 複数の `igx-icon` 要素が Banner の直接の子孫として挿入される場合、Banner はそれらすべてを最初に配置しようとします。`igx-icon` は 1 つのみ、直接渡すことに注意してください。Banner メッセージのアイコンを使用する場合、`span` タグでラップしてください。

`Igx-icon` を Banner に渡す場合、`igx-banner` のコンテンツに挿入してください。

```html
    <!--banner.component.html-->
    <igx-banner #connectionBanner>
        <igx-icon>signal_wifi_off</igx-icon>
        You have lost connection to the internet. This app is offline.
    </igx-banner>
    ...
```

#### カスタム Banner ボタンの追加

`IgxBannerModule` は、Banner ボタンをテンプレート化するためのディレクティブ ([`IgxBannerActionsDirective`]({environment:angularApiUrl}/classes/igxbanneractionsdirective.html).) を公開します。このディレクティブを使用してデフォルト Banner ボタン (`Dismiss`) をオーバーライドし、ユーザー定義のカスタム操作を追加します。ほとんどのボタン インタラクションは Banner を閉じることであるため、`click` ハンドラーでBanner の `close()` メソッドを呼び出してください。

> [!NOTE]
> Google の [`マテリアル デザイン` ガイドライン](https://material.io/design/components/banners.html#anatomy) では、Banner に表示するボタンは 2 つまでです。`IgxBannerComponent` は、`igx-banner-actions` タグで 2 要素以上渡すことを明示的に制限**しません**が、マテリアル デザイン ガイドに従うことを推奨します。 

Connection Banner のテンプレート化は、`igx-banner-actions` セレクターを使用するカスタム アクション ハンドラーを渡すことができます。

```html
    <!--banner.component.html-->
    <igx-banner #connectionBanner>
        <igx-icon>signal_wifi_off</igx-icon>
        You have lost connection to the internet. This app is offline.
        <igx-banner-actions>
            <button igxButton igxRipple (click)="connectionBanner.close()">Continue Offline</button>
            <button igxButton igxRipple (click)="wifiState = true">Turn On Wifi</button>
        </igx-banner-actions>
    </igx-banner>
    ...
```

閉じるオプション (`'Continue Offline'`) は詳細なロジックを必要としないため、`connectionBanner.close()` のみの呼び出しが可能です。確認操作 (`‘Turn On Wifi’`) は追加のロジックを必要とするため、コンポーネントで定義します。


```typescript
// banner.component.ts
import { Component, OnInit, OnDestroy, ViewChild } from "@angular/core";
import { IgxBannerComponent } from 'igniteui-angular'
...
export class MyBannerComponent implements OnInit, OnDestroy {
    @ViewChild(IgxBannerComponent) public banner: IgxBannerComponent;
    public onNetworkStateChange = new Subject(); // Emits when WiFi state is changed
    private _wifiState = false;
    public get wifiState(): boolean {
        return this._wifiState;
    }
    public set wifiState(v: boolean) {
        this._wifiState = v;
        this.onNetworkStateChange.next();
    }
    ...
    public ngOnInit() { // subscribe to the event;
        this.banner.open();
        this.onNetworkStateChange.subscribe(() => this.refreshBanner()); // call change handler
    }

    public ngOnDestroy(): void { // unsubscribe
        this.onNetworkStateChange.complete();
    }
    ...
    // Define change handler
    public refreshBanner() {
        if (!this.wifiState) {
            this.banner.open();
        } else {
            if (!this.banner.collapsed) {
                this.banner.close();
            }
        }
    }
}
```

サブスクリプションが `wifiState` に対するすべての変更を発生するため、デモ navbar のバナーが WiFi アイコンを使用して切り替えができるようになります。

以下はテンプレート化したバナーのデモです。

#### デモのテンプレート化

<div class="sample-container loading" style="height: 530px">
    <iframe id="banner-sample-2-iframe" frameborder="0" seamless="" width="100%" height="100%" data-src="{environment:demosBaseUrl}/notifications/banner-sample-2" class="lazyload"></iframe>
</div>
<div>
    <button data-localize="stackblitz" disabled class="stackblitz-btn" data-iframe-id="banner-sample-2-iframe" data-demos-base-url="{environment:demosBaseUrl}">stackblitz で表示</button>
</div>

### カスタム アニメーションの適用

Banner コンポーネントは、[`animationSettings`]({environment:angularApiUrl}/classes/igxbannercomponent.html#animationsettings) にカスタム オープンの設定とアニメーションのクローズを許容する `Input` プロパティを公開します。カスタム アニメーションは、ユーザー定義または [`IgniteUI for Angular animation suite`]({environment:sassApiUrl}/index.html) から渡すことができます。Bannerで使用されるデフォルト アニメーションは、`growVerIn` が開始、`growVerOut` が終了です。

スライドインするためにBannerが使用するアニメーションを変更します。

```html
<!--banner.component.html-->
    <igx-banner #connectionBanner [animationSettings]="animationSettings">
        ...
    </igx-banner>
    ...
```

```typescript
// banner.component.ts
import { IgxBannerComponent, slideInLeft, slideOutRight } from 'igniteui-angular'
...
export class MyBannerComponent {
    ...
    public animationSettings = {
        openAnimation: slideInLeft,
        closeAnimation: slideOutRight
    }
    ...
}
```

#### アニメーション デモ

<div class="sample-container loading" style="height: 530px">
    <iframe id="banner-sample-3-iframe" frameborder="0" seamless="" width="100%" height="100%" data-src="{environment:demosBaseUrl}/notifications/banner-sample-3" class="lazyload"></iframe>
</div>
<div>
    <button data-localize="stackblitz" disabled class="stackblitz-btn" data-iframe-id="banner-sample-3-iframe" data-demos-base-url="{environment:demosBaseUrl}">view on stackblitz</button>
</div>

### イベントにバインド
Banner コンポーネントは状態の変更時にイベントを発生します。[`onOpening`]({environment:angularApiUrl}/classes/igxbannercomponent.html#onopening) と [`onOpened`]({environment:angularApiUrl}/classes/igxbannercomponent.html#onopened) が Banner が表示される (前と後に) ときに呼び出されます。一方、[`onClosing`]({environment:angularApiUrl}/classes/igxbannercomponent.html#onclosing) と [`onClosed`]({environment:angularApiUrl}/classes/igxbannercomponent.html#onclosed) はBannerが閉じるときにエミットされます。*Ing* イベント (`onOpening`, `onClosing`) はキャンセル可能です。 `ICancelEventArgs` インターフェイスを使用してオブジェクトは `cancel` プロパティを持ちます。`cancel` プロパティを true に設定します。対応するエンド操作とイベントはトリガーされません。たとえば、`onOpening` をキャンセルした場合、Banner の `open` メソッドは完了せずに Banner が表示されません。

発生したオブジェクトへバインドしたイベントをキャンセルするために `cancel` プロパティに `true` に設定します。

```html
<!--banner.component.html-->
    <igx-banner #connectionBanner (onOpening)="handleOpen($event)">
        ...
    </igx-banner>
```
```typescript
// banner.component.ts
...
export class MyBannerComponent {
    ...
    public handleOpen(event) {
        event.cancel = true;
    }
}
```
> [!NOTE]
> 上記が適用されるとオープニング イベントが常にキャンセルされるため、Banner が開くことはありません。

## API リファレンス

* [IgxBannerComponent]({environment:angularApiUrl}/classes/igxbannercomponent.html)
* [IgxBannerComponent Styles]({environment:sassApiUrl}/index.html#mixin-igx-banner)