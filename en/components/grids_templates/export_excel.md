@@if (igxName === 'IgxGrid') {
---
title: Export to Excel Component - Native Angular | Ignite UI for Angular
_description: Users can export their data for editing or offline presentation can do so in Excel format with the Export to Excel Ignite UI for Angular component.
_keywords: Ignite UI for Angular, UI controls, Angular widgets, web widgets, UI widgets, Angular, Native Angular Controls, Native Angular Components Suite, Native Angular Controls, Native Angular Components Library, Angular Grid, Angular Data Grid, Angular Grid Control, Angular Grid Component, Excel Export, Angular Excel Component, Angular Export Excel
---
}
@@if (igxName === 'IgxTreeGrid') {
---
title: Export to Excel Component - Native Angular | Ignite UI for Angular
_description: Users can export their data for editing or offline presentation can do so in Excel format with the Export to Excel Ignite UI for Angular component.
_keywords: Ignite UI for Angular, UI controls, Angular widgets, web widgets, UI widgets, Angular, Native Angular Controls, Native Angular Components Suite, Native Angular Controls, Native Angular Components Library, Angular Tree Grid, Angular Tree Grid, Angular Tree Grid Control, Angular Tree Grid Component, Excel Export, Angular Excel Component, Angular Export Excel
---
}
@@if (igxName === 'IgxHierarchicalGrid') {
---
title: Export to Excel Component - Native Angular | Ignite UI for Angular
_description: Users can export their data for editing or offline presentation can do so in Excel format with the Export to Excel Ignite UI for Angular component.
_keywords: Ignite UI for Angular, UI controls, Angular widgets, web widgets, UI widgets, Angular, Native Angular Controls, Native Angular Components Suite, Native Angular Controls, Native Angular Components Library, Angular Hierarchical Grid,, Angular Hierarchical Grid Control, Angular Hierarchical Grid Component, Excel Export, Angular Excel Component, Angular Export Excel
---
}

### @@igComponent Export to Excel

<p class="highlight">
The Excel Exporter service can export data in MS Excel format from the @@igxName. The exporting functionality is encapsulated in the [`IgxExcelExporterService`]({environment:angularApiUrl}/classes/igxexcelexporterservice.html) class and the data is exported in MS Excel table format. This format allows features like filtering, sorting, etc. To do this you need to invoke the [`IgxExcelExporterService`]({environment:angularApiUrl}/classes/igxexcelexporterservice.html)'s [`export`]({environment:angularApiUrl}/classes/igxexcelexporterservice.html#export) method and pass the @@igxName component as first argument.</p>

<div class="divider"></div>

#### Excel Exporter Demo

@@if (igxName === 'IgxGrid') {
<div class="sample-container loading" style="height: 300px;">
    <iframe id="excel-export-sample-iframe" src="{environment:demosBaseUrl}/services/export-excel-sample-1"
        width="100%" height="100%" seamless frameBorder="0" onload="onSampleIframeContentLoaded(this);"></iframe>
</div>
<div>
<button data-localize="stackblitz" disabled class="stackblitz-btn" data-iframe-id="excel-export-sample-iframe"
    data-demos-base-url="{environment:demosBaseUrl}">view on stackblitz</button>
</div>
}
@@if (igxName === 'IgxTreeGrid') {
<div class="sample-container loading" style="height: 350px;">
    <iframe id="excel-export-sample-iframe" src="{environment:demosBaseUrl}/services/export-excel-tree-grid-sample"
        width="100%" height="100%" seamless frameBorder="0" onload="onSampleIframeContentLoaded(this);"></iframe>
</div>
<div>
<button data-localize="stackblitz" disabled class="stackblitz-btn" data-iframe-id="excel-export-sample-iframe"
    data-demos-base-url="{environment:demosBaseUrl}">view on stackblitz</button>
</div>
}
@@if (igxName === 'IgxHierarchicalGrid') {
    <!-- todo -->
}

<div class="divider--half"></div>

#### Exporting @@igComponent's Data

To start using the IgniteUI Excel Exporter first import the [`IgxExcelExporterService`]({environment:angularApiUrl}/classes/igxexcelexporterservice.html) in the app.module.ts file and add the service to the `providers` array:

```typescript
// app.module.ts

...
import { IgxExcelExporterService } from "igniteui-angular/services/index";

@NgModule({
  providers: [ IgxExcelExporterService ]
})

export class AppModule {}
```

> **Note:** The Excel Exporter service has a peer dependency on the JSZip library. The JSZip library should be installed when using the Excel Exporter.

To initiate an export process you may use the handler of a button in your component's template.

```html
<@@igSelector #@@igObjectRef [data]="localData" [autoGenerate]="true"></@@igSelector>
<button (click)="exportButtonHandler()">Export @@igxName to Excel</button>
```

You may access the exporter service by defining an argument of type [`IgxExcelExporterService`]({environment:angularApiUrl}/classes/igxexcelexporterservice.html) in the component's constructor and the Angular framework will provide an instance of the service. To export some data in MS Excel format you need to invoke the exporter service's [`export`]({environment:angularApiUrl}/classes/igxexcelexporterservice.html#export) method and pass the @@igxName component as first argument.

Here is the code which will execute the export process in the component's typescript file:

```typescript
// component.ts

...
import { IgxExcelExporterService, IgxExcelExporterOptions } from "igniteui-angular";
import { @@igxNameComponent } from "igniteui-angular";
...

@ViewChild("@@igObjectRef") public @@igObjectRef: IgxGridComponent;

constructor(private excelExportService: IgxExcelExporterService) {
}

public exportButtonHandler() {
  this.excelExportService.export(this.@@igObjectRef, new IgxExcelExporterOptions("ExportedDataFile"));
}

```

If all went well, you should see the @@igxName component and a button under it. When pressing the button, it will trigger the export process and the browser will download a file named "ExportedDataFile.xlsx" which contains the data from the @@igComponent component in MS Excel format.

#### Customizing the Exported Content

In the above examples the Excel Exporter service was exporting all available data. There are situations in which you may want to skip exporting a row or even an entire column. To achieve this you may hook to the [`onColumnExport`]({environment:angularApiUrl}/classes/igxexcelexporterservice.html#oncolumnexport) and/or [`onRowExport`]({environment:angularApiUrl}/classes/igxexcelexporterservice.html#onrowexport) events which are fired respectively for each column and/or each row and cancel the respective event by setting the event argument object's [`cancel`]({environment:angularApiUrl}/interfaces/irowexportingeventargs.html#cancel) property to `true`.

The following example will exclude a column from the export if its header is "Age" and if its index is 1:

```typescript
// component.ts

this.excelExportService.onColumnExport.subscribe((args: IColumnExportingEventArgs) => {
  if (args.header == "Age" && args.columnIndex == 1) {
      args.cancel = true;
  }
});
this.excelExportService.export(this.@@igObjectRef, new IgxExcelExporterOptions("ExportedDataFile"));
```

When you are exporting data from the @@igComponent component, the export process takes in account features like row filtering and column hiding and exports only the data visible in the @@igComponent. You can configure the exporter service to include filtered rows or hidden columns by setting properties on the [`IgxExcelExporterOptions`]({environment:angularApiUrl}/classes/igxexcelexporteroptions.html) object. These properties are described in the table below.

#### API References

The Excel Exporter service has a few more APIs to explore, which are listed below.

* [IgxExcelExporterService API]({environment:angularApiUrl}/classes/igxexcelexporterservice.html)
* [IgxExcelExporterOptions API]({environment:angularApiUrl}/classes/igxexcelexporteroptions.html)

Additional components that were used:

* [@@igxNameComponent API]({environment:angularApiUrl}/classes/@@igTypeDoc.html)
* [@@igxNameComponent Styles]({environment:sassApiUrl}/index.html#function-igx-grid-theme)

<div class="divider"></div>

#### Additional Resources

<div class="divider--half"></div>
Our community is active and always welcoming to new ideas.

* [Ignite UI for Angular **Forums**](https://www.infragistics.com/community/forums/f/ignite-ui-for-angular)
* [Ignite UI for Angular **GitHub**](https://github.com/IgniteUI/igniteui-angular)
