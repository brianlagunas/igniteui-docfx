---
title: Snackbar コンポーネント
_description: Ignite UI for Angular Snackbar を使用すると、単一行メッセージをモバイルおよびデスクトップ アプリケーションに含みます。
_keywords: Ignite UI for Angular, UI コントロール, Angular ウィジェット, web ウィジェット, UI ウィジェット, Angular, ネイティブ Angular コンポーネント スィート, ネイティブ Angular コントロール, ネイティブ Angular コンポーネント ライブラリ, Angular Snackbar コンポーネント, Angular Snackbar コントロール
_language: ja
---

## Snackbar

<p class="highlight">Ignite UI for Angular Snack Bar コンポーネントは単一行のメッセージで操作のフィードバックを提供します。元に戻すなどの操作へのリンクを追加できます。Snack Bar メッセージがその他の画面要素の上に表示されます。モバイル デバイス画面の下部に配置され、より大きいデバイス画面の左下に配置されます。</p>
<div class="divider"></div>

### Snackbar デモ

<div class="sample-container loading" style="height: 350px">
    <iframe id="snackbar-sample-iframe" frameborder="0" seamless width="100%" height="100%" src="{environment:demosBaseUrl}/notifications/snackbar-sample-4" onload="onSampleIframeContentLoaded(this);"></iframe>
</div>
<div>
    <button data-localize="stackblitz" disabled class="stackblitz-btn" data-iframe-id="snackbar-sample-iframe" data-demos-base-url="{environment:demosBaseUrl}">StackBlitz で表示</button>
</div>
<div class="divider--half"></div>

> [!NOTE]
> Ignite UI for Angular コンポーネントをプロジェクトに追加する前に、すべての必要な依存関係を構成し、プロジェクトのセットアップが正しく完了したことを確認してください。「[**インストール**](https://jp.infragistics.com/products/ignite-ui-angular/getting-started#installation)」のトピックで手順を参照できます。

### 使用方法

Ignite UI for Angular Snack Bar を初期化する前に、`IgxSnackbarModule` を **app.module.ts** ファイルにインポートします。

```typescript
// app.module.ts

...
import { IgxSnackbarModule } from 'igniteui-angular';

@NgModule({
    ...
    imports: [..., IgxSnackbarModule],
    ...
})
export class AppModule {}
```

#### Snackbar の表示

Snackbar コンポーネントを表示するには、ボタン クリックで [`show()`]({environment:angularApiUrl}/classes/igxsnackbarcomponent.html#show) メソッドを呼び出します。

```html
<!--sample.component.html-->

<button igxButton="raised" (click)="snackbar.show()">Delete Message</button>
<div>
    <igx-snackbar #snackbar>Message deleted</igx-snackbar>
</div>
```

サンプルが正しく構成された場合、ボタン クリック時にテキスト メッセージを表示する Snackbar が表示されます。

<div class="sample-container loading" style="height: 170px">
    <iframe id="snackbar-sample-iframe" frameborder="0" seamless="" width="100%" height="100%" data-src="{environment:demosBaseUrl}/notifications/snackbar-sample-1" class="lazyload"></iframe>
</div>

#### 非表示/自動的に隠す

開いた後は、[`displayTime`]({environment:angularApiUrl}/classes/igxsnackbarcomponent.html#displaytime) 入力によって指定した期間遅延後に非表示になります。デフォルト値は 4000 ミリ秒です。この動作はデフォルトで有効ですが、[`autoHide`]({environment:angularApiUrl}/classes/igxsnackbarcomponent.html#autohide) を **false** に設定して変更できます。この場合、Snackbar は非表示になりません。Snackbar の [`hide()`]({environment:angularApiUrl}/classes/igxsnackbarcomponent.html#hide) メソッドを使用して、コードでコンポーネントを閉じることができます。

```html
<!--sample.component.html-->

<button igxButton="raised" (click)="snackbar.show()">Send message</button>
<div>
  <igx-snackbar #snackbar [autoHide]="false" actionText="CLOSE" (onAction)="close(snackbar)">Message sent</igx-snackbar>
</div>
```

```typescript
// sample.component.ts

public close(element) {
    element.hide();
}
```

サンプルを正しく構成した後、ボタンをクリックするとメッセージおよびアクション ボタンを含む Snackbar が表示されます。自動的に隠す機能が無効で、[CLOSE] ボタンのクリックで Snackbar が非表示になります。

<div class="sample-container loading" style="height: 170px">
    <iframe id="snackbar-sample-iframe" frameborder="0" seamless="" width="100%" height="100%" data-src="{environment:demosBaseUrl}/notifications/snackbar-sample-2" class="lazyload"></iframe>
</div>

#### 表示期間

[`displayTime`]({environment:angularApiUrl}/classes/igxsnackbarcomponent.html#displaytime) でミリ秒間隔に設定し、Snackbar コンポーネントが表示される期間を構成します。

```html
<!--sample.component.html-->

<button igxButton="raised" (click)="snackbar.show()">Send message</button>
<div>
  <igx-snackbar #snackbar displayTime="1000">Message sent</igx-snackbar>
</div>
```

サンプルが正しく構成された場合、Snackbar が自動ですばやく非表示になります。

<div class="sample-container loading" style="height: 170px">
    <iframe id="snackbar-sample-iframe" frameborder="0" seamless="" width="100%" height="100%" data-src="{environment:demosBaseUrl}/notifications/snackbar-sample-3" class="lazyload"></iframe>
</div>

#### Snackbar のカスタマイズ
Snackbar の内容をカスタマイズして、メッセージやボタンよりも複雑な要素を表示することもできます。たとえば、ファイルの読み込み中にスナックバーを表示したい場合は、読み込みアニメーションをそのコンテンツに追加することができます。

```html
<!--sample.component.html-->
<button igxButton="raised" (click)="snackbar.show()">Load file</button>
<div>
  <igx-snackbar #snackbar displayTime="5000">File loading
    <svg id="dots" height="20px">
        <g id="dots" fill="#FFFFFF">
            <circle id="dot1" cx="5" cy="18" r="2"></circle>
            <circle id="dot2" cx="15" cy="18" r="2"></circle>
            <circle id="dot3" cx="25" cy="18" r="2"></circle>
        </g>
    </svg>
  </igx-snackbar>
</div>
```

```scss
//sample.component.scss
#dots #dot1 {
    animation: load 1s infinite;
}

#dots #dot2 {
    animation: load 1s infinite;
    animation-delay: 0.2s;
}

#dots #dot3 {
    animation: load 1s infinite;
    animation-delay: 0.4s;
}

@keyframes load {
    0% {
      opacity: 0;
    }
    50% {
      opacity: 1;
    }
    100% {
      opacity: 0;
    }
}
```

結果としてメッセージと 3 つのローディング ドットがスナックバーに表示されます。

<div class="sample-container loading" style="height: 170px">
    <iframe id="snackbar-sample-iframe-1" frameborder="0" seamless="" width="100%" height="100%" data-src="{environment:demosBaseUrl}/notifications/snackbar-sample-5" class="lazyload"></iframe>
</div>

<div>
    <button data-localize="stackblitz" disabled class="stackblitz-btn" data-iframe-id="snackbar-sample-iframe-1" data-demos-base-url="{environment:demosBaseUrl}">StackBlitz で表示</button>

</div>

#### リストの Snackbar

Snackbar の主な機能を説明しました。次の例はより複雑なサンプルにコンポーネントを追加します。通知およびアクションの元に戻す機能を提供する Snackbar を作成します。

削除可能な連絡先のリストを作成します。項目を削除後、メッセージおよびアクションを元に戻すボタンを含む Snackbar が表示されます。

```html
<!--sample.component.html-->

<igx-list>
    <igx-list-item [isHeader]="true">Contacts</igx-list-item>

	<igx-list-item igxRipple="pink" igxRippleTarget=".igx-list__item" *ngFor="let item of navItems">
        <div class="item-container">
            <div class="contact">
                <igx-avatar [src]="item.avatar" roundShape="true"></igx-avatar>
                <div class="contact__info">
                    <span class="name">{{item.text}}</span>
                </div>
            </div>
            <span igxButton="icon" igxRipple igxRippleCentered="true" (click)="delete(item)">
                <igx-icon color="#ff5252">delete</igx-icon>
            </span>
		</div>

    </igx-list-item>

    <igx-snackbar actionText="Undo" (onAction)="restore()">Contact deleted</igx-snackbar>
</igx-list>
```

```typescript
//sample.component.ts

import { Component, OnInit, ViewChild } from "@angular/core";
import { IgxSnackbarComponent } from 'igniteui-angular';

...
@ViewChild(IgxSnackbarComponent)
public snackbar: IgxSnackbarComponent;
public navItems: any[];
public deletedItems = [];

constructor() { }

public ngOnInit() {
    this.navItems = [{
        avatar: "assets/images/avatar/2.jpg",
        text: "Richard Mahoney"
    },
    {
        avatar: "assets/images/avatar/4.jpg",
        text: "Lisa Landers"
    },
    {
        avatar: "assets/images/avatar/14.jpg",
        text: "Marianne Taylor"
    },
    {
        avatar: "assets/images/avatar/17.jpg",
        text: "Ward Riley"
    }];
  }

public delete(item) {
    this.deletedItems.push([item, this.navItems.indexOf(item)]);
    this.navItems.splice(this.navItems.indexOf(item), 1);
    this.snackbar.show();
}

public restore() {
    const [item, index] = this.deletedItems.pop();
    this.navItems.splice(index, 0, item);
    this.snackbar.hide();
}

```

<div class="sample-container loading" style="height: 350px">
    <iframe id="snackbar-sample-iframe" frameborder="0" seamless="" width="100%" height="100%" data-src="{environment:demosBaseUrl}/notifications/snackbar-sample-4" class="lazyload"></iframe>
</div>

<div>
    <button data-localize="stackblitz" disabled class="stackblitz-btn" data-iframe-id="snackbar-sample-iframe" data-demos-base-url="{environment:demosBaseUrl}">StackBlitz で表示</button>
</div>

<div class="divider--half"></div>

### API リファレンス

このトピックでは、[`IgxSnackbarComponent`]({environment:angularApiUrl}/classes/igxsnackbarcomponent.html) を使用と構成方法を説明しました。API の詳細については以下のリンク先を参照してください。

* [`IgxSnackbarComponent`]({environment:angularApiUrl}/classes/igxsnackbarcomponent.html)

スタイル:

* [`IgxSnackbarComponent Styles`]({environment:sassApiUrl}/index.html#function-igx-snackbar-theme)

### その他のリソース

<div class="divider--half"></div>

コミュニティに参加して新しいアイデアをご提案ください。
* [Ignite UI for Angular **フォーラム** (英語)](https://www.infragistics.com/community/forums/f/ignite-ui-for-angular)
* [Ignite UI for Angular **GitHub** (英語)](https://github.com/IgniteUI/igniteui-angular)