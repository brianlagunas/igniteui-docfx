﻿---
title: Dialog Window コンポーネント
_description: Ignite UI for Angular Dialog Window コンポーネントを使用すると、情報ダイアログまたはデータ変換ウィンドウを作成し、リアルタイムで情報を表示して管理できます。
_keywords: Ignite UI for Angular, UI コントロール, Angular ウィジェット, web ウィジェット, UI ウィジェット, Angular, ネイティブ Angular コンポーネント スィート, ネイティブ Angular コントロール, ネイティブ Angular コンポーネント ライブラリ, Angular Dialog Window コンポーネント, Angular Dialog Window コントロール
_language: ja
---

## Dialog Window
<p class="highlight">Ignite UI for Angular Dialog Window コンポーネントをメッセージを表示するか、入力フォームを表示するために使用します。コンポーネントはアプリケーション コンテンツの中央上にダイアログ ウィンドウを開きます。キャンセル可能な標準の警告メッセージを提供できます。</p>
<div class="divider"></div>

### Dialog デモ
<div class="sample-container loading" style="height:300px">
    <iframe id="dialog-sample-iframe" src='{environment:demosBaseUrl}/interactions/dialog' width="100%" height="100%" seamless frameBorder="0" onload="onSampleIframeContentLoaded(this);"></iframe>
</div>
<div>
    <button data-localize="stackblitz" disabled class="stackblitz-btn" data-iframe-id="dialog-sample-iframe" data-demos-base-url="{environment:demosBaseUrl}">StackBlitz で表示</button>
</div>
<div class="divider--half"></div>

### 使用方法

Ignite UI for Angular Dialog Window を初期化する前に、[**IgxDialogModule**]({environment:angularApiUrl}/classes/igxsdialogmodule.html) を **app.module.ts** ファイルにインポートします。

```typescript
// app.module.ts

...
import { IgxDialogModule } from 'igniteui-angular';

@NgModule({
    ...
    imports: [..., IgxDialogModule],
    ...
})
export class AppModule {}
```
<div class="divider--half"></div>

#### 警告

通知を追加するには、メール コンポーネントのテンプレートで、以下のコードを追加すると通知ダイアログが作成されます。[`title`]({environment:angularApiUrl}/classes/igxdialogcomponent.html#title)、 [`message`]({environment:angularApiUrl}/classes/igxdialogcomponent.html#message)、[`leftButtonLabel`]({environment:angularApiUrl}/classes/igxdialogcomponent.html#leftbuttonlabel) を設定し、[`onLeftButtonSelect`]({environment:angularApiUrl}/classes/igxdialogcomponent.html#onleftbuttonselect) イベントを処理します。

```html
<!--email.component.html-->

<igx-dialog #alert
    title="Notification"
    message="Your email has been sent successfully!"
    leftButtonLabel="OK"
	(onLeftButtonSelect)="alert.close()">
</igx-dialog>
```

<div class="sample-container loading" style="height:250px">
    <iframe id="dialog-sample-1-iframe" data-src='{environment:demosBaseUrl}/interactions/dialog-sample-1' width="100%" height="100%" seamless="" frameBorder="0" class="lazyload"></iframe>
</div>
<div>
    <button data-localize="stackblitz" disabled class="stackblitz-btn" data-iframe-id="dialog-sample-1-iframe" data-demos-base-url="{environment:demosBaseUrl}">StackBlitz で表示</button>
</div>
<div class="divider--half"></div>

#### 標準ダイアログ

規格のダイアログを追加するには、ファイル マネージャー コンポーネントのテンプレートで、以下のコードを追加すると規格のダイアログが作成されます。[`title`]({environment:angularApiUrl}/classes/igxdialogcomponent.html#title)、 [`message`]({environment:angularApiUrl}/classes/igxdialogcomponent.html#message)、[`leftButtonLabel`]({environment:angularApiUrl}/classes/igxdialogcomponent.html#leftbuttonlabel)、[`rightButtonLabel`]({environment:angularApiUrl}/classes/igxdialogcomponent.html#rightbuttonlabel) を設定し、[`onLeftButtonSelect`]({environment:angularApiUrl}/classes/igxdialogcomponent.html#onleftbuttonselect) および [`onRightButtonSelect`]({environment:angularApiUrl}/classes/igxdialogcomponent.html#onrightbuttonselect) イベントを処理します。

```html
<!--file-manager.component.html-->

<igx-dialog #dialog title="Confirmation"
    leftButtonLabel="Cancel"
    (onLeftButtonSelect)="dialog.close()"
    rightButtonLabel="OK"
    (onRightButtonSelect)="onDialogOKSelected($event)"
	message="Are you sure you want to delete the Microsoft_Annual_Report_2015.pdf and Microsoft_Annual_Report_2015.pdf files?">
</igx-dialog>
```

<div class="sample-container loading" style="height:250px">
    <iframe id="dialog-sample-2-iframe" data-src='{environment:demosBaseUrl}/interactions/dialog-sample-2' width="100%" height="100%" seamless="" frameBorder="0" class="lazyload"></iframe>
</div>
<div>
    <button data-localize="stackblitz" disabled class="stackblitz-btn" data-iframe-id="dialog-sample-2-iframe" data-demos-base-url="{environment:demosBaseUrl}">StackBlitz で表示</button>
</div>
<div class="divider--half"></div>

#### カスタム ダイアログ

カスタム ダイアログを追加するには、サインイン コンポーネントのテンプレートで、以下のコードを追加するとカスタム ダイアログが作成されます。[`title`]({environment:angularApiUrl}/classes/igxdialogcomponent.html#title)、[`leftButtonLabel`]({environment:angularApiUrl}/classes/igxdialogcomponent.html#leftbuttonlabel)、[`rightButtonLabel`]({environment:angularApiUrl}/classes/igxdialogcomponent.html#rightbuttonlabel)、[`closeOnOutsideSelect`]({environment:angularApiUrl}/classes/igxdialogcomponent.html#closeonoutsideselect) を設定し、[`onLeftButtonSelect`]({environment:angularApiUrl}/classes/igxdialogcomponent.html#onleftbuttonselect) および [`onRightButtonSelect`]({environment:angularApiUrl}/classes/igxdialogcomponent.html#onrightbuttonselect) イベントを処理します。
また、[**igxLabel**](input_group.md) および [**igxInput**](input_group.md) ディレクティブでデコレートされるラベルおよび入力の 2 つのグループを追加できます。

```html
<!--sign-in.component.html-->

<igx-dialog #form title="Sign In"
    leftButtonLabel="Cancel"
    (onLeftButtonSelect)="form.close()"
    (onRightButtonSelect)="signIn($event)"
    rightButtonLabel="Sign In"
    [closeOnOutsideSelect]="true">
    <form class="signInForm">
        <igx-input-group>
            <igx-prefix>
                <igx-icon>person</igx-icon>
            </igx-prefix>
            <label igxLabel for="username">Username</label>
            <input igxInput id="username" type="text" />
        </igx-input-group>
        <igx-input-group>
            <igx-prefix>
                <igx-icon>lock</igx-icon>
            </igx-prefix>
            <label igxLabel>Password</label>
            <input igxInput id="password" type="password" />
        </igx-input-group>
    </form>
</igx-dialog>
```

<div class="sample-container loading" style="height:300px">
    <iframe id="dialog-sample-3-iframe" data-src='{environment:demosBaseUrl}/interactions/dialog-sample-3' width="100%" height="100%" seamless="" frameBorder="0" class="lazyload"></iframe>
</div>
<div>
    <button data-localize="stackblitz" disabled class="stackblitz-btn" data-iframe-id="dialog-sample-3-iframe" data-demos-base-url="{environment:demosBaseUrl}">StackBlitz で表示</button>
</div>
<div class="divider--half"></div>

#### タイトルとアクションのカスタマイズ

ダイアログ タイトル領域は `igxDialogTitle` ディレクティブまたは ` igx-dialog-title` セレクターを使ってカスタマイズできます。また、アクション領域は `igxDialogActions` ディレクティブまたは ` igx-dialog-actions` セレクターを使ってカスタマイズできます。

```html
<!-- dialog.component.html -->

<igx-dialog #dialog [closeOnOutsideSelect]="true" message="This will create a new social media account.">
    <igx-dialog-title>
        <div class="dialog-container">
            <igx-icon>account_box</igx-icon>
            <div class="dialog-title">Create a new account?</div>
        </div>
    </igx-dialog-title>
    <div igxDialogActions class="dialog-container dialog-actions">
        <button igxButton (click)="dialog.close()">CREATE</button>
        <button igxButton (click)="dialog.close()">CANCEL</button>
    </div>
</igx-dialog>
```

<div class="sample-container loading" style="height:300px">
    <iframe id="custom-dialog-sample-iframe" data-src='{environment:demosBaseUrl}/interactions/custom-dialog-sample' width="100%" height="100%" seamless="" frameBorder="0" class="lazyload"></iframe>
</div>
<div>
    <button data-localize="stackblitz" disabled class="stackblitz-btn" data-iframe-id="custom-dialog-sample-iframe" data-demos-base-url="{environment:demosBaseUrl}">stackblitz で表示</button>
</div>
<div class="divider--half"></div>

### API まとめ
<div class="divider--half"></div>

* [IgxDialogComponent]({environment:angularApiUrl}/classes/igxdialogcomponent.html)
* [IgxDialogComponent Styles]({environment:sassApiUrl}/index.html#function-igx-dialog-theme)
* [IgxOverlay]({environment:angularApiUrl}/interfaces/overlaysettings.html)
* [IgxOverlay Styles]({environment:sassApiUrl}/index.html#function-igx-overlay-theme)

### 追加のリソース

<div class="divider--half"></div>
コミュニティに参加して新しいアイデアをご提案ください。
* [Ignite UI for Angular **フォーラム** (英語)](https://www.infragistics.com/community/forums/f/ignite-ui-for-angular)
* [Ignite UI for Angular **GitHub** (英語)](https://github.com/IgniteUI/igniteui-angular)