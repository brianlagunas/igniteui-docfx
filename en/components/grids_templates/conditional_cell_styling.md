@@if (igxName === 'IgxGrid') {
---
title: Conditional Cell Styling - Native Angular | Ignite UI for Angular
_description: Conditional Cell Styling feature provides a means for column cells styling based on custom conditions.
_keywords: Ignite UI for Angular, UI controls, Angular widgets, web widgets, UI widgets, Angular, Native Angular Components Suite, Native Angular Controls, Native Angular Components Library, Angular Grid, Angular Table, Angular Data Grid component, Angular Data Table component, Angular Data Grid control, Angular Data Table control, Angular Grid component, Angular Table component, Angular Grid control, Angular Table control, Angular High Performance Grid, Angular High Performance Data Table, Cell Styling, Conditional Formatting, Conditional Cell Styling, Angular Grid Conditional Column Styling, Angular Data Table Conditional Column Styling, Angular Conditional Cell Styling
---
}
@@if (igxName === 'IgxTreeGrid') {
---
title: Conditional Cell Styling - Native Angular | Ignite UI for Angular
_description: Conditional Cell Styling feature provides a means for column cells styling based on custom conditions.
_keywords: Ignite UI for Angular, UI controls, Angular widgets, web widgets, UI widgets, Angular, Native Angular Components Suite, Native Angular Controls, Native Angular Components Library, Angular Tree Grid, Angular Tree Table, Angular Tree Grid component, Angular Tree Table component, Angular Tree Grid control, Angular Tree Table control, Angular Tree Grid component, Angular Tree Table component, Angular Tree Grid control, Angular Tree Table control, Angular High Performance Tree Grid, Angular High Performance Tree Table, Cell Styling, Conditional Formatting, Conditional Cell Styling, Angular Tree Grid Conditional Column Styling, Angular Tree Table Conditional Column Styling, Angular Conditional Cell Styling
---
}
@@if (igxName === 'IgxHierarchicalGrid') {
---
title: Conditional Cell Styling - Native Angular | Ignite UI for Angular
_description: Conditional Cell Styling feature provides a means for column cells styling based on custom conditions.
_keywords: Ignite UI for Angular, UI controls, Angular widgets, web widgets, UI widgets, Angular, Native Angular Components Suite, Native Angular Controls, Native Angular Components Library, Angular Hierarchical Grid, Angular Hierarchical Table, Angular Hierarchical Grid component, Angular Hierarchical Table component, Angular Hierarchical Grid control, Angular Hierarchical Table control, Angular High Performance Hierarchical Grid, Angular High Performance Hierarchical Table, Cell Styling, Conditional Formatting, Conditional Cell Styling, Angular Hierarchical Grid Conditional Column Styling, Angular Hierarchical Table Conditional Column Styling, Angular Conditional Cell Styling
---
}

### Conditional Cell Styling
The @@igxName component in Ignite UI for Angular provides **conditional cell styling** based on custom rules.

This can be achieved by setting the [`IgxColumnComponent`]({environment:angularApiUrl}/classes/igxcolumncomponent.html) input [`cellClasses`]({environment:angularApiUrl}/classes/igxcolumncomponent.html#cellclasses) to an object literal containing key-value pairs. The key is the name of the CSS class, while the value is either a callback function that returns a boolean, or boolean value.

#### Demo

@@if (igxName === 'IgxGrid') {
<div class="sample-container loading" style="height:530px">
    <iframe id="grid-cell-styling-sample-iframe" src='{environment:demosBaseUrl}/grid/grid-cell-styling' width="100%" height="100%" seamless frameBorder="0" onload="onSampleIframeContentLoaded(this);"></iframe>
</div>
<br/>
<div>
<button data-localize="stackblitz" disabled class="stackblitz-btn" data-iframe-id="grid-cell-styling-sample-iframe" data-demos-base-url="{environment:demosBaseUrl}">view on stackblitz</button>
</div>
}
@@if (igxName === 'IgxTreeGrid') {
<div class="sample-container loading" style="height:600px">
    <iframe id="treegrid-cell-styling-sample-iframe" src='{environment:demosBaseUrl}/tree-grid/treegrid-conditional-cell-style' width="100%" height="100%" seamless frameBorder="0" onload="onSampleIframeContentLoaded(this);"></iframe>
</div>
<br/>
<div>
<button data-localize="stackblitz" disabled class="stackblitz-btn" data-iframe-id="treegrid-cell-styling-sample-iframe" data-demos-base-url="{environment:demosBaseUrl}">view on stackblitz</button>
</div>
}
@@if (igxName === 'IgxHierarchicalGrid') {
<!-- TODO -->
}
<div class="divider--half"></div>

#### Overview
You can conditionally style the @@igxName cells by setting the [`IgxColumnComponent`]({environment:angularApiUrl}/classes/igxcolumncomponent.html) [`cellClasses`]({environment:angularApiUrl}/classes/igxcolumncomponent.html#cellclasses) input and defining custom rules.

@@if (igxName === 'IgxGrid') {
```html
<!-- sample.component.html -->
<igx-column field="BeatsPerMinute" dataType="number" [cellClasses]="beatsPerMinuteClasses"></igx-column>
```
}
@@if (igxName === 'IgxTreeGrid'){
```html
<!-- sample.component.html -->
<igx-column field="UnitPrice" header="Unit Price" [dataType]="'number'" [cellClasses] = "priceClasses">
    <ng-template igxCell let-cell="cell" let-val>
        <span *ngIf="cell.row.rowData.UnitPrice == 0">-</span>
        <span *ngIf="cell.row.rowData.UnitPrice != 0">${{val}}</span>
    </ng-template>
</igx-column>
```
}
@@if (igxName === 'IgxHierarchicalGrid') {
<!-- TODO -->
}

The [`cellClasses`]({environment:angularApiUrl}/classes/igxcolumncomponent.html#cellclasses) input accepts an object literal, containing key-value pairs, where the key is the name of the CSS class, while the value is either a callback function that returns a boolean, or boolean value.

@@if (igxName === 'IgxGrid') {
```typescript
// sample.component.ts

private upFontCondition = (rowData: any, columnKey: any): boolean => {
    return rowData[columnKey] > 95;
}

private downFontCondition = (rowData: any, columnKey: any): boolean => {
    return rowData[columnKey] <= 95;
}

public beatsPerMinuteClasses = {
    downFont: this.downFontCondition,
    upFont: this.upFontCondition
};
```

```scss
// sample.component.scss

::ng-deep {
    .upFont {
        color: green;
    }

    .downFont {
        color: red;
    }
}
```
}
@@if (igxName === 'IgxTreeGrid'){
```typescript
// sample.component.ts

private upPriceCondition = (rowData: any, columnKey: any): boolean => {
    return rowData[columnKey] > 25;
}

private downPriceCondition = (rowData: any, columnKey: any): boolean => {
    return rowData[columnKey] <= 25;
}

public priceClasses = {
    downPrice: this.downPriceCondition,
    upPrice: this.upPriceCondition
};
```

```scss
// sample.component.scss

::ng-deep {
    .upPrice {
        color: red;
    }

    .downPrice {
        color: green;
    }
}
```
}
@@if (igxName === 'IgxHierarchicalGrid') {
<!-- TODO -->
}

Use **::ng-deep** or **`ViewEncapsulation.None`** to force the custom styles down through the current component and its children.

### API References
<div class="divider--half"></div>

* [IgxColumnComponent]({environment:angularApiUrl}/classes/igxcolumncomponent.html)
* [@@igxNameComponent]({environment:angularApiUrl}/classes/@@igTypeDoc.html)
* [@@igxNameComponent Styles]({environment:sassApiUrl}/index.html#mixin-igx-grid)

### Additional Resources
<div class="divider--half"></div>

* [@@igComponent overview](@@igMainTopic.md)
* [Virtualization and Performance](virtualization.md)
* [Editing](editing.md)
* [Paging](paging.md)
* [Filtering](filtering.md)
* [Sorting](sorting.md)
* [Summaries](summaries.md)
* [Column Moving](column_moving.md)
* [Column Pinning](column_pinning.md)
* [Column Resizing](column_resizing.md)
* [Column Hiding](column_hiding.md)
* [Selection](selection.md)
* [Searching](search.md)
* [Toolbar](toolbar.md)
* [Multi Column Headers](multi_column_headers.md)
* [Display Density](display_density.md)

<div class="divider--half"></div>
Our community is active and always welcoming to new ideas.

* [Ignite UI for Angular **Forums**](https://www.infragistics.com/community/forums/f/ignite-ui-for-angular)
* [Ignite UI for Angular **GitHub**](https://github.com/IgniteUI/igniteui-angular)
