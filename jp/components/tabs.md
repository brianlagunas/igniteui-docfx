---
title: Tabs コンポーネント - ネイティブ Angular | Ignite UI for Angular
_description: Ignite UI for Angular Tabs コンポーネントはタブを上側に配置し、複数のタブ項目がある場合にスクロールを許可します。
_keywords: Ignite UI for Angular, UI コントロール, Angular ウィジェット, web ウィジェット, UI ウィジェット, Angular, ネイティブ Angular コンポーネント スィート, ネイティブ Angular コンポーネント, ネイティブ Angular コントロール, ネイティブ Angular コンポーネント ライブラリ, Angular Tabs コンポーネント, Angular Tabs コントロール, Angular Tabs
_language: ja
---

## Tabs

Ignite UI for Angular [`igx-tabs`]({environment:angularApiUrl}/classes/igxtabscomponent.html) コンポーネントは、同様なデータ セットの体系化や切り替えに使用します。[`igx-tab-item`]({environment:angularApiUrl}/classes/igxtabitemcomponent.html) および [`igx-tabs-group`]({environment:angularApiUrl}/classes/igxtabsgroupcomponent.html) のラッパーとして機能し、データのコンテナーおよびタブ ヘッダーを表します。Tabs コンポーネントは、タブを上側に配置して複数のタブ項目がある場合にスクロールを許可します。

### Tabs デモ
<div class="sample-container loading" style="height: 250px; width: 600px;">
    <iframe id="tabs-sample-0" frameborder="0" seamless width="100%" height="100%" src="{environment:demosBaseUrl}/layouts/tabs-sample-3" onload="onSampleIframeContentLoaded(this);"></iframe>
</div>
<div>
    <button data-localize="stackblitz" disabled class="stackblitz-btn" data-iframe-id="tabs-sample-0" data-demos-base-url="{environment:demosBaseUrl}">StackBlitz で開く</button>
</div>
<div class="divider--half"></div>

> [!NOTE]
> Ignite UI for Angular コンポーネントをプロジェクトに追加する前に、すべての必要な依存関係を構成し、プロジェクトのセットアップが正しく完了したことを確認してください。「[**インストール**](https://jp.infragistics.com/products/ignite-ui-angular/getting-started#installation)」のトピックで手順を参照できます。

### 使用方法

Ignite UI for Angular Tabs コンポーネントを初期化する前に `IgxTabsModule` を **app.module.ts** ファイルにインポートします。

```typescript
// app.module.ts

...
import { IgxTabsModule } from 'igniteui-angular';

@NgModule({
    ...
    imports: [..., IgxTabsModule],
    ...
})
export class AppModule {}
```

[`label`]({environment:angularApiUrl}/classes/igxtabsgroupcomponent.html#label) およびコンテンツを持つ複数のタブ グループを指定します。

```html
<igx-tabs>
  <igx-tabs-group label="Tab 1">This is Tab 1 content.</igx-tabs-group>
  <igx-tabs-group label="Tab 2">This is Tab 2 content.</igx-tabs-group>
  <igx-tabs-group label="Tab 3">This is Tab 3 content.</igx-tabs-group>
  <igx-tabs-group label="Tab 4">This is Tab 4 content.</igx-tabs-group>
  <igx-tabs-group label="Tab 5">This is Tab 5 content.</igx-tabs-group>
</igx-tabs>
```

サンプルを構成した後、結果は以下のようになります。

<div class="sample-container loading" style="height: 200px; width: 600px; border: 1px solid gray;">
    <iframe id="tabs-sample-1-iframe" data-src='{environment:demosBaseUrl}/layouts/tabs-sample-1' width="100%" height="100%" seamless="" frameBorder="0" class="lazyload"></iframe>
</div>
<div>
<button data-localize="stackblitz" disabled class="stackblitz-btn" data-iframe-id="tabs-sample-1-iframe"
    data-demos-base-url="{environment:demosBaseUrl}">StackBlitz で開く</button>
</div>

<div class="divider"></div>

### Tabs タイプ
2 種類のタブがあります。[`fixed`]({environment:angularApiUrl}/enums/tabstype.html#fixed) または [`contentfit`]({environment:angularApiUrl}/enums/tabstype.html#contentfit) タブを選択するには、[`tabsType`]({environment:angularApiUrl}/classes/igxtabscomponent.html#tabstype) 入力を設定します。
- **contentfit タブ** (デフォルト): タブ ヘッダーの幅はコンテンツ (ラベル、アイコン、両方) に基づいて決定され、すべてのタブのパディングが等しくなります。
選択したタブのタイプに関係なく、タブ ヘッダーの幅は指定した最小幅および最大幅によって制限されます。
- **fixed タブ**: すべてのタブ ヘッダーは同じ幅を持ち、Tabs コンテナーに一致します。提供されたスペースが足りない場合、スクロール ボタンが表示されます。

```html
<div class="items-wrapper__item items-wrapper__item-small items-wrapper__item--blue">
  <h4 class="sample-title">CONTENT-FIT TABS</h4>
  <igx-navbar title="Contacts" actionButtonIcon="menu">
    <igx-icon>search</igx-icon>
    <igx-icon>more_vert</igx-icon>
  </igx-navbar>
  <igx-tabs>
    <igx-tabs-group label="HOME">Home content.</igx-tabs-group>
    <igx-tabs-group label="RECENT CONTACTS">Recent contacts list.</igx-tabs-group>
    <igx-tabs-group label="MORE INFORMATION ABOUT SELECTED CONTACT">More detailed contact information.</igx-tabs-group>
  </igx-tabs>
</div>

<div class="items-wrapper__item items-wrapper__item-small items-wrapper__item--blue">
  <h4 class="sample-title">FIXED TABS</h4>
  <igx-navbar title="Contacts" actionButtonIcon="menu">
    <igx-icon>search</igx-icon>
    <igx-icon>more_vert</igx-icon>
  </igx-navbar>
  <igx-tabs tabsType="fixed">
    <igx-tabs-group label="HOME">Home content.</igx-tabs-group>
    <igx-tabs-group label="RECENT CONTACTS">Recent contacts list.</igx-tabs-group>
    <igx-tabs-group label="MORE INFORMATION ABOUT SELECTED CONTACT">More detailed contact information.</igx-tabs-group>
  </igx-tabs>
</div>
```

<div class="sample-container loading" style="height: 450px; width: 800px;">
    <iframe id="tabs-sample-2-iframe" data-src='{environment:demosBaseUrl}/layouts/tabs-sample-2' width="100%" height="100%" seamless="" frameBorder="0" class="lazyload"></iframe>
</div>
<div>
<button data-localize="stackblitz" disabled class="stackblitz-btn" data-iframe-id="tabs-sample-2-iframe"
    data-demos-base-url="{environment:demosBaseUrl}">StackBlitz で開く</button>
</div>

<div class="divider"></div>

### タブのカスタマイズ

タブにアイコンを追加します。Tabs コントロールはマテリアル デザイン [**アイコン**](https://material.io/icons/)と互換性があるため、アプリケーションにアイコンを簡単に追加できます。

最初に Material+Icons をメイン アプリケーション フォルダーの 'styles.css' ファイルにインポートします。

```css
// styles.css

...
@import url('https://fonts.googleapis.com/icon?family=Material+Icons');
...
```

```html
<igx-tabs>
  <igx-tabs-group label="MY ALBUMS" icon="library_music">
    <div style="margin: 15px">
      <igx-card>
        <igx-card-header class="compact">
          <igx-avatar src="assets/images/card/avatars/alicia_keys.jpg" roundShape="true"></igx-avatar>
          <div class="igx-card-header__tgroup">
            <h3 class="igx-card-header__title--small">HERE</h3>
            <h5 class="igx-card-header__subtitle">by Alicia Keys</h5>
          </div>
        </igx-card-header>
        <igx-card-actions>
          <div class="igx-card-actions__bgroup">
            <button igxButton igxRipple>PLAY</button>
          </div>
        </igx-card-actions>
      </igx-card>
    </div>
  </igx-tabs-group>
  <igx-tabs-group label="FAVOURITES" icon="favorite">
    <div style="margin: 15px">
      <h5 class="igx-card-header__subtitle">Add your favourite songs here.</h5>
    </div>
  </igx-tabs-group>
  <igx-tabs-group label="INFO" icon="info">
    <div style="margin: 15px">
      <h5 class="igx-card-header__subtitle">"Here" is the sixth studio album by American singer and songwriter Alicia Keys.</h5>
    </div>
  </igx-tabs-group>
</igx-tabs>
```

サンプルを正しく構成した場合、タブは以下の例のようになります。

<div class="sample-container loading" style="height: 250px; width: 600px;">
    <iframe id="tabs-sample-3-iframe" data-src='{environment:demosBaseUrl}/layouts/tabs-sample-3' width="100%" height="100%" seamless="" frameBorder="0" class="lazyload"></iframe>
</div>
<div>
<button data-localize="stackblitz" disabled class="stackblitz-btn" data-iframe-id="tabs-sample-3-iframe"
    data-demos-base-url="{environment:demosBaseUrl}">StackBlitz で開く</button>
</div>

<div class="divider--half"></div>

タブのラベルおよびアイコンの変更を拡張する場合、各タブ ヘッダーでカスタム テンプレートを作成することもできます。

```html
<igx-tabs>
    <igx-tabs-group>
        <ng-template igxTab>
            <div>
                <!-- your custom tab content goes here -->
            </div>
        </ng-template>
        <h1>Tab content</h1>
    </igx-tabs-group>
</igx-tabs>
```

### Tabs と Routing の使用

以下は、Tabs コンポーネントの使用と基本的なルーティングの例です。<a href="https://angular.io/guide/router" target="_blank">Angular Routing と Navigation</a> について説明します。

#### igxTab、routerLink ディレクティブ、ルーティング アウトレットの使用

 **igxTab**で基本的なルーティングを実装するには、[`igxTab`]({environment:angularApiUrl}/classes/igxtabitemtemplatedirective.html) ディレクティブを使用して igx-tabs の項目ヘッダーを再テンプレート化し、`ng-template` に `router-outlet` でリンクを提供します。`ng-template` コンテンツは、デフォルト タブ ヘッダーのスタイルをオーバーライドすることに注意してください。

```html
<!-- tabs-sample-1.component.html -->
<igx-tabs #tabs1>
  <igx-tabs-group *ngFor="let routerLink of routerLinks">
    <ng-template igxTab>
      {{routerLink.label}}
      <a routerLink="{{routerLink.link}}"></a>
    </ng-template>
  </igx-tabs-group>
</igx-tabs>

<div>
  <router-outlet></router-outlet>
</div>
```

```typescript
// tabs-sample-1.component.ts
this.routerLinks = [
  {
    label: 'View 1',
    link: '/view1',
    index: 0
  }, 
  {
    label: 'View 2',
    link: '/view2',
    index: 1
  },
  {
    label: 'View 3',
    link: '/view3',
    index: 2
  },
];
```
URL パスを特定のコンポーネントにマップするために必要となるすべてのルート定義を宣言します。URL パスを含むすべての子コンポーネントは、メインルーティングモジュール app.routing.module.ts にインポートされる別のルーティング モジュールの tabs.routing.module.ts にリストされます。RouterModule.forChild メソッドでルーターを構成します。

```typescript
// tabs.routing.module.ts
const routes: Routes = [
    // simple links
    { path: 'view1', component: View1Component },
    { path: 'view2', component: View2Component },
    { path: 'view3', component: View3Component },
    { path: '', redirectTo: 'view1', pathMatch: 'full' }
];

@NgModule({
    imports: [
        RouterModule.forChild(routes)
    ],
    exports: [
        RouterModule
    ]
})
export class TabsRoutingModule { }
```
RouterModule.forRoot メソッドを使用してメイン ルーターを構成します。

```typescript
// app.routing.module.ts
const routes: Routes = [
  {
    path: 'tabs',
    component: TabsSample1Component
  },
  { path: '', redirectTo: '/tabs', pathMatch: 'full' }
];

@NgModule({
    imports: [
        RouterModule.forRoot(routes)
    ],
    exports: [
        RouterModule
    ]
})
export class AppRoutingModule { }
```

戻る/次へ ブラウザー ボタンを処理するために ngOnInit に以下のコードを追加し、[`IgxTabsGroupComponent`]({environment:angularApiUrl}/classes/igxtabsgroupcomponent.html) [`select`]({environment:angularApiUrl}/classes/igxtabsgroupcomponent.html#select) メソッドを使用して関連性のあるタブ グループをアクティブ化します。

```typescript
// tabs-sample-1.component.ts
constructor(private router: Router) {}

public ngOnInit() {
  // Initial view loaded
  this.router.navigate(['view1']);

  // Handle the back/forward browser buttons
  this._navigationEndSubscription = this.router.events.pipe(filter(event => event instanceof NavigationEnd)).subscribe((args) => {
  const index = this.routerLinks.indexOf(this.routerLinks.find(tab => tab.link === this.router.url));
  (this.tabs.groups.filter(item => item.index === index)[0] as IgxTabsGroupComponent).select();
  });
}
```

<div class="sample-container loading">
    <iframe id="tabs-sample-4-iframe" data-src='{environment:demosBaseUrl}/layouts/tabs-sample-4' seamless="" frameBorder="0" style="display: none" class="lazyload"></iframe>
</div>
<div>
<button data-localize="stackblitz" disabled class="stackblitz-btn" data-iframe-id="tabs-sample-4-iframe"
    data-demos-base-url="{environment:demosBaseUrl}">stackblitz で開く</button>
</div>

#### 他のルーター アウトレットを Tabs コンテンツに使用
コンテンツ内にビューを描画する場合は、名前付きルーター アウトレットを使用します。[`onTabItemSelected`]({environment:angularApiUrl}/classes/igxtabscomponent.html#ontabitemselected) イベント ハンドラーを実装して特定のビューへ移動、描画します。

```html
<!-- tabs-sample-1.component.html -->
<!-- router-outlet inside the tabs items content -->
<igx-tabs #tabs1 (onTabItemSelected)="navigate($event)">
  <igx-tabs-group label="Product1" name="product1">
    <router-outlet name="product1"></router-outlet>
  </igx-tabs-group>
  <igx-tabs-group label="Product2" name="product2">
    <router-outlet name="product2"></router-outlet>
  </igx-tabs-group>
  <igx-tabs-group label="Product3" name="product3">
    <router-outlet name="product3"></router-outlet>
  </igx-tabs-group>
</igx-tabs>
```

```typescript
// tabs-sample-1.component.ts
public navigate(eventArgs) {
    const selectedIndex = eventArgs.group.index;
    switch(selectedIndex) {
      case 0: {
        this.router.navigate(['/productDetails',
          {
            outlets:
            {
              product1: ['product1']
            }
          }
        ]);
        break;
    }
    case 1: {
      this.router.navigate(['/productDetails',
        {
          outlets:
          {
            product2: ['product2']
          }
        }
      ]);
      break;
    }
    case 2: {
      this.router.navigate(['/productDetails',
          {
            outlets:
            {
              product3: ['product3']
            }
          }
        ]);
        break;
      }
    }
  }
```
URL パスを特定のコンポーネントにマップするために必要となるすべてのルート定義を宣言します。

```typescript
// tabs.routing.module.ts
const routes: Routes = [
  {
    // children outlets
    path: 'productDetails',
    children: [
      { path: 'product1', component: View1Component, outlet: 'product1' },
      { path: 'product2', component: View2Component, outlet: 'product2' },
      { path: 'product3', component: View3Component, outlet: 'product3' },
      { path: '', redirectTo: 'product1', pathMatch: 'full' }
    ]
  },
  {
    path: '',
    redirectTo: '/productDetails',
    pathMatch: 'full'
  }
];
...
```

<div class="sample-container loading">
    <iframe id="tabs-sample-5-iframe" data-src='{environment:demosBaseUrl}/layouts/tabs-sample-5' seamless="" frameBorder="0" style="display: none" class="lazyload"></iframe>
</div>
<div>
<button data-localize="stackblitz" disabled class="stackblitz-btn" data-iframe-id="tabs-sample-5-iframe"
    data-demos-base-url="{environment:demosBaseUrl}">stackblitz で開く</button>
</div>

### API リファレンス
<div class="divider"></div>

* [IgxAvatarComponent]({environment:angularApiUrl}/classes/igxavatarcomponent.html)
* [IgxCardComponent]({environment:angularApiUrl}/classes/igxcardcomponent.html)
* [IgxIconComponent]({environment:angularApiUrl}/classes/igxiconcomponent.html)
* [IgxNavbarComponent]({environment:angularApiUrl}/classes/igxnavbarcomponent.html)
* [IgxTabsComponent]({environment:angularApiUrl}/classes/igxtabscomponent.html)
* [IgxTabsComponent Styles]({environment:sassApiUrl}/index.html#function-igx-tabs-theme)
* [IgxTabsGroupComponent]({environment:angularApiUrl}/classes/igxtabsgroupcomponent.html)
* [IgxTabItemComponent]({environment:angularApiUrl}/classes/igxtabitemcomponent.html)

### その他のリソース

<div class="divider--half"></div>
コミュニティに参加して新しいアイデアをご提案ください。

* [Ignite UI for Angular **フォーラム** (英語)](https://www.infragistics.com/community/forums/f/ignite-ui-for-angular)
* [Ignite UI for Angular **GitHub** (英語)](https://github.com/IgniteUI/igniteui-angular)
