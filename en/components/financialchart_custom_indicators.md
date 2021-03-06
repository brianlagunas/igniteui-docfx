---
title: Financial Chart | Data Visualization Tools | Ignite UI for Angular | Infragistics | Custom Indicators
_description: Use the financial chart component to visualize financial data using a simple API. View the demo, dependencies, usage and toolbar for more information. 
_keywords: financial chart, Ignite UI for Angular, infragistics
---

## Custom Indicators

The `IgxFinancialChart` control allows you to define custom financial indicators to display in the Indicator Pane.

### Demo

<div class="sample-container" style="height: 500px">
    <iframe id="financial-chart-custom-indicators-iframe" src='{environment:demosBaseUrl}/charts/financial-chart-custom-indicators' width="100%" height="100%" seamless frameBorder="0" onload="onSampleIframeContentLoaded(this);"></iframe>
</div>
<div>
    <button data-localize="stackblitz" disabled class="stackblitz-btn"   data-iframe-id="financial-chart-custom-indicators-iframe" data-demos-base-url="{environment:demosBaseUrl}">View on StackBlitz
    </button>
</div>

<div class="divider--half"></div>

In the `IgxFinancialChart`, you can enable custom financial indicators by adding names for them to the `customIndicatorNames` property and performing calculations for them in the `applyCustomIndicators` event.

The following code example shows how to set up and calculate two custom indicators, one featuring the Simple Moving Average (SMA) and one displaying random values.

```html
 <igx-financial-chart
    width="850px"
    height="600px"
    [dataSource]="data"
    (applyCustomIndicators)="applyCustomIndicators($event)"
    customIndicatorNames="Open, Open (SMA)">
 </igx-financial-chart>
```

```typescript
    public applyCustomIndicators(event: { sender: any, args: FinancialChartCustomIndicatorArgs }) {
        if (event.args.index === 0) {
            const info: FinancialEventArgs = event.args.indicatorInfo;
            const ds = info.dataSource;
            const open = ds.openColumn;
            for (let i = 0; i < ds.indicatorColumn.length; i++) {
                ds.indicatorColumn[i] = open[i];
            }
        } else {
            const info: FinancialEventArgs = event.args.indicatorInfo;
            const ds = info.dataSource;
            const close = ds.closeColumn;
            for (let i = 0; i < ds.indicatorColumn.length; i++) {
                let startIndex = i - 9;
                if (startIndex < 0) {
                    startIndex = 0;
                }
                const count = (i - startIndex) + 1;

                let sum = 0;
                for (let j = startIndex; j <= i; j++) {
                    sum += close[j];
                }
                ds.indicatorColumn[i] = sum / count;
            }
        }
    }
```
