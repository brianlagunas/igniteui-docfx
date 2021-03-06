---
title: 금융 차트 - 퍼포먼스
_description: Ignite UI for Angular 금융 차트 컴포넌트는 간단하고 직관적인 API를 사용하여 재무 데이터를 표시하도록 쉽게 구성되어 있으며, 사용자가 데이터를 바인딩하면 차트는 데이터를 시각화하고 해석할 수 있는 다양한 방법을 제공합니다.
_keywords: Ignite UI for Angular, Angular, 네이티브 Angular 컴포넌트 세트, 네이티브 Angular 컨트롤, 네이티브 Angular 컴포넌트, 네이티브 Angular 컴포넌트 라이브러리, Angular 차트, Angular 차트 컨트롤, Angular 차트 예제, Angular 그리드 컴포넌트, Angular 차트 컴포넌트, Angular 금융 차트
_language: kr
---

## 퍼포먼스

`IgxFinancialChart` 컨트롤은 대량의 데이터 점을 렌더링할 수 있는 매우 우수한 성능을 제공합니다. 다음의 데모는 20년간의 데이터를 바인딩하고 캔들 스틱을 사용하여 1일 간격으로 주가를 표시합니다.

### 데모

<div class="sample-container loading" style="height: 550px">
    <iframe id="financial-chart-performance-iframe" src='{environment:demosBaseUrl}/charts/financial-chart-performance' width="100%" height="100%" seamless="" frameBorder="0" onload="onSampleIframeContentLoaded(this);"></iframe>
</div>
<div>
    <button data-localize="stackblitz" disabled class="stackblitz-btn"   data-iframe-id="financial-chart-performance-iframe" data-demos-base-url="{environment:demosBaseUrl}">StackBlitz 에서보기
    </button>
</div>
<div class="divider--half"></div>

다음의 코드는 금융 차트를 대량의 데이터에 바인딩하는 방법을 보여줍니다.

```typescript
import { GenerateOhlcPricesService } from "../services/generate-ohlc-prices.service";

export class AppComponent {
    public data: any;

    constructor(private dataService: GenerateOhlcPricesService) {
        const dateEnd = new Date(2018, 3, 20); // April 20, 2018
        const dateStart = new Date(1998, 3, 20); // April 20, 1998
        this.data = this.dataService.GetStockHistoryBetween(dateStart, dateEnd);
    }
}
```

```html
 <igx-financial-chart
    [dataSource]="data"
    width="850px"
    height="600px">
 </igx-financial-chart>
```

차트의 퍼포먼스에 영향을 주는 여러 Angular 고유 기능이 있으므로 애플리케이션에서 퍼포먼스를 최적화할 때 이를 고려해야 합니다.

-   컴포넌트에 바인딩할 속성에 대량의 데이터를 저장할 경우,  `@Component` 코레이터에서 `changeDetection: ChangeDetectionStrategy.OnPush`를 설정해야 합니다. Angular가 모든 변경 검출 주기에서 데이터 배열 내의 변경 사항을 확인하지 않도록 설정합니다.
-   Angular가 차트에 자동으로 데이터 변경을 알려주는 대신에 바인딩된 데이터가 변경된 방법을 컴포넌트에 알리도록 할 수 했습니다. 이러한 델타 알림은 Angular가 변경 검출을 실행할 때마다 100만 레코드 배열의 모든 변경을 비교하는 것보다 훨씬 효율적으로 실행할 수 있습니다. 바인딩된 데이터의 변경을 차트에 알리는 방법에 대한 자세한 것은 각 차트의 `notify*`메소드를 참조하십시오.
-   When Angular is in Debug mode, there is a lot of overhead in some browsers that will drag down performance. When evaluating real world performance always make sure to serve or build with `--prod` version.

[!NOTE]
For React:

-   When Angular is in development mode, there is a lot of overhead in some browsers that will drag down performance. When evaluating real world performance always make sure to use production builds.

또한, 애플리케이션에서 퍼포먼스를 최적화할 때 금융 차트의 다음 기능을 고려해야 합니다.

### 차트 유형

`chartType` 옵션을 설정하면 차트 퍼포먼스에 다음과 같은 영향을 미칠 수 있습니다:

-   `line` - 간단히 렌더링할 차트 유형이며 대량의 데이터 점을 렌더링하거나 대량의 데이터 소스를 플로팅할 때 권장됩니다.
-   `column` - `line` 차트 유형보다 렌더링이 복잡하며 단일 수치 값을 가진 데이터 항목을 렌더링할 경우에 권장됩니다.
-   `bar` - `column` 차트 유형보다 렌더링이 복잡하며 OHLC 수치 값을 가진 데이터 항목을 렌더링할 경우에 권장됩니다.
-   `candle` - `bar` 차트 유형보다 렌더링이 복잡하며 OHLC 수치 값을 가진 데이터 항목을 렌더링할 경우에도 권장됩니다.

### 볼륨 유형

`volumeType` 옵션을 설정하면 차트 퍼포먼스에 다음과 같은 영향을 미칠 수 있습니다:

-   `line` - 간단히 렌더링할 볼륨 유형이며 대량의 데이터 점을 렌더링하거나 대량의 데이터 소스를 플로팅할 때 권장됩니다.
-   `area` - `line` 볼륨 유형보다 렌더링이 복잡합니다.
-   `column` - `area` 볼륨 유형보다 렌더링이 복잡하며 1-3 재고의 볼륨 데이터를 렌더링할 경우에 권장됩니다.

### Marker Type

Setting the `markerTypes` option to `none` will decrease the amount of items to render than any other type.

### Legend Visibility

Setting the `isLegendVisible` option to `false` will increase performance since the legend will not be drawn.

### 줌 슬라이더 유형

`zoomSliderType` 옵션을 `none`으로 설정하면 차트 퍼포먼스가 향상되고 다른 인디케이터 및 볼륨 창을 위해 수직 공간을 더 많이 사용할 수 있습니다.

### 차트 창

`inidicatorTypes` 및 `overlayTypes` 옵션을 사용하여 복수의 창을 설정한 경우, 퍼포먼스가 저하될 수 있으므로 소수의 금융지표와 단일 금융 오버레이를 사용하는 것이 좋습니다.

### X축 모드

`xAxisMode` 옵션을 설정하면 차트 퍼포먼스에 다음과 같은 영향을 미칠 수 있습니다:

-   `ordinal` - 금융 차트에서 사용할 수 있는 가장 간단한 X축 모드이며 데이터 범위(예: 주말 또는 공휴일) 내에서 브레이크 렌더링이 필요하지 않은 경우에 권장됩니다.
-   `time` - 금융 차트에서 `ordinal`보다 복잡합니다 데이터 범위(예: 주말 또는 공휴일) 내에서 브레이크 렌더링이 필요할 경우에 권장됩니다.

### Y-Axis Mode

Setting the `yAxisMode` option to `numeric` is recommended for higher performance, as fewer operations are needed than using `percentChange` mode.

### Annotations

Enabling the Callout Annotations (`calloutsVisible`) or Final Value Annotations (`finalValueAnnotationsVisible`) will decrease performance of the financial chart.

### 축 비주얼

기본적으로 금융 차트는 최상의 퍼포먼스를 발휘하도록 최적화되어 있지만, 추가 차트 비주얼을 사용하면 퍼포먼스가 저하될 수 있는데 예를 들면 다음과 같습니다:

-   `xAxisInterval`
-   `yAxisInterval`
-   `xAxisTitle*`
-   `yAxisTitle*`
-   `xAxisTick*`
-   `yAxisTick*`
-   `xAxisMajor*`
-   `yAxisMajor*`
-   `xAxisMinor*`
-   `yAxisMinor*`
-   `xAxisLabel*`
-   `yAxisLabel*`
-   `xAxisStroke*`
-   `yAxisStroke*`
-   `xAxisStrip*`
-   `yAxisStrip*`

<div class="divider--half"></div>

### 추가 리소스

<div class="divider--half"></div>

-   [대량의 데이터 바인딩](financialchart_high_volume_data.md)
-   [실시간 데이터 바인딩](financialchart_real_time_data.md)
-   [복수 데이터 소스 바인딩](financialchart_binding_to_multiple_data.md)
