---
title: Grid sorting
_description: The Ignite UI for Angular Grid control features the fastest, touch-responsive data-rich grid with popular features, including hierarchical and list views.
_keywords: Ignite UI for Angular, UI controls, Angular widgets, web widgets, UI widgets, Angular, Native Angular Components Suite, Native Angular Controls, Native Angular Components Library, Angular Grid component, Angular Grid control, Angular High Performance Grid, Sorting, sort
---

### Grid Sorting

In Ignite UI for Angular, **Sorting** is enabled on a per-column level, meaning that the Grid can have a mix of sortable and non-sortable columns.

#### Demo
Additionally there is a custom contextmenu added for sorting using Grid's [`onContextMenu`]({environment:angularApiUrl}/classes/igxgridcomponent.html#oncontextmenu) Output.

<!-- #insert demo -->

This is done via the [`sortable`]({environment:angularApiUrl}/classes/igxcolumncomponent.html#sortable) input. With the grid sorting, you can also set the [`sortingIgnoreCase`]({environment:angularApiUrl}/classes/igxcolumncomponent.html#sortingignorecase) property to perform case sensitive sorting:

```html
<igx-column field="ProductName" header="Product Name" [dataType]="'string'" sortable="true"></igx-column>
```

#### Sorting through the API

You can sort any column or a combination of columns through the grid API using the grid [`sort`]({environment:angularApiUrl}/classes/igxgridcomponent.html#sort) method:

```typescript
import { SortingDirection } from 'igniteui-angular';

// Perform a case insensitive ascending sort on the ProductName column.
this.grid.sort({ fieldName: 'ProductName', dir: SortingDirection.Asc, ignoreCase: true });

// Perform sorting on both the ProductName and Price columns.
this.grid.sort([
    { fieldName: 'ProductName', dir: SortingDirection.Asc, ignoreCase: true },
    { fieldName: 'Price', dir: SortingDirection.Desc }
]);
```

> [!NOTE]
> Sorting is performed using our [`DefaultSortingStrategy`]({environment:angularApiUrl}/classes/defaultsortingstrategy.html) algorithm. Any [`IgxColumnComponent`]({environment:angularApiUrl}/classes/igxcolumncomponent.html#sortStrategy) or [`ISortingExpression`]({environment:angularApiUrl}/interfaces/isortingexpression.html#strategy) can use a custom implementation of the [`ISortingStrategy`]({environment:angularApiUrl}/interfaces/isortingstrategy.html) as a substitute algorithm. This is useful when custom sorting needs to be defined for complex template columns, or image columns, for example.

As with the filtering behavior, you can clear sorting state using the [`clearSort`]({environment:angularApiUrl}/classes/igxgridcomponent.html#clearsort) method:

```typescript
// Removes the sorting state from the ProductName column
this.grid.clearSort('ProductName');

// Removes the sorting state from every column in the grid
this.grid.clearSort();
```

> [!NOTE]
> The sorting operation **DOES NOT** change the underlying data source of the grid.

#### Initial sorting state

It is possible to set the initial sorting state of the grid by passing an array of sorting expressions to the [`sortingExpressions`]({environment:angularApiUrl}/classes/igxgridcomponent.html#sortingexpressions) property of the grid.

```typescript
public ngOnInit() {
    this.grid.sortingExpressions = [
        { fieldName: 'ProductName', dir: SortingDirection.Asc, ignoreCase: true },
        { fieldName: 'Price', dir: SortingDirection.Desc }
    ];
}
```

> [!NOTE]
> If values of type `string` are used by column of [`dataType`]({environment:angularApiUrl}/classes/igxcolumncomponent.html#datatype) `Date`, the grid won't parse it to `Date` objects and using Grid `sorting` won't work as expected. If you want to use `string` objects, additional logic should be implemented on an application level, in order to parse the values to `Date` object.

<div class="divider--half"></div>

#### Remote Sorting
You can provide grid's remote sorting by subscribing to [`onDataPreLoad`]({environment:angularApiUrl}/classes/igxgridcomponent.html#ondatapreload) and [`onSortingDone`]({environment:angularApiUrl}/classes/igxgridcomponent.html#onsortingdone) outputs.
<!-- More information on how to use it you can find in the `Grid Virtualization and Performance` [documentation](grid_virtualization.md#remote-sortingfiltering-virtualization). -->

<div class="divider--half"></div>

### API
<!-- #insert API references -->

### Additional Resources
<div class="divider--half"></div>

<!-- #insert Additional resources -->

<div class="divider--half"></div>
Our community is active and always welcoming to new ideas.

* [Ignite UI for Angular **Forums**](https://www.infragistics.com/community/forums/f/ignite-ui-for-angular)
* [Ignite UI for Angular **GitHub**](https://github.com/IgniteUI/igniteui-angular)