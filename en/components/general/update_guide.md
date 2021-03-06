---
title: Update Guide
_description: Information on updating to a newer version of the Ignite UI for Angular library.
_keywords: Ignite UI for Angular, update, npm package, version, UI controls, Angular widgets, web widgets, UI widgets, Angular, Native Angular Components Suite, Native Angular Controls, Native Angular Components Library
---

## Update Guide

In the Ignite UI for Angular [versioning](https://github.com/IgniteUI/igniteui-angular/wiki/Ignite-UI-for-Angular-versioning) the first number always matches the major version of Angular the code supports and the second is dedicated for major version releases. Breaking changes may be introduced between major releases.
A comprehensive list of changes for each release of **Ignite UI for Angular** can be found in the product [CHANGELOG](https://github.com/IgniteUI/igniteui-angular/blob/master/CHANGELOG.md)

The Ignite UI for Angular package also supports automatic version migration through `ng update` schematics. Those will attempt to migrate all possible breaking changes (renamed selectors, classes and @Input/Output properties), however there might be still changes that cannot be migrated. Those are usually related to typescript application logic and will be described [additionally below](#additional-manual-changes).

First run the [**`ng update`**](https://angular.io/cli/update) command which will analyze your application and available updates for its packages.
```cmd
ng update
```

> [!NOTE]
> We recommend commit all your changes before proceeding with the update. 

To update the **Ignite UI for Angular** package run the following command:
```cmd
ng update igniteui-angular
```
When you update `igniteui-angular` - it's recommended to update `@angular/core`, `@angular/cli` and `igniteui-cli` packages to their matching versions. 
To update the **Ignite UI CLI** package run the following command:
```cmd
ng update igniteui-cli
```
To update the **Angular Core** package run the following command:
```cmd
ng update @angular/core
```
To update the **Angular CLI** package use the following command:
```cmd
ng update @angular/cli
```

## Additional manual changes


Unfortunately not all changes can be automatically updated. Changes bellow are split into sections as they occur in the versions, so if any updates are required you should start from your current version and apply further updates from bottom to top.

For example: if you are updating from version 6.2.4 to 7.1.0 you'd start from the "From 6.x .." section apply those changes and work your way up:

### From 7.0.x to 7.1.x
 * If you use an IgxGrid with summaries in your application, you should know that now the `IgxSummaryOperand.operate()` method is called with empty data in order to calculate the necessary height for the summary row. For custom summary operands, the method should always return an array of IgxSummaryResult with proper length.

	Before version 7.1:
```typescript	
export class CustomSummary extends IgxNumberSummaryOperand {
	public operate(data?: any[]): IgxSummaryResult[] {
		return [{
			key: 'average',
			label: 'average',
			summaryResult: IgxNumberSummaryOperand.average(data).toFixed(2)
		}];
	}
}
```

	Since version 7.1:
```typescript
export class CustomSummary extends IgxNumberSummaryOperand {
	public operate(data?: any[]): IgxSummaryResult[] {
		return [{
			key: 'average',
			label: 'average',
			summaryResult: data.length ?  IgxNumberSummaryOperand.average(data).toFixed(2) : null
		}];
	}
}
```

### From 6.0.x to 6.1.x

* If you use an IgxCombo control in your application and you have set the `itemsMaxWidth` option, you should change this option to `itemsWidth`