@@if (igxName === 'IgxGrid') {
---
title: Grid Paging
_description: The Ignite UI for Angular Data Grid control features the fastest, touch-responsive data-rich grid with popular features, including hierarchical and list views.
_keywords: Ignite UI for Angular, UI controls, Angular widgets, web widgets, UI widgets, Angular, Native Angular Components Suite, Native Angular Controls, Native Angular Components Library, Angular Grid, Angular Table, Angular Data Grid component, Angular Data Table component, Angular Data Grid control, Angular Data Table control, Angular Grid component, Angular Table component, Angular Grid control, Angular Table control, Angular High Performance Grid, Angular High Performance Data Table, Paging, Pagination, Data Grid Paging, Data Table Paging
---
}
@@if (igxName === 'IgxTreeGrid') {
---
title: Tree Grid Paging
_description: The Ignite UI for Angular Tree Grid control features the fastest, touch-responsive data-rich tree grid with popular features, including hierarchical and list views.
_keywords: Ignite UI for Angular, UI controls, Angular widgets, web widgets, UI widgets, Angular, Native Angular Components Suite, Native Angular Controls, Native Angular Components Library, Angular Tree Grid, Angular Tree Table, Angular Tree Grid component, Angular Tree Table component, Angular Tree Grid control, Angular Tree Table control, Angular Tree Grid component, Angular Tree Table component, Angular Tree Grid control, Angular Tree Table control, Angular High Performance Tree Grid, Angular High Performance Tree Table, Paging, Pagination, Tree Grid Paging, Tree Table Paging
---
}
@@if (igxName === 'IgxHierarchicalGrid') {
---
title: Hierarchical Grid Paging
_description: The Ignite UI for Angular Hierarchical Grid control features the fastest, touch-responsive data-rich tree grid with popular features.
_keywords: Ignite UI for Angular, UI controls, Angular widgets, web widgets, UI widgets, Angular, Native Angular Components Suite, Native Angular Controls, Native Angular Components Library, Angular Hierarchical Grid, Angular Hierarchical Table, Angular Hierarchical Grid component, Angular Hierarchical Table component, Angular Hierarchical Grid control, Angular Hierarchical Table control, Angular High Performance Hierarchical Grid, Angular High Performance Hierarchical Table, Paging, Pagination, Hierarchical Grid Paging, Hierarchical Table Paging
---
}

### @@igComponent Paging

In Ignite UI for Angular @@igComponent, **Paging** is initialized on the root `@@igSelector` component and is configurable via the [`paging`]({environment:angularApiUrl}/classes/@@igTypeDoc.html#paging) and [`perPage`]({environment:angularApiUrl}/classes/@@igTypeDoc.html#perpage) inputs.

#### Demo

@@if (igxName === 'IgxGrid') {
<div class="sample-container loading" style="height:550px">
    <iframe id="grid-paging-sample-iframe" src='{environment:demosBaseUrl}/grid/grid-paging-sample' width="100%" height="100%" seamless frameBorder="0" onload="onSampleIframeContentLoaded(this);"></iframe>
</div>
<br/>
<div>
<button data-localize="stackblitz" disabled class="stackblitz-btn" data-iframe-id="grid-paging-sample-iframe" data-demos-base-url="{environment:demosBaseUrl}">view on stackblitz</button>
</div>
}
@@if (igxName === 'IgxTreeGrid') {
<div class="sample-container loading" style="height:550px">
    <iframe id="treegrid-paging-sample-iframe" src='{environment:demosBaseUrl}/tree-grid/treegrid-paging' width="100%" height="100%" seamless frameBorder="0" onload="onSampleIframeContentLoaded(this);"></iframe>
</div>
<br/>
<div>
<button data-localize="stackblitz" disabled class="stackblitz-btn" data-iframe-id="treegrid-paging-sample-iframe" data-demos-base-url="{environment:demosBaseUrl}">view on stackblitz</button>
</div>
}
@@if (igxName === 'IgxHierarchicalGrid') {
<div class="sample-container loading" style="height:560px">
    <iframe id="hierarchical-grid-paging-sample-iframe" src='{environment:demosBaseUrl}/hierarchical-grid/hierarchical-grid-paging' width="100%" height="100%" seamless frameBorder="0" onload="onSampleIframeContentLoaded(this);"></iframe>
</div>
<br/>
<div>
<button data-localize="stackblitz" disabled class="stackblitz-btn" data-iframe-id="hierarchical-grid-paging-sample-iframe" data-demos-base-url="{environment:demosBaseUrl}">view on stackblitz</button>
</div>
<div class="divider--half"></div>
}


Paging is a Boolean property that controls whether the feature is enabled, and the [`perPage`]({environment:angularApiUrl}/classes/@@igTypeDoc.html#perpage) property controls the visible records per page. Let’s update our @@igComponent to enable paging:

```html
<@@igSelector #@@igObjectRef [data]="data" [paging]="true" [perPage]="10" [paginationTemplate]="pager" height="500px" width="100%" displayDensity="cosy">
</@@igSelector>
```

The paging area supports templating by the user, if a template reference is passed to the @@igComponent during initialization. The example below is a template where the pagination is controlled through an input.

```html
<ng-template #myTemplate let-grid>
    Current page: {{ @@igObjectRef.page }}
    <input type="number" [ngModel]="grid.page" (onModelChange)="@@igObjectRef.paginate($event)" />
    Total pages: {{ @@igObjectRef.totalPages }}
</ng-template>

<@@igSelector [paging]="true" [paginationTemplate]="myTemplate">
    ...
</@@igSelector>
```

Paging can also be done programmatically through the @@igComponent API, using the [`paginate`]({environment:angularApiUrl}/classes/@@igTypeDoc.html#paginate), [`previousPage`]({environment:angularApiUrl}/classes/@@igTypeDoc.html#previouspage), [`nextPage`]({environment:angularApiUrl}/classes/@@igTypeDoc.html#nextpage) methods:

```typescript
// Go to page 6
this.@@igObjectRef.paginate(5);

// Go to previous/next page
this.@@igObjectRef.previousPage();
this.@@igObjectRef.nextPage();

// Check for first/last page
this.@@igObjectRef.isFirstPage;
this.@@igObjectRef.isLastPage;

// Get the number of pages
this.@@igObjectRef.totalPages;

// Change the number of records per page
this.@@igObjectRef.perPage = 25;

// Enables/disables paging
this.@@igObjectRef.paging = false;
```

@@if (igxName === 'IgxGrid' || igxName === 'IgxHierarchicalGrid') {
### Remote Data

Paging could also operate with remote data.

Lets first declare our service that will be responsible for data fetching.
We will need the count of all the data items in order to calculate pages count and we will add this logic to our service.
```typescript
@Injectable()
export class RemoteService {
    public remoteData: BehaviorSubject<any[]>;
    private url: string = "https://www.igniteui.com/api/products";

    constructor(private http: HttpClient) {
        this.remoteData = new BehaviorSubject([]);
    }

    public getData(index?: number, perPage?: number): any {
        let qS = "";

        if (perPage) {
            qS = `?$skip=${index}&$top=${perPage}&$count=true`;
        }

        this.http
            .get(`${this.url + qS}`).pipe(
                map((data: any) => {
                    return data;
                })
            ).subscribe((data) => this.remoteData.next(data));
    }

    public getDataLength(): any {
        return this.http.get(this.url).pipe(
            map((data: any) => {
                return data.length;
            })
        );
    }
}
```
After declaring the service, we need to create a component, which will be responsible for the @@igComponent construction and data subscription.
@@if (igxName === 'IgxGrid') {
```typescript
export class RemotePagingGridSample implements OnInit, AfterViewInit {
    public data: Observable<any[]>;

    constructor(private remoteService: RemoteService) {}

    public ngOnInit() {
        this.data = this.remoteService.remoteData.asObservable();
        this._dataLengthSubscriber = this.remoteService.getDataLength().subscribe((data) => {
            this.totalCount = data;
            this.totalPages = Math.ceil(data / this.perPage);
            this.buttonDeselection(this.page, this.totalPages);
        });
    }
}
```
}
@@if (igxName === 'IgxHierarchicalGrid') {
```typescript
export class HGridRemotePagingSampleComponent implements OnInit, AfterViewInit, OnDestroy {
    public page = 0;
    public lastPage = false;
    public firstPage = true;
    public totalPages: number = 1;
    public totalCount = 0;
    
    constructor(private remoteService: RemotePagingService) {}

    public ngOnInit(): void {
        this._dataLengthSubscriber = this.remoteService.getDataLength(
            { parentID: null, rootLevel: true, key: "Customers" }).subscribe((length) => {
            this.totalCount = length;
            this.totalPages = Math.ceil(length / this.perPage);
            this.buttonDeselection(this.page, this.totalPages);
        });
    }
}
```
}
We need to create a custom pager template to get the data only for the requested page and to pass the correct `skip` and `top` parameters to the remote service according to the selected page and items [`perPage`]({environment:angularApiUrl}/classes/@@igTypeDoc.html#perpage).
We also need to take care of the disabling and enabling of the pager buttons.

@@if (igxName === 'IgxGrid') {
```html
<ng-template #customPager>
    <button [disabled]="firstPage" (click)="paginate(0, false)" igxButton="icon" igxRipple igxRippleCentered="true">
        <igx-icon fontSet="material">first_page</igx-icon>
    </button>
    <button [disabled]="firstPage" (click)="previousPage()" igxButton="icon" igxRipple igxRippleCentered="true">
        <igx-icon fontSet="material">chevron_left</igx-icon>
    </button>
    <span>{{ page + 1 }} of {{totalPages}}</span>
    <button [disabled]="lastPage" (click)="nextPage()" igxRipple igxRippleCentered="true" igxButton="icon">
        <igx-icon fontSet="material">chevron_right</igx-icon>
    </button>
    <button [disabled]="lastPage" (click)="paginate(totalPages - 1, false)" igxButton="icon" igxRipple igxRippleCentered="true">
        <igx-icon fontSet="material">last_page</igx-icon>
    </button>
    <select style="margin-left: 1rem;" (change)="perPage = parseToInt($event.target.value);">
        <option [value]="val" [selected]="perPage == val" *ngFor="let val of [5, 10, 15, 25, 50, 100, 500]">{{ val }}</option>
    </select>
</ng-template>
```

```typescript
@ViewChild("customPager", { read: TemplateRef })
public remotePager: TemplateRef<any>;

public nextPage() {
    this.firstPage = false;
    this.page++;
    const skip = this.page * this.perPage;
    const top = this.perPage;
    this.remoteService.getData(skip, top);
    if (this.page + 1 >= this.totalPages) {
        this.lastPage = true;
    }
}

public previousPage() {
    this.lastPage = false;
    this.page--;
    const skip = this.page * this.perPage;
    const top = this.perPage;
    this.remoteService.getData(skip, top);
    if (this.page <= 0) {
        this.firstPage = true;
    }
}

public paginate(page: number, recalc: true) {
    this.page = page;
    const skip = this.page * this.perPage;
    const top = this.perPage;
    if (recalc) {
        this.totalPages = Math.ceil(this.totalCount / this.perPage);
    }
    this.remoteService.getData(skip, top);
    this.buttonDeselection(this.page, this.totalPages);
}

public buttonDeselection(page: number, totalPages: number) {
...
}

...
public ngAfterViewInit() {
    this.remoteService.getData(0, this.perPage);
    this.@@igObjectRef.paginationTemplate = this.remotePager;
}

```
}
@@if (igxName === 'IgxHierarchicalGrid') {
```html
<ng-template #customPager let-api>
    <button [disabled]="firstPage" (click)="paginate(0, false)" igxButton="icon" igxRipple igxRippleCentered="true">
        <igx-icon fontSet="material">first_page</igx-icon>
    </button>
    <button [disabled]="firstPage" (click)="previousPage()" igxButton="icon" igxRipple igxRippleCentered="true">
        <igx-icon fontSet="material">chevron_left</igx-icon>
    </button>
    <span>{{ page + 1 }} of {{totalPages}}</span>
    <button [disabled]="lastPage" (click)="nextPage()" igxRipple igxRippleCentered="true" igxButton="icon">
        <igx-icon fontSet="material">chevron_right</igx-icon>
    </button>
    <button [disabled]="lastPage" (click)="paginate(totalPages - 1, false)" igxButton="icon" igxRipple
        igxRippleCentered="true">
        <igx-icon fontSet="material">last_page</igx-icon>
    </button>
    <select style="margin-left: 1rem;" (change)="parseToInt($event.target.value);">
        <option [value]="val" [selected]="perPage == val" *ngFor="let val of [5, 10, 15, 20]">{{ val
            }}</option>
    </select>
</ng-template>
```
```typescript
@ViewChild("customPager", { read: TemplateRef })
public remotePager: TemplateRef<any>;
public title = "gridPaging";
    
@ViewChild("layout1")
public layout1: IgxRowIslandComponent;

@ViewChild("hierarchicalGrid")
public hierarchicalGrid: IgxHierarchicalGridComponent;
    
...
    
public ngAfterViewInit() {
    this.hierarchicalGrid.isLoading = true;
    this.remoteService.getData(
        { parentID: null, rootLevel: true, key: "Customers" }, 0, this.perPage).subscribe((data) => {
        this.hierarchicalGrid.isLoading = false;
        this.hierarchicalGrid.data = data;
        this.hierarchicalGrid.paginationTemplate = this.remotePager;
        this.hierarchicalGrid.cdr.detectChanges();
    });
}

...

public nextPage() {
    this.firstPage = false;
    this.page++;
    const skip = this.page * this.perPage;
    const top = this.perPage;
    this.remoteService.getData(
        { parentID: null, rootLevel: true, key: "Customers" }, skip, top).subscribe((data) => {
        this.hierarchicalGrid.data = data;
        this.hierarchicalGrid.cdr.detectChanges();
    });
    if (this.page + 1 >= this.totalPages) {
        this.lastPage = true;
    }
}

public previousPage() {
    this.lastPage = false;
    this.page--;
    const skip = this.page * this.perPage;
    const top = this.perPage;
    this.remoteService.getData(
        { parentID: null, rootLevel: true, key: "Customers" }, skip, top).subscribe((data) => {
        this.hierarchicalGrid.data = data;
        this.hierarchicalGrid.cdr.detectChanges();
    });
    if (this.page <= 0) {
        this.firstPage = true;
    }
}

public paginate(page: number, recalc: true) {
    this.page = page;
    const skip = this.page * this.perPage;
    const top = this.perPage;
    if (recalc) {
        this.totalPages = Math.ceil(this.totalCount / this.perPage);
    }
    this.remoteService.getData(
        { parentID: null, rootLevel: true, key: "Customers" }, skip, top).subscribe((data) => {
        this.hierarchicalGrid.data = data;
        this.hierarchicalGrid.cdr.detectChanges();
    });
    this.buttonDeselection(this.page, this.totalPages);
}

public buttonDeselection(page: number, totalPages: number) {
    ...
}

```
}
The last step will be to declare our template for the gird.
@@if (igxName === 'IgxGrid') {
```html
<@@igSelector #@@igObjectRef [data]="data | async" width="960px" height="550px" [paging]="true" [perPage]="perPage">
    <igx-column field="ID"></igx-column>
    <igx-column field="ProductName"></igx-column>
    <igx-column field="QuantityPerUnit"></igx-column>
    <igx-column field="SupplierName"></igx-column>
    <igx-column field="UnitsInStock"></igx-column>
    <igx-column field="Rating"></igx-column>
</@@igSelector>
```
}
@@if (igxName === 'IgxHierarchicalGrid') {
```html
<igx-hierarchical-grid [paging]="true" [perPage]="perPage"
    [primaryKey]="'CustomerID'" [height]="'550px'" [width]="'100%'" #hierarchicalGrid>
    <igx-column field="CustomerID"></igx-column>
        <igx-column field="CompanyName"></igx-column>
        <igx-column field="ContactName"></igx-column>
        <igx-column field="ContactTitle"></igx-column>
        <igx-column field="Country"></igx-column>
        <igx-column field="Phone"></igx-column>
        ...
</igx-hierarchical-grid>
```
}
This is absolutely enough if we want an up and running sample. But we can extend this sample even more by adding an option to change our paging template at run time. Let's see how we can achieve that. First we will start by adding one more paging template in our template:

```html
<ng-template #secCustomPager let-api>
    <button [disabled]="firstPage" (click)="previousPage()" igxButton="flat" igxButtonColor="#09f">
        PREV
    </button>
    <span *ngIf="shouldShowFirstPage" (click)="paginate(0, false)"><a class="pageNavLinks" [routerLink]=''>{{1}}</a> ...</span>
    <span *ngFor="let item of pages" (click)="paginate(item, false)">
        <a class="pageNavLinks {{activePage(item)}}" [routerLink]=''>{{item + 1}}</a>
    </span>
    <span *ngIf="shouldShowLastPage" (click)="paginate(totalPages - 1, false)">... <a class="pageNavLinks" [routerLink]=''>{{ totalPages }}</a></span>
    <button [disabled]="lastPage" (click)="nextPage()"  igxButton="flat" igxButtonColor="#09f">
        NEXT
    </button>
</ng-template>
```

After that we need to extend the methods that we have already created with some additional logic:

```typescript
// the same also applies for the methods previousPage() and paginate(page: number, recalc: true)
public nextPage() {
    ...
    if (this.grid1.paginationTemplate === this.secondPagerTemplate) {
        this.setNumberOfPagingItems(this.page, this.totalPages);
    }
}
// creates an array with the visible page numbers where the user can navigate according to the current page and the total page number
public setNumberOfPagingItems(currentPage, totalPages) {
    ....
}
```
And finally we need to add a button which allows the user to change the pager template at run time:

```html
<button (click)="changeTemplate()" class='changeBtn' igxButton="flat"
    igxButtonColor="#09f" igxButtonBackground="#dadada">Change Paging Template</button>
```

```typescript
public changeTemplate() {
    if (this.grid1.paginationTemplate === this.remotePager) {
        this.grid1.paginationTemplate = this.secondPagerTemplate;
        this.setNumberOfPagingItems(this.page, this.totalPages);
    } else {
        this.pages = [];
        this.grid1.paginationTemplate = this.remotePager;
    }
    this.grid1.cdr.detectChanges();
}
```

After all the changes above, the following result will be achieved.

#### Demo
@@if (igxName === 'IgxGrid') {
<div class="sample-container loading" style="height:650px">
    <iframe id="grid-remote-paging-sample-iframe" data-src='{environment:demosBaseUrl}/grid/grid-remote-paging-sample' width="100%" height="100%" seamless="" frameBorder="0" class="lazyload"></iframe>
</div>
<br/>
<div>
<button data-localize="stackblitz" disabled class="stackblitz-btn" data-iframe-id="grid-remote-paging-sample-iframe" data-demos-base-url="{environment:demosBaseUrl}">view on stackblitz</button>
</div>
}
@@if (igxName === 'IgxHierarchicalGrid') {
<div class="sample-container loading" style="height:560px">
    <iframe id="hierarchical-grid-remote-paging-sample-iframe" data-src='{environment:demosBaseUrl}/hierarchical-grid/hierarchical-grid-remote-paging' width="100%" height="100%" seamless="" frameBorder="0" class="lazyload"></iframe>
</div>
<br/>
<div>
<button data-localize="stackblitz" disabled class="stackblitz-btn" data-iframe-id="hierarchical-grid-remote-paging-sample-iframe" data-demos-base-url="{environment:demosBaseUrl}">view on stackblitz</button>
</div>
<div class="divider--half"></div>
}

If you want your sample to look exactly like this one, do not forget to apply the custom paging theme:

```css
@import '~igniteui-angular/lib/core/styles/themes/index';

@include igx-core();
@include igx-theme($default-palette, $legacy-support: true);


$custom-paginator-theme: igx-grid-paginator-theme(
    $text-color: #09f
);
$custom-button-theme: igx-button-theme(
    $icon-color: #09f,
    $icon-hover-color: #dadada,
    $icon-focus-color:rgb(0, 119, 255),
    $icon-focus-background: #aeaeae
);

.customPager {
    @include igx-grid-paginator($custom-paginator-theme);
    @include igx-button($custom-button-theme);
}
```
}
### API References
* [@@igxNameComponent API]({environment:angularApiUrl}/classes/@@igTypeDoc.html)
* [@@igxNameComponent Styles]({environment:sassApiUrl}/index.html#function-igx-grid-theme)
* [IgxGridPaginator Styles]({environment:sassApiUrl}/index.html#function-igx-grid-paginator-theme)

### Additional Resources
<div class="divider--half"></div>

* [@@igComponent overview](@@igMainTopic.md)
* [Virtualization and Performance](virtualization.md)
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
