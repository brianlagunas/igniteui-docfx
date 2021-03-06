---
title: Data Grid Component
_description: The Ignite UI for Angular Data Grid control features the fastest, touch-responsive data-rich grid with popular features, including hierarchical and list views.
_keywords: Ignite UI for Angular, UI controls, Angular widgets, web widgets, UI widgets, Angular, Native Angular Components Suite, Native Angular Controls, Native Angular Components Library, Angular Data Grid component, Angular Data Grid control, Angular Grid component, Angular Grid control, Angular High Performance Grid
---

## Data Grid

<p class="highlight">Display and manipulate tabular data with the Ignite UI for Angular Data Grid. Quickly bind your data with very little coding or configuration. Features include filtering, sorting, paging, templates, movable columns, and the ability to edit and update data. User actions are easy to understand and can be controlled programmatically.</p>

### Demo

<div class="sample-container loading" style="height:700px">
    <iframe id="grid-sample-iframe" src='{environment:demosBaseUrl}/grid/grid' width="100%" height="100%" seamless frameBorder="0" onload="onSampleIframeContentLoaded(this);"></iframe>
</div>
<br/>
<div>
<button data-localize="stackblitz" disabled class="stackblitz-btn" data-iframe-id="grid-sample-iframe" data-demos-base-url="{environment:demosBaseUrl}">view on stackblitz</button>
</div>
<div class="divider--half"></div>

### Dependencies

The grid is exported as an `NgModule`, thus all you need to do in your application is to import the `IgxGridModule` inside your `AppModule`:

```typescript
// app.module.ts

import { IgxGridModule } from 'igniteui-angular';
// Or
import { IgxGridModule } from 'igniteui-angular/grid';

@NgModule({
    imports: [
        ...
        IgxGridModule.forRoot(),
        ...
    ]
})
export class AppModule {}
```

Each of the components, directives and helper classes in the `IgxGridModule` can be imported either through the _grid_ sub-package or through the main bundle in _igniteui-angular_. While you don't need to import all of them to instantiate and use the grid, you usually will import them (or your editor will auto-import them for you) when declaring types that are part of the grid API.

```typescript
import { IgxGridComponent } from 'igniteui-angular/grid/';
// Or
import { IgxGridComponent } from 'igniteui-angular'
...

@ViewChild('myGrid', { read: IgxGridComponent })
public grid: IgxGridComponent;
```

### Usage

Now that we have the grid module imported, let’s get started with a basic configuration of the **igx-grid** that binds to local data:

```html
<igx-grid #grid1 id="grid1" [data]="localData" [autoGenerate]="true"></igx-grid>
```

The **id** property is a string value and is the unique identifier of the grid which will be autogenerated if not provided, while **data** binds the grid, in this case to local data.

The [`autoGenerate`]({environment:angularApiUrl}/classes/igxgridcomponent.html#autogenerate) property tells the **igx-grid** to auto generate the grid's [`IgxColumnComponent`]({environment:angularApiUrl}/classes/igxcolumncomponent.html) based on the data source fields. It will also try to deduce the appropriate data type for the column if possible. Otherwise, the developer needs to explicitly define the columns and the mapping to the data source fields.

### Styling Configuration
> [!NOTE]
> The [**IgxGridComponent**]({environment:angularApiUrl}/classes/igxgridcomponent.html) uses **css grid layout**, which is **not supported in IE without prefixing**, consequently it will not render properly.

In [**Angular**](https://angular.io/) most of the styles are prefixed implicitly thanks to the [Autoprefixer](https://www.npmjs.com/package/autoprefixer) plugin. 

For prefixing **grid layouts** however, you need to enable the [Autoprefixer](https://www.npmjs.com/package/autoprefixer) **grid property** with the comment `/* autoprefixer grid:on */`.

To facilitate your work, apply the comment in the `src/styles.scss` file.

 ```scss
 // src/styles.scss
    @import '~igniteui-angular/lib/core/styles/themes/index';
    @include igx-core();
    @include igx-theme($default-palette);

    /* autoprefixer grid:on */
 ...
 ``` 

### Columns configuration

[`IgxColumnComponent`]({environment:angularApiUrl}/classes/igxcolumncomponent.html) is used to define the grid's [`columns`]({environment:angularApiUrl}/classes/igxgridcomponent.html#columns) collection and to enable features per column like **sorting** and **paging**. Cell, header, and footer templates are also available.

Let's turn the [`autoGenerate`]({environment:angularApiUrl}/classes/igxgridcomponent.html#autogenerate) property off and define the columns collection in the markup:

```html
<igx-grid #grid1 [data]="data | async" [autoGenerate]="false" [paging]="true" [perPage]="6" (onColumnInit)="initColumns($event)"
    (onSelection)="selectCell($event)" [allowFiltering]="true">
    <igx-column field="Name" [sortable]="true" header=" "></igx-column>
    <igx-column field="AthleteNumber" [sortable]="true" header="Athlete number" [filterable]="false"></igx-column>
    <igx-column field="TrackProgress" header="Track progress" [filterable]="false">
        <ng-template igxCell let-value>
            <igx-linear-bar [stripped]="false" [value]="value" [max]="100"></igx-linear-bar>
        </ng-template>
    </igx-column>
</igx-grid>
```

Each of the columns of the grid can be templated separately. The column expects `ng-template` tags decorated with one of the grid module directives.

`igxHeader` targets the column header providing as a context the column object itself.

```html
...
<igx-column field="Name">
    <ng-template igxHeader let-column>
        {{ column.field | uppercase }}
    </ng-template>
</igx-column>
...
```

`igxCell` applies the provided template to all cells in the column. The context object provided in the template consists of the cell value provided implicitly and the cell object itself. It can be used to define a template where the cells can grow according to their content, as in the below example.

```html
...
<igx-column field="Name">
    <ng-template igxCell let-value>
        {{ value | titlecase }}
    </ng-template>
</igx-column>
...
```

In the snippet above we "take" a reference to the implicitly provided cell value. This is sufficient if you just want to present some data and maybe apply some custom styling or pipe transforms over the value of the cell. However even more useful is to take the [`IgxGridCellComponent`]({environment:angularApiUrl}/classes/igxgridcellcomponent.html) object itself as shown below:

```html
<igx-grid #grid [data]="data">
    <igx-column dataType="string" field="Name">
        <ng-template igxCell let-cell="cell">
            <!-- Implement row deleting inside the cell template itself -->
            <span tabindex="0" (keydown.delete)="grid.deleteRow(cell.rowIndex)">{{ cell.value | titlecase }}</span>
        </ng-template>
    </igx-column>
    <igx-column dataType="boolean" field="Subscribtion">
        <ng-template igxCell let-cell="cell">
            <!-- Bind the cell value through the ngModel directive and update the data source when the value is changed in the template -->
            <input type="checkbox" [ngModel]="cell.value" (ngModelChange)="cell.update($event)" />
        </ng-template>
    </igx-column>
<igx-grid>
```

The column also accepts one last template that will be used when a cell is in edit mode. As with the other column templates, the provided context object is again the cell value and the cell object itself. Of course in order to make the edit-mode template accessible to end users, you need
to set the [`editable`]({environment:angularApiUrl}/classes/igxcolumncomponent.html#editable) property of the [`IgxColumnComponent`]({environment:angularApiUrl}/classes/igxcolumncomponent.html) to `true`.

```html
<igx-column dataType="number" editable="true" field="Price">
    <ng-template igxCellEditor let-cell="cell">
        <label for="price">
            Enter the new price tag
        </label>
        <input name="price" type="number" [ngModel]="cell.value" (ngModelChange)="cell.update(convertToNumber($event))" />
    </ng-template>
</igx-column>
```

Make sure to check the API for the [`IgxGridCellComponent`]({environment:angularApiUrl}/classes/igxgridcellcomponent.html) in order to get accustomed with the provided properties you can use in your templates.

Each of the column templates can be changed programmatically at any point through the [`IgxColumnComponent`]({environment:angularApiUrl}/classes/igxcolumncomponent.html) object itself. For example in the code below, we have declared two templates for our user data. In our TypeScript code we'll get references to the templates themselves and then based on some condition we will render the appropriate template for the column in our application.

```html
<igx-grid>
    <!-- Column declarations -->
</igx-grid>

<ng-template #normalView let-value>
    <div class="user-details">{{ val }}</div>
    <user-details-component></user-details-component>
</ng-template>

<ng-template #smallView let-value>
    <div class="user-details-small">{{ val }}</div>
</ng-template>
```

```typescript
@ViewChild("normalView", { read: TemplateRef })
public normalView: TemplateRef<any>;

@ViewChild("smallView", { read: TemplateRef })
public smallView: TemplateRef<any>;

....

const column = this.grid.getColumnByName("User");
// Return the appropriate template based on some conditiion.
// For example saved user settings, viewport size, etc.
column.bodyTemplate = this.smallView;
```

Column properties can also be set in code in the [`initColumns`]({environment:angularApiUrl}/classes/igxgridcomponent.html#oncolumninit) event which is emitted when the columns are initialized in the grid.

```typescript
public initColumns(column: IgxGridColumn) {
    const column: IgxColumnComponent = column;
    if (column.field === 'ProductName') {
        column.sortable = true;
        column.editable = true;
    }
}
```

The code above will make the **ProductName** column sortable and editable and will instantiate the corresponding features UI (like inputs for editing, etc.).

### Data structure

The [IgxGridComponent]({environment:angularApiUrl}/classes/igxgridcomponent.html) takes only **flat data**. The data structure specific for rendering is in the form: 

```typescript
const OBJECT_ARRAY = [{
        ObjectKey1: value1,
        ObjectKey2: value2,
        .
        .
        .
        ObjectKeyN: valueN
    },
    {
        ObjectKey1: value1,
        ObjectKey2: value2,
        .
        .
        .
        ObjectKeyN: valueN
    },
    .
    .
    .,
    {
        ObjectKey1: value1,
        ObjectKey2: value2,
        .
        .
        .
        ObjectKeyN: valueN 
    }];

```
>[!WARNING]
>**The key values must not contain neither arrays or other objects**.

>If you use [autoGenerate]({environment:angularApiUrl}/classes/igxgridcomponent.html#autogenerate) columns **the data keys must be identical.** 

### Data binding

Before going any further with the grid we want to change the grid to bind to remote data service, which is the common scenario in large-scale applications. A good practice is to separate all data fetching related logic in a separate data service, so we are going to create a service which will handle the fetching of data from the server.

Let's implement our service in a separate file

```typescript
// northwind.service.ts

import { Injectable } from '@angular/core';
import { HttpClient } from '@angular/common/http';
import { Observable } from 'rxjs/Observable';
import { of } from 'rxjs/observable/of';
import { catchError, map } from 'rxjs/operators';
```

We're importing the `Injectable` decorator which is an [essential ingredient](https://angular.io/guide/dependency-injection) in every Angular service definition. The `HttpClient` will provide us with the functionality to communicate with backend services. It returns an `Observable` of some result to which we will subscribe in our grid component.

**Note**: Before Angular 5 the `HttpClient` was located in `@angular/http` and was named `Http`.

Since we will receive a JSON response containing an array of records, we may as well help ourselves by specifing what kind of data we're expecting to be returned in the observable by defining an interface with the correct shape. Type checking is always recommended and can save you some headaches down the road.

```typescript
// northwind.service.ts

export interface NorthwindRecord {
    ProductID: number;
    ProductName: string;
    SupplierID: number;
    CategoryID: number;
    QuantityPerUnit: string;
    UnitPrice: number;
    UnitsInStock: number;
    UnitsOnOrder: number;
    ReorderLevel: number;
    Discontinued: boolean;
    CategoryName: string;
}
```

The service itself is pretty simple consisting of one method: `fetchData` that will return an `Observable<NorthwindRecord[]>`. In cases when the request fails for any reason (server unavailable, network error, etc), the `HttpClient` will return an error. We'll leverage the `catchError` operator which intercepts an _Observable_ that failed and passes the error to an error handler. Our error handler will log the error and return a safe value.

```typescript
// northwind.service.ts

@Injectable()
export class NorthwindService {
    private url = 'http://services.odata.org/V4/Northwind/Northwind.svc/Alphabetical_list_of_products';

    constructor(private http: HttpClient) {}

    public fetchData(): Observable<NorthwindRecord[]> {
        return this.http
            .get(this.url)
            .pipe(
                map(response => response['value']),
                catchError(
                    this.errorHandler('Error loading northwind data', [])
                )
            );
    }

    private errorHandler<T>(message: string, result: T) {
        return (error: any): Observable<any> => {
            console.error(`${message}: ${error.message}`);
            return of(result as T);
        };
    }
}
```

Make sure to import both the `HttpClientModule` and our service in the application module and register the service as a provider.

```typescript
// app.module.ts

import { HttpClientModule } from '@angular/common/http';
...
import { NorthwindService } from './northwind.service';

@NgModule({
    imports: [
        ...
        HttpClientModule
        ...
    ],
    providers: [
        NorthwindService
    ]
})
export class AppModule {}
```

After implementing the service we will inject it in our component's constructor and use it to retrieve the data. The `ngOnInit` lifecycle hook is a good place to dispatch the initial request.

**Note**: In the code below, you may wonder why are we setting the _records_ property to an empty array before subscribing to the service. The Http request is asynchronous, and until it completes, the _records_ property will be _undefined_ which will result in an error when the grid tries to bind to it. You should either initialize it with a default value or use a `BehaviorSubject`.

```typescript
// my.component.ts

@Component({
    ...
})
export class MyComponent implements OnInit {

    public records: NorthwindRecord[];

    constructor(private northwindService: NorthwindService) {}

    ngOnInit() {
        this.records = [];
        this.northwindService.fetchData().subscribe((records) => this.records = records);
    }
}
```

and in the template of the component:

```html
    <igx-grid [data]="records">
        <igx-column field="ProductId"></igx-column>
        <!-- rest of the column definitions -->
        ...
    </igx-grid>
```

**Note**: The grid [`autoGenerate`]({environment:angularApiUrl}/classes/igxgridcomponent.html#autogenerate) property is best to be avoided when binding to remote data for now. It assumes that the data is available in order to inspect it and generate the appropriate columns. This is usually not the case until the remote service responds, and the grid will throw an error. Making [`autoGenerate`]({environment:angularApiUrl}/classes/igxgridcomponent.html#autogenerate) available, when binding to remote service, is on our roadmap for future versions.

### Keyboard navigation
Keyboard navigation is available by default in any grid and aims at covering as many as possible features and scenarios for the end user. When you focus a specific cell and press one of the following key combinations, the described behaviour is performed:

 - `Arrow Up` - navigates one cell up (no wrapping);
 - `Arrow Down` - navigates one cell down (no wrapping);
 - `Arrow Left` - navigates one cell left (no wrapping between lines);
 - `Arrow Right` - navigates one cell right (no wrapping between lines);
 - `Ctrl + Arrow Up` - navigates to the first cell in the current column;
 - `Ctrl + Arrow Down` - navigates to the last cell in the current column;
 - `Ctrl + Arrow Left` -  moves to leftmost cell in row;
 - `Home` - moves to leftmost cell in row;
 - `Ctrl + Home` - moves to top left cell in the grid;
 - `Ctrl + Arrow Right` - moves to rightmost cell in row;
 - `End` - moves to rightmost cell in row;
 - `Ctrl + End` - moves to bottom right cell in the grid;
 - `Page Up` - scrolls one page (view port) up;
 - `Page Down` -  scrolls one page (view port) down;
 - `Enter` - enters edit mode;
 - `F2` - enters edit mode;
 - `Esc` - exits edit mode;
 - `Tab` - sequentially move the focus over the next cell on the row and if the last cell is reached move to next row; If next row is group row the whole row is focused, if it is data row, move focus over the first cell; When cell is in edit mode, will move the focus to next editable cell in the row, and from the right-most editable cell to the `CANCEL` and `DONE` buttons, and from the `DONE` button to the left-most editable cell within the currently edited row;
 - `Shift + Tab` - sequentially move focus to the previous cell on the row, if the first cell is reached move the focus to the previous row. If previous row is group row focus the whole row or if it is data row, focus the last cell of the row; when cell is in edit mode, will move the focus to the next editable cell in the row, and from the right-most editable cell to the `CANCEL` and `DONE` buttons, and from the `DONE` button to the left-most editable cell within the currently edited row;
 - `Space` -  if the row is selectable, on keydown space triggers row selection;
 - `Alt + Arrow Left` over GroupRow - collapses the group row content if the row is not already collapsed;
 - `Alt + Arrow Right` over GroupRow - expands the group row content if the row is not already expanded;
 - on mouse `wheel` -  blurs the focused element;

### Live Updating Demo

This sample demonstrates the `igxGrid` bound to live data. 

<div class="sample-container loading" style="height:915px">
    <iframe id="grid-sample-finjs-iframe" data-src='{environment:demosBaseUrl}/finjs-sample' width="100%" height="100%" seamless="" frameborder="0" class="lazyload"></iframe>
</div>
<div>
<button data-localize="stackblitz" disabled class="stackblitz-btn" data-iframe-id="grid-sample-finjs-iframe" data-demos-base-url="{environment:demosBaseUrl}">view on stackblitz</button>
</div>

## Known Limitations

|Limitation|Description|
|--- |--- |
|Column widths set in `percentage` and `px`|Currently we do not support mixing of column widths with `%` and `px`.|
|When trying to filter a column of type `number`|If a value different than `number` is entered into the filtering input, `NaN` is returned due to an incorrect cast.|
|Grid [`width`]({environment:angularApiUrl}/classes/igxgridcomponent.html#width) does not depend on the column widths | The [`width`]({environment:angularApiUrl}/classes/igxcolumncomponent.html#width) of all columns does not determine the spanning of the grid itself. It is determined by the parent container dimensions or the defined grid's [`width`]({environment:angularApiUrl}/classes/igxgridcomponent.html#width).|
|Grid nested in parent container | When grid's [`width`]({environment:angularApiUrl}/classes/igxgridcomponent.html#width) is not set and it is placed in a parent container with defined dimensions, the grid spans to this container.|
|Grid `OnPush` ChangeDetectionStrategy |The grid operates with `ChangeDetectionStrategy.OnPush` so whenever some customization appears make sure that the grid is notified about the changes that happens.|
| Columns have a minimum allowed column width. Depending on the [`displayDensity`]({environment:angularApiUrl}/classes/igxgridcomponent.html#displaydensity) option, they are as follows: <br/>"compact": 24px <br/> "cosy": 32px <br/> "comfortable ": 48px | If width less than the minimum allowed is set it will not affect the rendered elements. They will render with the minimum allowed width for the corresponding [`displayDensity`]({environment:angularApiUrl}/classes/igxgridcomponent.html#displaydensity). This may lead to an unexpected behavior with horizontal virtualization and is therefore not supported.
| Row height is not affected by the height of cells that are not currently rendered in view. | Because of virtualization a column with a custom template (that changes the cell height) that is not in the view will not affect the row height. The row height will be affected only while the related column is scrolled in the view.

<div class="divider--half"></div>

## API References
* [IgxGridComponent]({environment:angularApiUrl}/classes/igxgridcomponent.html)
* [IgxGridComponent Styles]({environment:sassApiUrl}/#function-igx-grid-theme)
* [IgxColumnComponent]({environment:angularApiUrl}/classes/igxcolumncomponent.html)
* [IgxGridRowComponent]({environment:angularApiUrl}/classes/igxgridrowcomponent.html)
* [IgxGridCellComponent]({environment:angularApiUrl}/classes/igxgridcellcomponent.html)

## Additional Resources
<div class="divider--half"></div>

* [Virtualization and Performance](virtualization.md)
* [Paging](paging.md)
* [Filtering](filtering.md)
* [Sorting](sorting.md)
* [Summaries](summaries.md)
* [Column Moving](column_moving.md)
* [Column Pinning](column_pinning.md)
* [Column Resizing](column_resizing.md)
* [Selection](selection.md)

<div class="divider--half"></div>
Our community is active and always welcoming to new ideas.

* [Ignite UI for Angular **Forums**](https://www.infragistics.com/community/forums/f/ignite-ui-for-angular)
* [Ignite UI for Angular **GitHub**](https://github.com/IgniteUI/igniteui-angular)
