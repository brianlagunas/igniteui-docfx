---
title: Paste from Excel - Native Angular | Ignite UI for Angular
_description: Users can paste data into igxGrid that is copied from Excel.
_keywords: Ignite UI for Angular, UI controls, Angular widgets, web widgets, UI widgets, Angular, Native Angular Controls, Native Angular Components Suite, Native Angular Controls, Native Angular Components Library, Angular Grid, Angular Data Grid, Angular Grid Control, Angular Grid Component, Paste from Excel, Angular Paste from Excel
---

### Paste from Excel

The Ignite UI for Angular [`IgxGrid`]({environment:angularApiUrl}/classes/igxgridcomponent.html) can read Excel data that is copied to the clipboard. In this section we will show you how to do this with some custom code.

#### Paste from Excel Demo

This sample demonstrates how to implement pasting from Excel into the [`igxGrid`]({environment:angularApiUrl}/classes/igxgridcomponent.html).
To work with the sample open up any Excel spreadsheet, copy some rows, and paste it into the grid using the keyboard (Ctrl + V, Shift + Insert, Command + V).

On the top there is a dropdown button with 2 options:
<ol>
<li>"Paste data as new rows" – in this mode any data copied from Excel will be appended to the grid as new rows</li>
<li>"Paste starting from active cell" – in this mode the data in the grid will be overwritten.</li>
</ol>

The new data after the paste is decorated in Italic.

<div class="sample-container loading" style="height: 570px;">
    <iframe id="excel-paste-sample-iframe" src="{environment:demosBaseUrl}/grid/grid-paste"
        width="100%" height="100%" seamless frameBorder="0" onload="onSampleIframeContentLoaded(this);"></iframe>
</div>
<div>
<button data-localize="stackblitz" disabled class="stackblitz-btn" data-iframe-id="excel-paste-sample-iframe"
    data-demos-base-url="{environment:demosBaseUrl}">view on stackblitz</button>
</div>
<div class="divider"></div>

#### Usage

You should add the `paste-handler` directive (you can find its code in the next section) to the [`igxGrid`]({environment:angularApiUrl}/classes/igxgridcomponent.html) and handle its `onDataProcessed` event. The `onDataProcessed` event has one parameter that gives you access to the Excel data in the form of an array. For reference see the `addRecords` and `updateRecords` methods.

```html
<igx-grid #grid1 [data]="data" [width]="'100%'" [height]="'505px'" [autoGenerate]="false" paste-handler (onDataProcessed)="dataPasted($event)" [primaryKey]="'ID'">
    <igx-column [field]="'Name'"></igx-column>
    <igx-column [field]="'Title'"></igx-column>
    <igx-column [field]="'Phone'"></igx-column>
    <igx-column [field]="'Country'"></igx-column>
</igx-grid>
```

```typescript
    public dataPasted(processedData) {
        if (this.pasteMode === "Paste data as new records") {
            this.addRecords(processedData);
        } else {
            this.updateRecords(processedData);
        }
    }

    public addRecords(processedData: any[]) {
        const columns = this.grid1.visibleColumns;
        const pk = this.grid1.primaryKey;
        const addedData = [];
        for (const curentDataRow of processedData) {
            const rowData = {};
            for (const col of columns) {
                rowData[col.field] = curentDataRow[col.visibleIndex];
            }
            // generate PK
            rowData[pk] = this.grid1.data.length + 1;
            this.grid1.addRow(rowData);
            addedData.push(rowData);
            this.grid1.cdr.detectChanges();
        }
        // scroll to last added row
        this.grid1.verticalScrollContainer.scrollTo(this.grid1.data.length);

        this.grid1.verticalScrollContainer.onChunkLoad.pipe(take(1)).subscribe(() => {
            this.clearStyles();
            for (const data of addedData) {
                const row = this.grid1.getRowByKey(data[pk]);
                if (row) {
                    row.nativeElement.style["font-style"] = "italic";
                    row.nativeElement.style.color = "gray";
                }
            }
        });
    }
    public updateRecords(processedData: any[]) {
        const cell = this.grid1.selectedCells[0];
        const pk = this.grid1.primaryKey;
        if (!cell) { return; }
        const rowIndex = cell.row.index;
        // const rowPkValue = cell.row.rowData[pk];
        const cellIndex = cell.column.visibleIndex;
        const columns = this.grid1.visibleColumns;
        let index = 0;
        const updatedRecsPK = [];
        for (const curentDataRow of processedData) {
            const rowData = {};
            const dataRec = this.grid1.data[rowIndex + index];
            const rowPkValue = dataRec ? dataRec[pk] : this.grid1.data.length + 1;
            rowData[pk] = rowPkValue;
            for (let j = 0; j < columns.length; j++) {
                let currentCell;
                if (j >= cellIndex) {
                    currentCell = curentDataRow.shift();
                }
                const colKey = columns[j].field;
                rowData[colKey] = currentCell || (!!dataRec ? dataRec[colKey] : null);
            }
            if (!dataRec) {
                // no rec to update, add instead
                rowData[pk] = rowPkValue;
                this.grid1.addRow(rowData);
                continue;
            }
            this.grid1.updateRow(rowData, rowPkValue);
            this.grid1.cdr.detectChanges();
            updatedRecsPK.push(rowPkValue);
            index++;
        }

        this.clearStyles();
        for (const pkVal of updatedRecsPK) {
            const row = this.grid1.getRowByKey(pkVal);
            if (row) {
            row.nativeElement.style["font-style"] = "italic";
            row.nativeElement.style.color = "gray";
            }
        }
    }

    protected clearStyles() {
        for (const row of this.grid1.rowList.toArray()) {
            row.nativeElement.style["font-style"] = "";
            row.nativeElement.style.color = "";
        }
    }
```
<div class="divider"></div>

#### Paste Handler Directive

This is the `paste-handler` implementation. The code creates a DOM `textarea` element which is used to receive the pasted data from the clipboard. When the data is pasted in the `textarea` the directive parses it into an array and then emits a custom event `onDataProcessed` passing the parsed data.

```typescript
import { Directive, EventEmitter, HostListener, Output} from "@angular/core";

@Directive({ selector: "[paste-handler]" })
export class PasteHandler {
    public textArea;

    @Output()
    public onDataProcessed = new EventEmitter<any>();

    public ngOnInit(): void {
        const div = document.createElement("div");
        const divStyle = div.style;
        divStyle.position = "fixed";
        document.body.appendChild(div);
        this.textArea = document.createElement("textarea");
        const style = this.textArea.style;
        style.opacity = "0";
        style.height = "0px";
        style.width = "0px";
        style.overflow = "hidden";
        div.appendChild(this.textArea);

        this.textArea.addEventListener("paste", (eventArgs) => { this.onPaste(eventArgs); });
    }

    @HostListener("focusin", ["$event"])
    public focusIn(eventArgs) {
    }

    @HostListener("keydown", ["$event"])
    public ControlV(eventArgs) {
        const ctrl = eventArgs.ctrlKey;
        const key = eventArgs.keyCode;
        // Ctrl-V || Shift-Ins || Cmd-V
        if ((ctrl || eventArgs.metaKey) && key === 86 || eventArgs.shiftKey && key === 45) {
            this.textArea.focus();
        }
    }

    public onPaste(eventArgs) {
    let data;
    const clData = "clipboardData";

    // get clipboard data - from window.cliboardData for IE or from the original event's arguments.
    if (window[clData]) {
        window.event.returnValue = false;
        data = window[clData].getData("text");
    } else {
        data = eventArgs[clData].getData("text/plain");
    }

    // process the clipboard data
    const processedData = this.processData(data);

    this.onDataProcessed.emit(processedData);
    }

    public processData(data) {
        const pasteData = data.split("\n");
        for (let i = 0; i < pasteData.length; i++) {
            pasteData[i] = pasteData[i].split("\t");
            // Check if last row is a dummy row
            if (pasteData[pasteData.length - 1].length === 1 && pasteData[pasteData.length - 1][0] === "") {
                pasteData.pop();
            }
            // remove empty data
            if (pasteData.length === 1 &&
                 pasteData[0].length === 1 &&
                  (pasteData[0][0] === "" || pasteData[0][0] === "\r")) {
                    pasteData.pop();
            }
        }
        return pasteData;
    }
}

```

### API References
* [IgxGridComponent]({environment:angularApiUrl}/classes/igxgridcomponent.html)

### Additional Resources
<div class="divider--half"></div>

* [Excel Exporter](export_excel.md)

<div class="divider--half"></div>
Our community is active and always welcoming to new ideas.

* [Ignite UI for Angular **Forums**](https://www.infragistics.com/community/forums/f/ignite-ui-for-angular)
* [Ignite UI for Angular **GitHub**](https://github.com/IgniteUI/igniteui-angular)
