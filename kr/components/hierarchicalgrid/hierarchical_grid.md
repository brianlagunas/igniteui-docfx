---
title: Hierarchical Grid Component
_description: The Ignite UI for Angular Hierarchical Grid control features the fastest, touch-responsive data-rich hierarchical grid with popular features.
_keywords: Ignite UI for Angular, UI controls, Angular widgets, web widgets, UI widgets, Angular, Native Angular Components Suite, Native Angular Controls, Native Angular Components Library, Angular Hierarchical Grid component, Angular Hierarchical Grid control, Angular High Performance Hierarchical Grid, Hierarchical Grid
---
## Hierarchical Grid
<p class="highlight">Display and manipulate hierarchically structured data with the Ignite UI for Angular Hierarchical Grid. Features include Filtering, Sorting, Paging, Templates, Column Pinning, Column Moving and Column Hiding, as well as Updating the visualized data. The Hierarchical Grid builds upon the Data Grid Component and extends its functionality by allowing the users to expand or collapse the rows of the parent grid, revealing the according child grid, when more detailed information is needed.</p>

### Demo

<div class="sample-container loading" style="height:520px">
    <iframe id="grid-sample-iframe" src='{environment:demosBaseUrl}/hierarchical-grid/hierarchical-grid-resizing' width="100%" height="100%" seamless frameBorder="0" onload="onSampleIframeContentLoaded(this);"></iframe>
</div>
<br/>
<div>
<button data-localize="stackblitz" disabled class="stackblitz-btn" data-iframe-id="grid-sample-iframe" data-demos-base-url="{environment:demosBaseUrl}">view on stackblitz</button>
</div>
<div class="divider--half"></div>

### Dependencies
The Hierarchical Grid is exported as an `NgModule` - all you need to do in your application is import the _IgxHierarchicalGridModule_ inside your `AppModule`.

```typescript
// app.module.ts

import { IgxHierarchicalGridModule } from 'igniteui-angular';

@NgModule({
    imports: [
        ...
        IgxHierarchicalGridModule,
        ...
    ]
})
export class AppModule {}
```

We can obtain a reference to the Hierarchical Grid in TypeScript the following way:

```typescript
@ViewChild('hgrid1', { read: IgxHierarchicalGridComponent })
public hgrid1: IgxHierarchicalGridComponent;
```

### Data Binding

**igx-hierarchical-grid** derives from **igx-grid** and shares most of its functionality. The main difference is that it allows multiple levels of hierarchy to be defined. They are configured through a separate tag within the definition of **igx-hierarchical-grid**, called **igx-row-island**. The **igx-row-island** component defines the configuration for each child grid for the particular level. Multiple row islands per level are also supported.
The Hierarchical Grid supports two ways of binding to data: 

#### 1. Using hierarchical data

If the application loads the whole hierarchical data as an array of objects referencing children arrays of objects, then the Hierarchical Grid can be configured to read it and bind to it automatically. Here is an example of a properly structured hierarchical data source:

```javascript
export const singers = [{
    "Artist": "Naomí Yepes",
    "Photo": "assets/images/hgrid/naomi.png",
    "Debut": "2011",
    "Grammy Nominations": 6,
    "Grammy Awards": 0,
    "Tours": [{
        "Tour": "Faithful Tour",
        "Started on": "Sep-12",
        "Location": "Worldwide",
        "Headliner": "NO",
        "Toured by": "Naomí Yepes"
    }],
    "Albums": [{
        "Album": "Dream Driven",
        "Launch Date": new Date("August 25, 2014"),
        "Billboard Review": "81",
        "US Billboard 200": "1",
        "Artist": "Naomí Yepes",
        "Songs": [{
            "No.": "1",
            "Title": "Intro",
            "Released": "*",
            "Genre": "*",
            "Album": "Dream Driven"
        }]
    }]
}];
```
Each **igx-row-island** should specify the key of the property that holds the children data.

```html
<igx-hierarchical-grid #hierarchicalGrid [data]="singers" [autoGenerate]="true">
    <igx-row-island [key]="'Albums'" [autoGenerate]="true">
        <igx-row-island [key]="'Songs'" [autoGenerate]="true">
        </igx-row-island>
    </igx-row-island>
    <igx-row-island [key]="'Tours'" [autoGenerate]="true">
    </igx-row-island>
</igx-hierarchical-grid>
```
> [!NOTE]
> Note that instead of `data` the user configures only the `key` that the **igx-hierarchical-grid** needs to read to set the data automatically.

#### 2. Using Load-On-Demand

Most applications are designed to load as little data as possible initially, which results in faster load times. In such cases **igx-hierarchical-grid** may be configured to allow user-created services to feed it with data on demand. The following configuration uses a special `@Output` and a newly introduced loading-in-progress template to provide a fully-featured load-on-demand.

```html
<!-- hierarchicalGridSample.component.html -->

    <igx-hierarchical-grid #hGrid [primaryKey]="'CustomerID'" [autoGenerate]="true" [height]="'600px'" [width]="'100%'">
        <igx-row-island [key]="'Orders'" [primaryKey]="'OrderID'" [autoGenerate]="true"  (onGridCreated)="gridCreated($event, 'CustomerID')">
            <igx-row-island [key]="'Order_Details'" [primaryKey]="'ProductID'" [autoGenerate]="true" (onGridCreated)="gridCreated($event, 'OrderID')">
            </igx-row-island>
        </igx-row-island>
    </igx-hierarchical-grid>
```

```typescript
//  hierarchicalGridSample.component.ts

export class HierarchicalGridLoDSampleComponent implements AfterViewInit {
    @ViewChild("hGrid")
    public hGrid: IgxHierarchicalGridComponent;

    constructor(private remoteService: RemoteLoDService) { }

    public ngAfterViewInit() {
        this.hGrid.isLoading = true;
        this.remoteService.getData({ parentID: null, rootLevel: true, key: "Customers" }).subscribe((data) => {
            this.hGrid.isLoading = false;
            this.hGrid.data = data;
            this.hGrid.cdr.detectChanges();
        });
    }

    public gridCreated(event: IGridCreatedEventArgs, _parentKey: string) {
        const dataState = {
            key: event.owner.key,
            parentID: event.parentID,
            parentKey: _parentKey,
            rootLevel: false
        };
        event.grid.isLoading = true;
        this.remoteService.getData(dataState).subscribe(
            (data) => {
                event.grid.isLoading = false;
                event.grid.data = data;
                event.grid.cdr.detectChanges();
            }
        );
    }
}
```

```typescript
// remote-load-on-demand.service.ts

@Injectable()
export class RemoteLoDService {
    public url = `https://services.odata.org/V4/Northwind/Northwind.svc/`;

    constructor(private http: HttpClient) { }

    public getData(dataState?: any): Observable<any[]> {
        return this.http.get(this.buildUrl(dataState)).pipe(
            map((response) => response["value"])
        );
    }

    public buildUrl(dataState) {
        let qS = "";
        if (dataState) {
            qS += `${dataState.key}?`;

            if (!dataState.rootLevel) {
                if (typeof dataState.parentID === "string") {
                    qS += `$filter=${dataState.parentKey} eq '${dataState.parentID}'`;
                } else {
                    qS += `$filter=${dataState.parentKey} eq ${dataState.parentID}`;
                }
            }
        }
        return `${this.url}${qS}`;
    }
}
```
### Features

The grid features could be enabled and configured through the **igx-row-island** markup - they get applied for every grid that is created for it. Changing options at runtime through the row island instance changes them for each of the grids it has spawned. 

```html
<igx-hierarchical-grid [data]="localData" [displayDensity]="density" [autoGenerate]="false"
    [allowFiltering]='true' [paging]="true" [height]="'600px'" [width]="'800px'" #hGrid>
    <igx-column field="ID" [pinned]="true" [filterable]='true'></igx-column>
    <igx-column-group header="Information">
        <igx-column field="ChildLevels"></igx-column>
        <igx-column field="ProductName" hasSummary='true'></igx-column>
    </igx-column-group>
    <igx-row-island [key]="'childData'" [autoGenerate]="false" [rowSelectable]='true' #layout1>
        <igx-column field="ID" [hasSummary]='true' [dataType]="'number'"></igx-column>
        <igx-column-group header="Information2">
            <igx-column field="ChildLevels"></igx-column>
            <igx-column field="ProductName"></igx-column>
        </igx-column-group>
    </igx-row-island>
</igx-hierarchical-grid>
```

The following grid features work on a per grid level, which means that each grid instance manages them independently of the rest of the grids:

- Sorting
- Filtering
- Paging
- Multi Column Headers
- Hiding
- Pinning
- Moving
- Summaries
- Search

The Selection and Navigation features work globally for the whole **igx-hierarchical-grid** 

- Selection 
    Selection does not allow selected cells to be present for two different child grids at once.
- Navigation
    When navigating up/down, if next/prev element is a child grid, navigation will continue in the related child grid, marking the related cell as selected and focused. If the child cell is outside the current visible view port it is scrolled into view so that selected cell is always visible.

### Keyboard navigation
Keyboard navigation is supported by default by the Hierarchical Grid. When you focus a cell and press one of the following key combinations, the described behaviour is performed:

 - `Arrow Up` - navigates one cell up, going up the grid hierarchy if necessary (no wrapping);
 - `Arrow Down` - navigates one cell down, going deeper into the grid hierarchy if necessary (no wrapping);
 - `Arrow Left` - navigates one cell left (no wrapping between lines);
 - `Arrow Right` - navigates one cell right (no wrapping between lines);
 - `Ctrl + Arrow Up` - navigates to the first cell in the current column;
 - `Ctrl + Arrow Down` - navigates to the last cell in the current column;
 - `Ctrl + Arrow Left` -  moves to leftmost cell in the row;
 - `Home` - moves to leftmost cell in the row;
 - `Ctrl + Home` - moves to top left cell in the grid;
 - `Ctrl + Arrow Right` - moves to rightmost cell in the row;
 - `End` - moves to rightmost cell in the row;
 - `Ctrl + End` - moves to bottom right cell in the grid;
 - `Page Up` - scrolls one page (view port) up;
 - `Page Down` -  scrolls one page (view port) down;
 - `Enter` - enters edit mode;
 - `F2` - enters edit mode;
 - `Esc` - exits edit mode;
 - `Tab` - sequentially moves the focus over the next cell on the row and if the last cell is reached, moves to the next row. If the focus is on the last cell of an expanded row, moves the focus inside its first child; When a cell is in edit mode, will move the focus to next editable cell in the row, and from the right-most editable cell to the `CANCEL` and `DONE` buttons, and from the `DONE` button to the left-most editable cell within the currently edited row;
 - `Shift + Tab` - sequentially moves focus to the previous cell on the row and if the first cell is reached, moves the focus to the previous row. If the focus is on the first cell of an expanded child grid, moves the focus inside its parent; When a cell is in edit mode, will move the focus to the next editable cell in the row, and from the right-most editable cell to the `CANCEL` and `DONE` buttons, and from the `DONE` button to the left-most editable cell within the currently edited row;
 - `Space` -  if the row is selectable, on keydown space triggers row selection;
 - `Alt + Arrow Left` on a parent grid row - collapses the parent row content if the row is not already collapsed;
 - `Alt + Arrow Up` on a parent grid row - collapses the parent row content if the row is not already collapsed;
 - `Alt + Arrow Right` on a parent grid row - expands the parent row content if the row is not already expanded;
 - `Alt + Arrow Down` on a parent grid row - expands the parent row content if the row is not already expanded;
 - on mouse `wheel` -  blurs the focused element;


#### "Collapse All" Button

The Hierarchical Grid allows the users to conveniently collapse all its currently expanded rows by pressing the "Collapse All" button at its top left corner. Additionally, every child grid which contains other grids and is a Hierarchical Grid itself, also has such a button - this way the user is able to collapse only a given grid in the hierarchy: 

![](../../images/unfold_less_icon_screenshot.jpg)

### Known Limitations

|Limitation|Description|
|--- |--- |
|Group By|Group By feature is not supported by the hierarchical grid.|
|Export to Excel|Export to Excel is currently not supported by the Hierarchical Grid, but it would be available in future versions of Ignite UI for Angular.|

### CRUD operations

> [!NOTE]
> An important difference from the flat Data Grid is that each instance for a given row island has the same transaction service instance and accumulates the same transaction log. In order to enable the CRUD functionality users should inject the `IgxHierarchicalTransactionServiceFactory`.

Calling CRUD API methods should still be done through each separate grid instance.

## API References

* [IgxHierarchicalGridComponent]({environment:angularApiUrl}/classes/igxhierarchicalgridcomponent.html)
* [IgxRowIslandComponent]({environment:angularApiUrl}/classes/igxrowislandcomponent.html)
* [IgxGridComponent]({environment:angularApiUrl}/classes/igxgridcomponent.html)
* [IgxGridComponent Styles]({environment:sassApiUrl}/#function-igx-grid-theme)
* [IgxColumnComponent]({environment:angularApiUrl}/classes/igxcolumncomponent.html)
* [IgxGridRowComponent]({environment:angularApiUrl}/classes/igxgridrowcomponent.html)
* [IgxGridCellComponent]({environment:angularApiUrl}/classes/igxgridcellcomponent.html)

### Additional Resources
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