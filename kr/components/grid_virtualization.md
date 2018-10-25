﻿---
title: 가상화 지시문 - 네이티브 Angular | Ignite UI for Angular 
_description: Ignite UI for Angular 가상화 지시문은 대용량 데이터 세트를 처리할 때 그리드의 속도와 성능을 뒷받침하는 핵심 메커닉으로 가상 렌더링 메커니즘을 통해 메모리에 있는 DOM 객체 수를 수정하여 쉽게 스크롤할 수 있습니다. 
_keywords: Ignite UI for Angular, UI 컨트롤, Angular 위젯, 웹 위젯, UI 위젯, Angular, 네이티브 Angular 컴포넌트 세트, 네이티브 Angular 컨트롤, 네이티브 Angular 컴포넌트 라이브러리, 네이티브 Angular 컴포넌트, Angular 데이터 그리드 컴포넌트, Angular 데이터 그리드 컨트롤, Angular 그리드 컴포넌트, Angular 그리드 컨트롤, Angular 고성능 그리드, Angular 가상화 지시문, 가상화, 퍼포먼스
_language: kr
---

### 그리드 가상화 및 성능

Ignite UI for Angular에서 `igxGrid` 컨트롤은 `igxForOf` 지시문을 사용하고 내용을 세로 및 가로로 가상화합니다.

#### 데모

<div class="sample-container loading" style="height:550px">
    <iframe id="grid-sample-2-iframe" src='{environment:demosBaseUrl}/grid-sample-2' width="100%" height="100%" seamless frameBorder="0" onload="onSampleIframeContentLoaded(this);"></iframe>
</div>
<br/>
<div>
<button data-localize="stackblitz" disabled class="stackblitz-btn" data-iframe-id="grid-sample-2-iframe" data-demos-base-url="{environment:demosBaseUrl}">view on stackblitz</button>
</div>

### 가상화 활성화

`igxForOf` 지시문을 사용함으로써 데이터 그리드는 현재 보기 포트에 표시된 내용만 렌더링하고 사용자가 데이터를 가로/세로로 스크롤하는 동안 표시된 데이터를 스와핑하여 DOM 렌더링 및 메모리 사용을 최적화합니다. `igxGrid`의 `width` 및 `height`의 기본값은 `100%`이며, 표시되는 내용이 사용 가능한 공간에 맞지 않고 스크롤바가 세로 또는 가로로 필요한 경우에 가상화가 활성화됩니다. 그러나, 그리드의 `width` 및/또는 `height`를 명시적으로 `null`로 설정할 수 있는데 즉 관련된 규격이 내부 항목의 전체 크기에 근거하여 결정됩니다. 그러면 스크롤바가 표시되지 않고 모든 항목이 해당 규격(`width`가 `null`인 경우에는 열, height가 `null`인 경우에는 행)이 렌더링됩니다.

데이터의 크기는 다음에 따라 결정됩니다:

*   수직(행) 가상화의 행 높이입니다. 이것은 `rowHeight` 옵션에 의해 결정되며 기본적으로 50(px)입니다.
*   수평(열) 가상화의 개별 열 너비(픽셀 단위)입니다. 각 열 컴포넌트에 대해 명시적으로 폭을 설정하거나 명시적으로 폭이 설정되지 않은 모든 열에 적용되는 그리드의 `columnWidth` 옵션을 설정할 수 있습니다.

규격을 설정하지 않은 채로 그리드에 기본 동작을 적용하면 대부분의 경우 원하는 레이아웃이 생성됩니다. 열 너비의 경우에는 열 수, 너비가 설정된 열 및 그리드 컨테이너의 계산된 너비에 따라 결정됩니다. 그리드는 할당하려는 폭이 136(px) 미만인 경우 이외에는 사용 가능한 공간 안에 모든 열을 맞추려고 합니다. 이 경우, 할당되지 않은 너비를 가진 열은 136(px)의 최소 너비로 설정되고 가로 스크롤바가 표시됩니다. 그리드는 가로 방향으로 가상화됩니다.

명시적으로 열 너비를 백분율(%)로 설정하는 경우, 대부분의 경우 가로 스크롤바가 없는 가로 방향으로 가상화되지 않는 그리드를 작성합니다.

### 원격 가상화

`igxGrid` supports the scenario in which the data chunks are requested from a remote service, exposing the behavior implemented in the `igxForOf` directive it uses internally.

### 그리드 원격 가상화 데모

<div class="sample-container loading" style="height:550px">
    <iframe id="grid-sample-4-iframe" src='{environment:demosBaseUrl}/grid-sample-4' width="100%" height="100%" seamless frameBorder="0" onload="onSampleIframeContentLoaded(this);"></iframe>
</div>
<br/>
<div>
<button data-localize="stackblitz" disabled class="stackblitz-btn" data-iframe-id="grid-sample-4-iframe" data-demos-base-url="{environment:demosBaseUrl}">view on stackblitz</button>
</div>

이 기능을 사용하려면 얻은 인수를 기반으로 적절한 요청을 하기 위해 `onDataPreLoad` 출력에 서브스크라이브하고 서비스에서 제공하는 해당 정보와 공개 `igxGrid` 속성 `totalItemCount`를 설정해야 합니다. 

```html
<igx-grid #grid [data]="remoteData | async" [height]="'500px'" [width]="'100%'" [autoGenerate]='false' (onDataPreLoad)="processData(false)"
    (onSortingDone)="processData(true)">
    <igx-column [field]="'ProductID'" [sortable]="true"></igx-column>
    <igx-column [field]="'ProductName'" [sortable]="true"></igx-column>
    <igx-column [field]="'UnitPrice'" [dataType]="'number'" [formatter]="formatCurrency" [sortable]="true"></igx-column>
    ...
</igx-grid>
```

```typescript
public ngAfterViewInit() {
    this._remoteService.getData(this.grid.virtualizationState, this.grid.sortingExpressions[0], true, (data) => {
            this.grid.totalItemCount = data["@odata.count"];
    });
}

public processData() {
    if (this.prevRequest) {
        this.prevRequest.unsubscribe();
    }

    this._prevRequest = this._remoteService.getData(this.grid.virtualizationState,
        this.grid.sortingExpressions[0], reset, () => {
        ...
        this.cdr.detectChanges();
    });
}
```

데이터를 요청할 때는 `startIndex` 및 `chunkSize` 속성을 제공하는 `IForOfState` 인터페이스를 사용해야 합니다.

***참고:*** 첫 번째 `chunkSize`는 항상 0이며 특정 애플리케이션애플리케이션 시나리오에 따라 결정해야 합니다.

### 원격 정렬/필터링 가상화
원격 정렬 및 필터링은 `onDataPreLoad`, `onSortingDone`, `onFilteringDone` 출력에 서브스크라이브하고 공개 `igxGrid` 속성 `totalItemCount`를 서비스에서 제공하는 각 정보와 함께 설정하고 얻은 인수를 기반으로 적절한 요청을 작성합니다.

원격 데이터를 요청할 때 필터링 작업은 대소문자를 구분합니다.

<div class="sample-container loading" style="height:550px">
    <iframe id="grid-remote-filtering-iframe" src='{environment:demosBaseUrl}/grid-remote-filtering' width="100%" height="100%" seamless frameBorder="0" onload="onSampleIframeContentLoaded(this);"></iframe>
</div>
<br/>
<div>
<button data-localize="stackblitz" disabled class="stackblitz-btn" data-iframe-id="grid-remote-filtering-iframe" data-demos-base-url="{environment:demosBaseUrl}">view on stackblitz</button>
</div>

### 가상화 제한 사항

*   행 높이의 변경은 지원되지 않습니다. 모든 행의 높이는 동일해야 합니다.
*   행/열의 지정된 규격은 실제 렌더링된 요소와 일치해야 합니다. 예를 들면, 행 높이를 높이는 템플릿 또는 클래스를 그리드 셀에 대해 정의한 경우에 지정한 `rowHeight` 값과 일치하지 않는 경우에는 수직 가상화가 정상적으로 작동하지 않습니다. 가상 항목 수는 더 이상 DOM의 실제 요소를 반영하지 않습니다. 열 및 너비도 동일하게 적용됩니다.
*   브라우저에는 현재 DOM 요소에 대한 높이 제한이 있습니다. 이 때문에 행의 전체 높이는 브라우저의 높이 제한을 초과해서는 안됩니다. 그렇지 않으면 `igxGrid`의 동작이 정상이 아닐 수 있습니다. 예를 들면, Internet Explorer 11의 높이 제한은 1,533,916픽셀로 이는 높이가 50px인 행의 제한은 30,678행입니다.
*   그리드에 응답하는 너비 및/또는 높이가 있으며 브라우저 창 또는 다른 요소 크기에 따라 크기를 변경하는 경우, 스크롤 위치는 0으로 다시 설정됩니다. 스크롤바의 위치 및 크기 변경에 대해서는 향후 자연스러운 해결책이 릴리스될 예정입니다.
*   Mac OS에서 "스크롤할 때 스크롤바 만 표시" 옵션이 true(기본값)로 설정되어 있으면 가로 스크롤바가 표시되지 않습니다. 이것은 그리드의 행 컨테이너에 오버플로가 숨기기로 설정되어 있기 때문입니다. 옵션을 "항상"으로 변경하면 스크롤바가 표시됩니다.

### FAQ

#### 왜 가상화가 작동하려면 그리드에 규격을 설정해야 합니까?

렌더링하기 전에 컨테이너 및 항목의 크기에 대한 정보가 없는 경우에 그리드에 임의의 위치로 스크롤하면 스크롤바의 너비 또는 높이를 설정하거나 표시 항목을 결정하는데 오류가 발생합니다. 실제 규격에 대한 추측이 스크롤바의 오작동으로 이어지고 궁극적으로 사용자의 경험을 저하시킵니다. 가상화를 유효화시키기 위해서는 관련 규격을 설정해야 합니다.

### 추가 리소스
<div class="divider--half"></div>

* [그리드 개요](grid.md)
* [페이징](grid_paging.md)
* [필터링](grid_filtering.md)
* [정렬](grid_sorting.md)
* [요약](grid_summaries.md)
* [열 이동](grid_column_moving.md)
* [열 핀 고정](grid_column_pinning.md)
* [열 크기 조정](grid_column_resizing.md)
* [선택](grid_selection.md)

<div class="divider--half"></div>
커뮤니티는 활동적이고 새로운 아이디어를 항상 환영합니다.

* [Ignite UI for Angular **Forums**](https://www.infragistics.com/community/forums/f/ignite-ui-for-angular)
* [Ignite UI for Angular **GitHub**](https://github.com/IgniteUI/igniteui-angular)